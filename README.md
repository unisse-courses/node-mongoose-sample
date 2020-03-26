# NodeJS mongoose Example
This is the example code for the lecture on mongoose for CCAPDEV, AY2019-2020, Term 2.
It's basically the mongoose version of the [node-mongodb-sample](https://github.com/unisse-courses/node-mongodb-sample) with some modifications and additions.

## Pre-requisite
Complete [node-mongodb-sample](https://github.com/unisse-courses/node-mongodb-sample) first!!!

## Learning Objectives
At the end of going through this example **after** completing the [node-mongodb-sample](https://github.com/unisse-courses/node-mongodb-sample), you should be able to:
1. Compare the differences of using the native MongoDB driver and mongoose
2. Understand how to define the Schema and perform different CRUD operations

## Requirements
* [NodeJS & npm](https://www.npmjs.com/get-npm)
* [MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/)
* Any text editor for JavaScript, HTML & CSS (VSCode, Atom, SublimeText, etc.)

## MongoDB Installation
You should already have mongodb installed if you were able to complete the previous sample. But if not, follow these instructions to install mongodb.

1. Download MongoDB Community Server from [here](https://www.mongodb.com/download-center/community).
2. Follow the instructions for your operating system from [this guide](https://docs.mongodb.com/manual/administration/install-community/).
3. You can also follow along this [YouTube Video by Traversy Media](https://youtu.be/-56x56UppqQ) for installing and using mongo `shell` & MongoDB Compass (similar to MySQL Workbench).
4. Make sure that mongodb is running as a service in the background. Otherwise, this will not work.

## Local Setup
1. Clone this repository: `git clone https://github.com/unisse-courses/node-mongoose-sample.git`
2. Navigate to the directory: `cd node-mongoose-sample`
3. Install the dependencies: `npm install`
    * I've already installed mongoose so it's in the `package.json` file already.
4. Run the server: `node index.js`
    * Navigate to `http://localhost:9090/` in the browser to view the app.

To stop the server, simply key in `CTRL+C` (Windows) or `control (^) + C` (Mac).

##### Note: This repository will only allow you to clone and pull the code provided here. To be able to **push changes**, you need to **fork** this repository to your account and that will allow you to keep a personal copy of any changes you may have.

## What to do next?
This is a **complete** repository already. The application is fully functional and there's no need for you to code anymore.

What you need to do is dig through the code and **compare** this with the mongodb example. There are inline comments in the files. To make things easier, there's a separate [`GUIDE.md`](GUIDE.md) to help you navigate through the process of converting to use mongoose.
