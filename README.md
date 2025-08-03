# react-helmet-async

A thread-safe Helmet for React 16+ that supports modern React features and server-side rendering.

## Why react-helmet-async?

React Helmet is a fantastic library for managing your app's `<head>` tags from within your React component tree. However, the original `react-helmet` has thread safety issues with server-side rendering when using asynchronous operations.

This package solves those problems by:

- **Thread-safe SSR**: Each request gets its own isolated context, preventing data leaks between concurrent requests
- **Modern React support**: Built for React 16+ with support up to React 19
- **Async-friendly**: Works seamlessly with Apollo GraphQL, data fetching, and other asynchronous operations
- **Familiar API**: Drop-in replacement with minimal changes required

Originally created by The New York Times to solve production issues with meta tag management in high-traffic environments.

## Installation

```bash
npm install @vuer-ai/react-helmet-async
# or
yarn add @vuer-ai/react-helmet-async
# or
pnpm add @vuer-ai/react-helmet-async
```

## Quick Start

### Client-side Usage

```jsx
import React from 'react';
import ReactDOM from 'react-dom';
import { Helmet, HelmetProvider } from '@vuer-ai/react-helmet-async';

const App = () => (
  <HelmetProvider>
    <div>
      <Helmet>
        <title>My App</title>
        <meta name="description" content="My awesome React app" />
        <link rel="canonical" href="https://example.com/" />
      </Helmet>
      <h1>Hello World</h1>
    </div>
  </HelmetProvider>
);

ReactDOM.render(<App />, document.getElementById('root'));
```

### Server-side Usage

```jsx
import React from 'react';
import { renderToString } from 'react-dom/server';
import { Helmet, HelmetProvider } from '@vuer-ai/react-helmet-async';

// Create a fresh context for each request
const helmetContext = {};

const app = (
  <HelmetProvider context={helmetContext}>
    <App>
      <Helmet>
        <title>Server-rendered App</title>
        <meta name="description" content="Thread-safe meta tags" />
      </Helmet>
      <h1>Hello World</h1>
    </App>
  </HelmetProvider>
);

const html = renderToString(app);
const { helmet } = helmetContext;

// Use helmet data in your HTML template
const htmlTemplate = `
<!DOCTYPE html>
<html ${helmet.htmlAttributes.toString()}>
<head>
  ${helmet.title.toString()}
  ${helmet.meta.toString()}
  ${helmet.link.toString()}
</head>
<body ${helmet.bodyAttributes.toString()}>
  <div id="root">${html}</div>
</body>
</html>
`;
```

## Key Features

### Thread-Safe Server Rendering

Unlike the original `react-helmet`, this library properly isolates state per request, preventing the common issue where concurrent server requests would corrupt each other's meta tags.

### SEO Tag Prioritization

Prioritize important SEO tags in the `<head>`:

```jsx
<Helmet prioritizeSeoTags>
  <title>Important Title</title>
  <meta property="og:title" content="Social Media Title" />
  <link rel="canonical" href="https://example.com" />
  <meta name="description" content="Page description" />
</Helmet>
```

### Works with Modern Data Fetching

Perfect for use with Apollo GraphQL, Relay, or any async data fetching:

```jsx
import { getDataFromTree } from '@apollo/client/react/ssr';

const helmetContext = {};
const app = (
  <ApolloProvider client={client}>
    <HelmetProvider context={helmetContext}>
      <App />
    </HelmetProvider>
  </ApolloProvider>
);

await getDataFromTree(app);
const html = renderToString(app);
const { helmet } = helmetContext;
```

## API

The API is nearly identical to the original `react-helmet`, with the key difference being the required `<HelmetProvider>` wrapper:

- `<HelmetProvider>` - Provides context for Helmet instances
- `<Helmet>` - Manages head tags (same API as original)
- All the same tag types: `title`, `meta`, `link`, `script`, `style`, `base`, `noscript`
- All the same attributes and props

## React Version Support

This library supports:
- React 16.6+
- React 17.x
- React 18.x  
- React 19.x

## Migration from react-helmet

1. Install `@vuer-ai/react-helmet-async`
2. Replace imports: `react-helmet` → `@vuer-ai/react-helmet-async`
3. Wrap your app with `<HelmetProvider>`
4. Update server-side rendering to use context instead of static methods

That's it! The rest of your `<Helmet>` components work exactly the same.

## License

Licensed under the Apache 2.0 License