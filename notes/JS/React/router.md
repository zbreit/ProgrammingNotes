# React Router
React Router is a package used to create navigation for your React app.

## Components
 - **`<Router>`** Used as the top-level app component. The app's current route will determine which one of the `<Router>`'s children are displayed.
 - **`<Route>`** A given page to be displayed. If the Router's overall path matches a given `<Route>`'s path, that `<Route>` will be displayed.
   - Props
     - **path**: The path to the route (e.g. `'/'`, `'/events'`).
       - It can include parameters (i.e., `'/events:event-id'` means the given route is the string `'/events'` followed by an event id).
       - You can make a parameter optional by enclosing its name in parentheses (i.e., `'/events(:event-id)'`)
     - **component**: The component to display for the route
 - **`<IndexRoute>`** Same as `<Route>`, but gets displayed on the initial render (i.e. the starting route).
 - **`<Link>`** A link to a new route
   - Props
     - **to**: A path to a given route
## Boilerplate
### App.js
```js
import React from 'react';
import ReactDOM from 'react-dom';
import { Router, Route, IndexRoute } from 'react-router';

import { HomeScreen, Events, Settings } from 'my-code';

ReactDOM.render(
    <Router history={hashHistory}>
        <IndexRoute path='/' component={HomeScreen}/>
        <Route path='/events:event-id' component={Events}/>
        <Route path='/settings' component={Settings}/>
    </Router>,
document.getElementById('root'));
```
