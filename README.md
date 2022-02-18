# FullStackApplicationProject

This project was created as practice developing a full state application. The context for this was to create a banking reimbursement system. For a fictional banking company, each employee should be able to make a reimbursement request to their manager with a comment for the reimbursement request. Each manager should be able to approve or reject any request as needed along with adding a comment. In addition, managers should be able to review a statistics page on all employees. Several other additional features were going to be implemented for an admin to directly manipulate a database from the front end. Because of time constraints on the project, these additional features are unfinished but all other features have been completed.

## overview

These applications consist of two main sub-projects: the front end written entirely in React Native using Expo, and the backend written in Express and connected to Azure Cosmos DB. [A pdf is provided](https://github.com/Bednaz98/FullStackApplicationProject/blob/main/Project1-Rembersement-System.pdf) in this repo describing several design features graphically.

### backend

The backend was designed using a _DAO Wrapper_ that could switch between three classes that would access data. The first one interacted directly with Cosmos DB (CosmosDAO). The second (LocalDAO), reads and writes data to a local file. The last one (Virtual DAO), stores all data in variables in memory. The purpose of this was to make switching behaviors of the DAO as easy as possible. This had several advantages:

1. During testing, no API calls were made to Cosmos during testing. This helps to avoid any cost that might arise from too many HTTP calls.
2. Having different functionality aided in debugger different parts of the process.
   - When exclusively working on the backend, having persistent data is not favorable for doing jest tests that requires many asynchronous I/O processes. Using a virtual DAO that only exist for testing, then deleted after made the process easier.
   - When working on the front end, having the Local DAO already have data persistently stored and not having to make API calls to Cosmos made the process easier to debug communication between the front and backend.

### Front end

Axios was used to make HTTP calls to the backend. Rather than having the logic for HTTP requests directly in any given component, an HTTP handler class was created to handle many of the operations. This allowed for cleaner, shorter code and isolated functionality for testing. Along with this, a component library was created to make consistent styling easier. The library consists of a component wrapper that returns already styled JSX elements. The purpose of this was to only have styling be done one and then use the view component to position all other components.

## [License](https://github.com/Bednaz98/FullStackApplicationProject/blob/main/LICENSE)
