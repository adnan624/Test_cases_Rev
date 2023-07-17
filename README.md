# How to Write Test Cases in React using Jest and Enzyme.

## Getting started

In this File, we will write the test cases for our React component from scratch using Jest and Enzyme. Also, 
we will learn more about Jest and Enzyme.

## What is Testing

Testing is a line-by-line review of how your code will execute. A suite of tests for an application comprises various bit of code to verify whether an application is executing successfully and without error. Testing also comes in handy when updates are made to code. After updating a piece of code, you can run a test to ensure that the update does not break functionality already in the application.

## Why Testing ?
It’s good to understand why we doing something before doing it. So, why test, and what is its purpose?

1--->The first purpose of testing is to prevent regression. Regression is the reappearance of a bug that had previously been fixed. It makes a feature stop functioning as intended after a certain event occurs.
2--->Testing ensures the functionality of complex components and modular applications.
3--->Testing is required for the effective performance of application or product.

## What Is Jest?
Jest is a JavaScript test runner that provides resources for writing and running tests. React Testing Library offers a set of testing helpers that structure your tests based on user interactions rather than components' implementation details.

## What Is Enzyme?

Enzyme is a JavaScript Testing utility for React that makes it easier to assert, manipulate, and traverse your React Components' output. It was developed at Airbnb and later transferred to an independent organization.

## Installing and Configuring Jest
we will be installing Jest and writing tests, then will be using Create React App, because it is ready for use and ships with Jest.

npx create-react-app my-app

npm install --save-dev enzyme enzyme-adapter-react-16 react-test-renderer

Now that we have created our project with both Jest and Enzyme, we need to create a setupTest.js file in the src folder of the project. The file should look like this:

import { configure } from "enzyme";
import Adapter from "enzyme-adapter-react-16";
configure({ adapter: new Adapter() });

This imports Enzyme and sets up the adapter to run our tests.

let’s learn some basics, What is 'it or test' , 'describe' , 'expect' , 'mount' , 'shallow' ?
1. it or test --You would pass a function to this method, and the test runner would execute that function as a block of tests.
2. describe --This optional method is for grouping any number of it or test statements.
3. expect --This is the condition that the test needs to pass. It compares the received parameter to the matcher. It also gives you access to a number of matchers that 4. let --you validate different things. You can read more about it in the documentation.
5. mount --This method renders the full DOM, including the child components of the parent component, in which we are running the tests.
6. shallow --This renders only the individual components that we are testing. It does not render child components. This enables us to test components in isolation.

## Unit testing
It is an essential and integral part of the software development process that helps us ensure the product’s stability.
It is the level of testing at which every component of the software is tested.

## Significance of unit testing
It helps us improve the quality of code.
In a world of changing requirements, it helps us identify future breaks.
Since bugs are found early, it helps us reduce the cost of bug fixes.

Create our first test, for a React mini-application created for this Documentation.
Run npm install to install all of the packages, and then npm start to launch the app. 

## Step 1: Install the create-react-app npm package with the following command in the desired location.
npm install -g create-react-app

## Enzyme installation

npm install –save-dev enzyme
npm install –save-dev enzyme-adapter-react-16

## Writing the first test case

Add the following code in the App.test.tsx file, which is the file where we write test cases.

import React from 'react'
import Enzyme, { shallow } from 'enzyme'
import Adapter from 'enzyme-adapter-react-16'
import App from './App'

Enzyme.configure({ adapter: new Adapter() })

describe('Test Case For App', () => {
  it('should render button', () => {
    const wrapper = shallow(<App />)
    const buttonElement  = wrapper.find('#ClickMe');
    expect(buttonElement).toHaveLength(1);
    expect(buttonElement.text()).toEqual('Click Me');
  })
})

In the previous code example, we stored the shallow renderer of the App component in the wrapper variable. We can access the length and text of the button inside the Button tag within the component’s output, and we can also check if the text we passed matches the toEqual match function.

## Use the following command to run the test cases.

npm test

## Test with user interaction
Let’s write a new test case that simulates clicking a button component and confirms its dependent actions.

## Step 1: Add the following code in the App.tsx file.

import React, { Component } from 'react';
import './App.scss';

class App extends React.Component<any, any> {
  constructor(props: any) {
    super(props);
    this.state = {
      ClickCount:0
    };
    this.ClickMe = this.ClickMe.bind(this);
}

ClickMe(){
  this.setState({
    ClickCount:this.state.ClickCount + 1
  });
}

  render() {
    return (
      <div>       
        <button id="ClickMe" className="click-me" onClick={this.ClickMe}>Click Me</button>
        <p>You clicked me :: {this.state.ClickCount}</p>
      </div>
    )
  }
};

export default App;

## Step 2: Add the following code snippet in the App.test.tsx file.

import React from 'react'
import Enzyme, { shallow } from 'enzyme'
import Adapter from 'enzyme-adapter-react-16'
import App from './App'

Enzyme.configure({ adapter: new Adapter() })

describe('Test Case For App', () => {
  it('should render button', () => {
    const wrapper = shallow(<App />)
    const buttonElement  = wrapper.find('#ClickMe');
    expect(buttonElement).toHaveLength(1);
    expect(buttonElement.text()).toEqual('Click Me');
  }),
  
  it('increments count by 1 when button is clicked', () => {
    const wrapper = shallow(<App />);
    const buttonElement  = wrapper.find('#ClickMe');
    buttonElement.simulate('click');
    const text = wrapper.find('p').text();
    expect(text).toEqual('You clicked me :: 1');
  });
})

## Step 3: Run the npm test command to run the test cases in the desired application location. 

## Test case for state variable

## Step 1: Add the below code snippet in the App.tsx file.

import React, { Component } from 'react';
import './App.scss';

class App extends React.Component<any, any> {
  constructor(props: any) {
    super(props);
    this.state = {
      ClickCount:0,
      IamDisabled : true
    };
    this.ClickMe = this.ClickMe.bind(this);
}

ClickMe(){
  this.setState({
    ClickCount:this.state.ClickCount + 1
  });
}

  render() {
    return (
      <div>       
        <button id="ClickMe" className="click-me" onClick={this.ClickMe}>Click Me</button>
        <p>You clicked me :: {this.state.ClickCount}</p>
        <button id=" IamDisabled " className="click-me" disabled={this.state.IamDisabled}>Disabled</button>
      </div>
    )
  }
};

export default App;

## Step 2: Add the following code snippet in the App.test.tsx file.

import React from 'react'
import Enzyme, { shallow } from 'enzyme'
import Adapter from 'enzyme-adapter-react-16'
import App from './App'

Enzyme.configure({ adapter: new Adapter() })

describe('Test Case For App', () => {
  it('should render button', () => {
    const wrapper = shallow(<App />)
    const buttonElement  = wrapper.find('#ClickMe');
    expect(buttonElement).toHaveLength(1);
    expect(buttonElement.text()).toEqual('Click Me');
  }),
  
  it('increments count by 1 when button is clicked', () => {
    const wrapper = shallow(<App />);
    const buttonElement  = wrapper.find('#ClickMe');
    buttonElement.simulate('click');
    const text = wrapper.find('p').text();
    expect(text).toEqual('You clicked me :: 1');
  });
})


describe('Test Case for App Page', () => {
    test('Validate Disabled Button disabled', () => {
        const wrapper = shallow(
            <App />
        );
        expect(wrapper.state('IamDisabled')).toBe(true);
    });
});

## Conclusion

 we have learned how to do unit testing in React with the Jest and Enzyme frameworks. With this in your toolkit, you can check the stability of your app and also enhance the quality of the code



