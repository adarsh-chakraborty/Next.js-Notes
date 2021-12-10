# Next.js

#### What is Next.js? and why would we use it?

Next.js calls itself a **React Framework for Production** and that name makes alot of sense, but what that really means.

**"Next.js offers alot of features that make building large scale production ready, React apps easier."**

Where React is a library and focused on building user interfaces and in the end, it's all client side javascript.

Next.js is a Framework built on React, It offers alot more than building user-interfaces which we have to add our own otherwise, like routing and other third party libraries. Out of the Box!

### Key Features of Next.js

#### 1. Server Side Rendering

Next.js supports server side rendering out of the box, Server Side Rendering is all about preparing the content of the page on the server instead on the client. It automatically pre-renders the content without any extra setup from our side. By Default. Out of the Box.

#### 2. File based routing

We don't even get a routing system with react. We have to install a third party library for routing, that's not it. The route we setup in react is in our code.

Next.js gets rid of that in-code route definition, Instead with Next.js we get file based routing system.We define our pages and routes with files and folders.

#### 3. Fullstack Capabilities

We can add some code which can work with filesystem or reaches out to database. We can have some standalone database related code with Next.js

With Next.js, It's very easy to add our own Backend API to our react project using Node JS code.

***
## Creating a new Next.js app

Make sure to have Node js Installed on the system and then run the following command:

```shell
npx create-next-app
```
### Nested Routing

Routing of the app is based on files & folders in the `pages` folder.

Each file is a route, and every new folder enables us to create nested routes.

```shell
pages > news.js = /news
pages > news > index.js = /news 
pages > news > latest.js = /news/latest
```

### Dynamic Routing

Using the same pages over and over again, with different data & content served to user.

To create a dynamic page, Change the filename to some identifer between square brackets **[identifer].js** Now next.js can load this file for different values in the page `/someID`. 

**Alternatively,** You can change the folder name to be the identifier `[someId]` and inside the folder, you can have an `index` file. 

#### Extracting the value from URL

To get the user's entered value from the URL, import the `useRouter` hook from package `next/router`

```javascript
import { useRouter } from 'next/router';

function DetailPage(){
    const router = useRouter(); 
    console.log(router.query.identifer);
    // here newsID is the identifer. i.e [newsId].js 
    const someId = router.query.newsId;

    return <h1>Detail Page</h1>
}
```

Explaination:
- import `{ useRouter }` hook from `next/router`.
- call the hook in the component, it returns a router object.
- the router object has certain pieces of data and methods we can call.
- we can get the current parameter in the url by `router.query.identier` where identifer is the filename enclosed in `[filename].js`

That's how we can build dynamic pages based on some parameter in the url.

---

# Navigation

We can use Link component instead of normal anchor tags, Link component prevents the browser default of refreshing page.

```javascript
import Link from 'next/link';

function NewsPage(){
    return <ul><li>
    <Link href="/news/next12">Next JS v12</Link>
    </li></ul>;
}
```

Explaination:
- import `Link` component from `next/link` as default.
- Use the Link component instead of anchor tag. It even has a `href` prop for url.
- Link renders an anchor element in html but without re-loading the page.

### Programmatic Navigation

We can navigate the user to some place Programmatically by using `useRouter` hook.

```javascript
import { useRouter } from 'next/router';

function MeetupItem(props) {
  const router = useRouter();
  const showDetailsHandler = () => {
    router.push('/'+props.id);
  }
  return ();
}

export default MeetupItem;
```

`router.push('/some-path')` pushes a new link to navigation stack just like `Link` component.

---
# _app.js file

There exists a file named `_app.js` in `pages` folder, It's a special file.

It's a kind of root component that nextjs will render, It uses props to receive data and destructure them to pull information out of props. i.e `{ Component, pageProps }`

- Component prop is the page that is rendered, so it will be different for each page.
- pageProps are specific props that our page might be getting.

Now we know that _app.js is the actual page content for our app, and It will change from pageA to pageB.

If we have any central layout for our entire app, It's the best place to wrap the entire app with a layout component.

```javascript
import '../styles/globals.css';
import Layout from '../components/layout/Layout';

function MyApp({ Component, pageProps }) {
  return (
    <Layout>
      <Component {...pageProps} />
    </Layout>
  );
}

export default MyApp;
```


