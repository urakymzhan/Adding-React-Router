---
Adding React Router
---

- [This page upgraded to RR V6 from v5](https://reactrouter.com/docs/en/v6/upgrading/v5)

The project you have built is described as a **single page application** but most web pages we use daily are built as, or at least act as, multi-page applications.

A single page application is just that: a single html page. Single page applications control the DOM by updating, adding, or removing elements. In this way they can function as multi-page applications.

A single page application built with React can display different content through components. Components can represent whole pages of content in a React app.

You can use the React Router library to make your React apps function like multi-page apps. You'll add a sub-page for each public place location. These sub-pages will show detailed information about each location.

# React Router

**React Router** is a library that can create a multipage experience in React. It does this by selectively rendering components. You'll define components that render at routes. A **route** is an address that appears in the address bar of the browser.

To work with React Router it helps to understand some terminology.

- **Router** - A parent component that manages Routes
- **Route** - A component that displays another component

Think of the Router as the manager, you only need one of these. The Router checks the URL in the address bar and passes this information to its descendant Routes.

Imagine a website with three pages built with React using React Router. The Router and Route components might be arranged like this:

- Router
  - Route - Home Page
  - Route - About Page
  - Route - Map Page

A Route is responsible for displaying components. Routes have a path property: when the path matches the URL in the address, the Route displays the appropriate component, otherwise not.

In code this might look like:

```js
<Router>
  <Route path='/home' ... />
  <Route path='/about' ... />
  <Route path='/home' ... />
</Router>
```

**Important!** The two names: Router and Route are different by only a single character, but they are very different in function and must be used correctly. Watch your spelling!

# Getting started

The first step to using React Router is to import it.

> [action]
>
> Got to the terminal and run:
>
> `npm install react-router-dom`

This should import the React Router libraries as a dependency to your project.

Coming up, you'll import `HashRouter` into `App.js`. This is a component that manages routes.

> [info]
>
> Quick note! `HashRouter` and `BrowserRouter` are two options. They act the same in our app and only differ in how they handle the URL/Path.
>
> HashRouter includes a # in the URL, while BrowserRouter does not include the #.
>
> For example a HashRouter URL might look like this:
>
> `http://localhost:3000/#/about`
>
> The same URL in BrowserRouter would look like this:
>
> `http://localhost:3000/about`
>
> Why use one or the other? In most cases they are interchangeable. Since we plan to publish the completed site to GitHub pages in the future, we're using HashRouter because GitHub pages doesn't work with BrowserRouter!

## Setting up the Router

Router manages routes. It should be a top level component. For this reason you'll define your Router in `App.js`.

> [action]
>
> Open `App.js`. Import `HashRouter` and `Route` at the top.

```js
import { HashRouter as Router, Route } from "react-router-dom";
```

Why `HashRouter as Router`? This is an alias. You're importing HashRouter but using it under the name `Router` instead. This will make it easier to make changes in the future if needed.

> [action]
>
> Next, Wrap your entire App in the `<Router>` component.

```JS
function App() {
  return (
    <Router>

      <div className="App">
        <Title />
        <PLACESList />
          // maybe footer if you did previous stretch challenge
         <PageFooter/>
      </div>

    </Router>
  );
}
```

Notice how Router surrounds everything. Routes must be children of a Router!

### Adding Routes

A route displays a component as a path. You want the `PLACESList` to display at the `/` path.

> [action]
>
> Update the `App` function in `App.js` to the following:

```js
function App() {
  return (
    <Router>
      <div className="App">
        <Title />
        <Routes>
          <Route path="/" element={<PLACESList />} />
        </Routes>
        <PageFooter />
      </div>
    </Router>
  );
}
```

Make sure to wrap `Routes` your `Route`'s.

Notice when you created the Route you used two props: `path` and `element`. Path defines the URL that will make the component display.

The `/` route is the root route. So the list should display now at `http://localhost:3000/`. In your browser, add something to the end of the path in the address bar, and see what happens when you try to navigate to it. Try this as an example:

`http://localhost:3000/#/about`

> [action]
>
> Make this change to the `Route` in `App.js`:

```js
<Route path="/" element={<PLACESList />} />
```

Now try these paths in the address bar of the browser:

## Adding another route

Your site could use an About page. Let's create a new component!

> [action]
>
> Make a new file `src/About.js` with the following code:

```JS

function About() {
  return (
    <div>
      <h1>About CHICAGOTOUR</h1>
      <p>Chicago, on Lake Michigan in Illinois, is among the largest cities in
      the U.S. Famed for its bold architecture, it has a skyline punctuated by skyscrapers such as
      the iconic John Hancock Center, 1,451-ft.
      Willis Tower (formerly the Sears Tower) and the neo-Gothic Tribune Tower.
      The city is also renowned for its museums,
      including the Art Institute of Chicago with its noted
      Impressionist and Post-Impressionist works. </p>
    </div>
  )
}

export default About
```

This component will display a heading and a paragraph of text. You can add some styles later, and maybe a picture and more info like a map. For now we are concerned with Routes.

> [action]
>
> Back in `App.js` import the `About` Component at the top.

```js
import About from "./About";
```

> Inside the `Router`, add a new `Route`:

```js
...
<Router>
  <div className="App">
    <title />
      <Routes>
        <Route path="/" element={<PLACESList/>} />
        <Route path="/about" element={<About/>} />
      </Routes>
    <PageFooter />
  </div>
</Router>
...
```

Notice the new route has a path of `/about` and renders the `About` component.

Save your work and try it in the browser. Try these two paths in the address bar:

Should display the list

`http://localhost:3000/#/`

Should display the about page

`http://localhost:3000/#/about`

# Linking to Routes

This is working but we can't ask people to navigate to pages by typing the URL, people need something to click!

React Router provides a `NavLink` component. The `NavLink` sets the address to navigate to in our browser's URL bar, and navigates the user to that address. It's like the `<a>` tag but specific to React Router.

> [action]
>
> Add two links to the Title Component. Open `Title.js`. Add this to the top of the page:

```js
import { NavLink } from "react-router-dom";
```

here you've imported `NavLink` from React Router DOM.

> [action]
>
> Now add two links to your `Title` in `src/Title.js`. Note below we also have the subtitle from an earlier stretch challenge:

```js
function Title() {
  return (
    <div className="Title">
      <header>
        <h1>CHICAGOTOUR</h1>
        <div className="Title-Subtitle">Chicago Places to Visit</div>

        <div>
          <NavLink to="/">List</NavLink>
          <NavLink to="/about">About</NavLink>
        </div>
      </header>
    </div>
  );
}
```

Notice that each `NavLink` has a `to` prop. This sets what the path in the address bar will become when you click this link.

Try it out in your browser!

The `NavLink`s need some style. `NavLink` translates to a regular anchor `<a>` tag in the DOM. You can treat these like any other tag/component:

> [action]
>
> In `src/Title.js`, give the NavLinks a class name:

```js
<NavLink className="nav-link" to="/">List</NavLink>
<NavLink className="nav-link" to="/about">About</NavLink>
```

> Then, open `src/Title.css` and add some styles.

```CSS
.Title .nav-link {
  display: inline-block;
  padding: 0.5em 1em;
  color: rgba(255, 255, 255, 0.835);
  font-weight: bold;
  text-decoration: none;
}
```

This looks better, but you could do more! Currently the active link (the link that represents the current "page") doesn't stand out from the other links. It should, as this would help users understand where they are what they can do, thereby improving the UX (User eXperience).

You can pass a function to either style or className that will allow you to customize the inline styling or the class string based on the component's active state.

> [action]
>
> _Edit_ your `NavLink`s in `src/Title.js` to be the following:

```js
    <NavLink
      to="/"
      className={({ isActive }) => "nav-link" + (isActive ? "-active" : "")}
    >
      Home
    </NavLink>
    <NavLink
      to="/about"
      className={({ isActive }) => "nav-link" + (isActive ? "-active" : "")}
    >
      About
    </NavLink>
```

With these options, the selected `NavLink` will have the class: `nav-link-active`. You should add a style for this!

> [action]
>
> Add the following to `src/PageHeader.css`:

```CSS
.Title .nav-link-active {
  color: #fff;
  display: inline-block;
  padding: 0.5em 1em;
  font-weight: bold;
}

```

# Details page Route Parameters

Things are looking pretty good. Now let's tackle the details page. The details page will be a page that is dedicated to a single location. It will show all of the information for that location. Right now we show all locations on the List Page but the information is minimal. The details page will be a page dedicated to just one location.

Currently there are only a small number of places in our data list, but there are a lot more places that might be added in the future. We don't want to make a component for each place. Instead you will make a single component and pass props to it containing the information that needs to display.

When you made the list of `PLACESSpace` components, you passed all of the values the component displays into the component via props. You also made all of those components in the list with `map()`.

This time you'll take a different approach. In this situation you want to make a single component and you'll be displaying it with React Router as a Route. Router allows you to pass values to a Route through the URL/path. This is good for this use because the URL/path can be bookmarked, Which will allow visitors to bookmark a detail page or return to it directly by entering its URL.

### Making the Details Component

This component will be a lot like the `PLACESSpace` component but will show more details. Let's call it `PLACESDetails`.

Where the `PLACESpace` component showed the image, title, and address. The `PLACESDetails` component will show all of the images (remember images in the data is an _array_), title, address, description, hours, and features of a single place.

Remember how all of the data is in the `places-data.json` file? Any of your components can import this file. As long as a component knows the index of the item in the data, it can display it.

The goal then is to pass the index to the `PLACESDetails` component, and `PLACESDetails` will get the information it needs from the data.

> [action]
>
> Make a new file named: `src/PLACESDetails.js`, and add the following code to it:

```js
// src/PLACESDetails.js

import data from "./places-data.json";

function PLACESDetails(props) {
  const { id } = props.match.params; // Location index
  const { images, title, desc, hours, features, geo } = data[id];

  return (
    <div>
      <div>
        <img src={`${process.env.PUBLIC_URL}/images/${images[0]}`} />
      </div>

      <div>
        <h1>{title}</h1>
        <p>{desc}</p>
        <p>{hours}</p>
        <p>{features}</p>
        <p>
          {geo.lat} {geo.lon}
        </p>
      </div>
    </div>
  );
}

export default PLACESDetails;
```

The code above is just like the other components you've made. One small change is at the top you've imported `sfPLACES-data.js`.

Inside the function you defined a variable: `id` and set the value to `props.match.params`.

`const { id } = props.match.params // Location index`

On the next line you're using the `id` to get the data for the location at the index. Using deconstruction we can break object at that index down into: `images`, `title`, `desc`, `hours`, `features`, and `geo` coordinates.

The rest of the component is similar to the other components you wrote previously. Feel free to modify this and add styles. Notice that `images` is an array to display images. For example, you're using `images[0]` to get the first image in this array.

### Details Route

Set up a Route to display the details component.

> [action]
>
> Open `App.js`, and add an import for `PLACESDetails.js` at the top:

```js
import PLACESDetails from "./PLACESDetails";
```

> Then in `App.js`, within the return block of the component, make a new Route below the existing Routes:

```js
<Route path="/details/:id" element={<PLACESDetails />} />
```

Notice the path here is different. `path="/:id"` it contains a `:`. This is a parameter. The value following the `/` is now a variable and can be anything. For example:

`http://localhost:3000/#/0` `id` would be 0

or

`http://localhost:3000/#/13` `id` would be 13

You have access to this value inside a Route with: `useParams()`

Take a look back at `src/PLACESDetails.js` somewhere around line 6 you should have:

`const { id } = useParams()`

Here you get the value of id.

You can test your work by trying these addresses in your browser:

`http://localhost:3000/#/details/0`
`http://localhost:3000/#/details/1`
`http://localhost:3000/#/details/2`

What's important here is your app can find a details page by entering a URL. A user now could go directly to a page by entering that address, they could also bookmark a page.

### Passing the id

To be able to link to something with an id we need to have that id. Here in this step you'll pass the id to a `PLACESSpace` from `PLACESList`.

> [action]
>
> Open `PLACESList.js`. Find the line where you mapped data to the `PLACESSpace` via the `spaces` const, and edit it to be the below code. Notice the small changes with `i` and `id`:

```JS
const spaces = data.map(({ title, address, images, hours }, i) => {
  return (
    <PLACESSpace
      id={i}
      key={title}
      name={title}
      address={address}
      image={images[0]}
      hours={hours}
    />
  )
})
```

On the first line there is a second parameter to:

`map(obj, i)`, or

`map({ ... }, i)`. here is the whole line as it is shown above:

`const spaces = data.map(({ title, address, images, hours }, i) => {`

The second change is the added prop `id={i}` in the `PLACESSpace` component.

```js
<PLACESSpace id={i} // added new prop id here! ... />
```

When using `map()` this method provides the index of the element as a second parameter. This is useful in many cases, you're using it here as the index of the data from our JSON data.

You can now access this index inside an instance of `PLACESSpace` as `props.id`.

# Linking to Details

With the last piece in place you can get to the details Route. This is good but you really want visitors to be able to click a location in the list and show its details.

For a page to link to its details, it needs to know the index in the array where its data is stored. This will happen in `PLACESList`.

You can also do this by using a `<Link>` component. `<Link>` is a component provided by React Router for linking/navigating to different Routes.

`Link` is different from `NavLink` in that `NavLink` is used for top level navigation that would be visible on all pages. `Link` on the other hand is for general navigation that might appear anywhere else. The big difference is `NavLink` offers the extra feature of `activeClassName` and `Link` doesn't have this.

Let's make some links in the `PLACESSpace`. It's probably best if people can click both the title and image to link to the detail page.

> [action]
>
> In `src/PLACESpace.js`, import the Link component at the top.

```js
import { Link } from "react-router-dom";
```

Since id should now be passed as a prop you can access it with:

`props.id`

or deconstruct it with:

`const { id } = props`

Or if you're already deconstructing props just add it to the list:

`const { name, image, address, hours, id } = props`

> [action]
>
> In `src/PLACESpace.js`, first add `id` to your props. Then wrap the `img` in a `Link`. You should have something like this:

```js
const { name, image, address, hours, id } = props

...

<Link to={`/details/${id}`}>
  <img src={`${process.env.PUBLIC_URL}/images/${image}`} width="300" height="300" alt="Hello" />
</Link>
```

Notice the `to` path! Remember the path will look for a param following the `/`. Here the param will be the id!

> [action]
>
> In `src/PLACESpace.js`, do the same with the title:

```js
<h1>
  <Link to={`/details/${id}`}>{name}</Link>
</h1>
```

Check your work! Clicking a link should take you to the detail page for that location.

# Now Commit

> [action]

```bash
$ git add .
$ git commit -m 'added routes'
$ git push
```
