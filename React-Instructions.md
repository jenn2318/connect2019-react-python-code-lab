# Create React-App Instructions

## We want to setup the front end using create react app:
$ npm install -g create-react-app

## Next you want to setup your application to be called front end:
$ create-react-app frontend

# Run the following commands to navigate into the working directory and start the frontend server
$ cd frontend
$ npm start

## We can now visit this address — http://localhost:3000 — to see the default React app


## Let's style the UI with bootstrap and reactstrap with the following commands:
$ yarn add bootstrap reactstrap


### Let’s open the src/index.css file and replace the styles there with this one:

 /__ frontend/src/index.css  __/

    body {
      margin: 0;
      padding: 0;
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", "Roboto", "Oxygen",
        "Ubuntu", "Cantarell", "Fira Sans", "Droid Sans", "Helvetica Neue",
        sans-serif;
      -webkit-font-smoothing: antialiased;
      -moz-osx-font-smoothing: grayscale;
      background-color: #282c34;
    }
    .todo-title {
      cursor: pointer;
    }
    .completed-todo {
      text-decoration: line-through;
    }
    .tab-list > span {
      padding: 5px 8px;
      border: 1px solid #282c34;
      border-radius: 10px;
      margin-right: 5px;
      cursor: pointer;
    }
    .tab-list > span.active {
      background-color: #282c34;
      color: #ffffff;
    }

### We will import Bootstrap’s stylesheet in src/index.js so that we can use Bootstrap’s classes:

import React from 'react';
      import ReactDOM from 'react-dom';
      import 'bootstrap/dist/css/bootstrap.min.css';       // add this
      import './index.css';
      import App from './App';
      import * as serviceWorker from './serviceWorker';


## Let’s replace the code in src/App.js with this one:
// frontend/src/App.js

    import React, { Component } from "react";
    const todoItems = [
      {
        id: 1,
        title: "Go to Market",
        description: "Buy ingredients to prepare dinner",
        completed: true
      },
      {
        id: 2,
        title: "Study",
        description: "Read Algebra and History textbook for upcoming test",
        completed: false
      },
      {
        id: 3,
        title: "Sally's books",
        description: "Go to library to rent sally's books",
        completed: true
      },
      {
        id: 4,
        title: "Article",
        description: "Write article on how to use django with react",
        completed: false
      }
    ];
    class App extends Component {
      constructor(props) {
        super(props);
        this.state = {
          viewCompleted: false,
          todoList: todoItems
        };
      }
      displayCompleted = status => {
        if (status) {
          return this.setState({ viewCompleted: true });
        }
        return this.setState({ viewCompleted: false });
      };
      renderTabList = () => {
        return (
          <div className="my-5 tab-list">
            <span
              onClick={() => this.displayCompleted(true)}
              className={this.state.viewCompleted ? "active" : ""}
            >
              complete
            </span>
            <span
              onClick={() => this.displayCompleted(false)}
              className={this.state.viewCompleted ? "" : "active"}
            >
              Incomplete
            </span>
          </div>
        );
      };
      renderItems = () => {
        const { viewCompleted } = this.state;
        const newItems = this.state.todoList.filter(
          item => item.completed == viewCompleted
        );
        return newItems.map(item => (
          <li
            key={item.id}
            className="list-group-item d-flex justify-content-between align-items-center"
          >
            <span
              className={`todo-title mr-2 ${
                this.state.viewCompleted ? "completed-todo" : ""
              }`}
              title={item.description}
            >
              {item.title}
            </span>
            <span>
              <button className="btn btn-secondary mr-2"> Edit </button>
              <button className="btn btn-danger">Delete </button>
            </span>
          </li>
        ));
      };
      render() {
        return (
          <main className="content">
            <h1 className="text-white text-uppercase text-center my-4">Todo app</h1>
            <div className="row ">
              <div className="col-md-6 col-sm-10 mx-auto p-0">
                <div className="card p-3">
                  <div className="">
                    <button className="btn btn-primary">Add task</button>
                  </div>
                  {this.renderTabList()}
                  <ul className="list-group list-group-flush">
                    {this.renderItems()}
                  </ul>
                </div>
              </div>
            </div>
          </main>
        );
      }
    }
    export default App;
    
   
  ## Create a components folder in the src directory:
    $ mkdir src/components
    
    
   ## Create a Modal.js file in the components folder:
    $ touch src/components/Modal.js
    
    
     Open the Modal.js file and populate it with the code snippet below:
    
    // frontend/src/components/Modal.js

    import React, { Component } from "react";
    import {
      Button,
      Modal,
      ModalHeader,
      ModalBody,
      ModalFooter,
      Form,
      FormGroup,
      Input,
      Label
    } from "reactstrap";

    export default class CustomModal extends Component {
      constructor(props) {
        super(props);
        this.state = {
          activeItem: this.props.activeItem
        };
      }
      handleChange = e => {
        let { name, value } = e.target;
        if (e.target.type === "checkbox") {
          value = e.target.checked;
        }
        const activeItem = { ...this.state.activeItem, [name]: value };
        this.setState({ activeItem });
      };
      render() {
        const { toggle, onSave } = this.props;
        return (
          <Modal isOpen={true} toggle={toggle}>
            <ModalHeader toggle={toggle}> Todo Item </ModalHeader>
            <ModalBody>
              <Form>
                <FormGroup>
                  <Label for="title">Title</Label>
                  <Input
                    type="text"
                    name="title"
                    value={this.state.activeItem.title}
                    onChange={this.handleChange}
                    placeholder="Enter Todo Title"
                  />
                </FormGroup>
                <FormGroup>
                  <Label for="description">Description</Label>
                  <Input
                    type="text"
                    name="description"
                    value={this.state.activeItem.description}
                    onChange={this.handleChange}
                    placeholder="Enter Todo description"
                  />
                </FormGroup>
                <FormGroup check>
                  <Label for="completed">
                    <Input
                      type="checkbox"
                      name="completed"
                      checked={this.state.activeItem.completed}
                      onChange={this.handleChange}
                    />
                    Completed
                  </Label>
                </FormGroup>
              </Form>
            </ModalBody>
            <ModalFooter>
              <Button color="success" onClick={() => onSave(this.state.activeItem)}>
                Save
              </Button>
            </ModalFooter>
          </Modal>
        );
      }
    }
    
    
    
    Now let's make your own Todo List App with your own ideas....
