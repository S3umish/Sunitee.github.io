---
layout: post
title:      "Thinking In React "
date:       2021-06-25 19:26:03 +0000
permalink:  thinking_in_react
---


"One of the many great parts of React is how it makes you think about apps as you build them. " 

**What is React ??**, its a  frontend framework which allows the web developers create and design new applications. It is built entirely out of JavaScript with a combination of dependencies. The best part of React is that it provides a specific way to organize and structure the design of a web application. React framework is maintained by Facebook. React Native is used for development of mobile apps. 

 NPM **Node Package Manager** is the set of files or a package containing reusable code, is installed to load React.
 
 JSX, **JavaScript extension** is an extension of vanilla JavaScript with a specific syntax , which looks like HTML, is used to create components of the React app. 
 
 **Components**, the JSX snippets  are the building blocks, they lets us separate code based on the functionality , in a logical and easy way to read and produce highly reusable independent chunk of code. 
 
 Separation of concern and Single Responsibility Principal is applied to arrange the code in a readable fashion.
 
 React has more awesome features, few of them  are highlighted here :
 
**A virtual DOM** ,  renders content in a fast and efficient manner, helps design higly interactive apps.

**A declarative writing** structure helps design user friendly apps .

**Babel** a transpiler , which converts modern Javascript and custom code like JSX into more widely compatible Javascript.

**Webpack** is a bundler that takes all our work along with any required dependency code and packages it all up in a single transferable bundle.

**create-react-app** tool setsup a preconfigured default project from scratch which gets ready to launch with npm start.

**npm start** is the command to start a server for the app to run on. It will host the app and open a browser window to display it. If we make changes in the app and the server is running, it will display and update the app in the browser and display any errors.

**App.js** is the topmost level called the parent component of our react app. It includes all dependencies, imports and exports, Provider, Dom, Reducers, Store and Developmental Tools.

Here's the snippet of  folder App.js  , which is nested under src folder of the app.


```
// src > App.js

import React,{ Component } from 'react';
import { connect } from 'react-redux';
import './App.css';

import CarsContainer from './containers/CarsContainer';
import CarForm from './containers/CarForm'

import Home from './components/Home'
import About from './components/About'
import Footer from './components/Footer'
import Navigation from './components/Navigation'

import {
  BrowserRouter as Router,
  Switch,
  Route
} from "react-router-dom";

import 'bootstrap/dist/css/bootstrap.min.css'


class App extends Component {
  render(){
  return (
  
    <Router>
      <div className="App">
        <Navigation /> 
        <Switch>
          <Route exact path= "/">
            <Home />
          </Route>  
          <Route exact path= "/about">
            <About />
          </Route>  
          <Route  exact path= "/cars">
            <CarsContainer />
          </Route> 
          <Route exact path= "/cars/new">
            <CarForm />
          </Route> 

        </Switch>
          <Footer/>
      
    </div>
    </Router>
       
  );
  }
}

export default connect()(App);

```



Hope this information will help newbies to "React module" get excited for the latest in the apps development.

Happy Coding !!





