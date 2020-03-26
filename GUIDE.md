# 🧭 Code Navigation Guide
Use this guide to navigate through the steps taken to understand the changes that went through the code from using mongodb to using mongoose! 🔎

## Defining the Schema
Before anything else in mongoose, we need to create the schema. Following the best practice of [one schema/model per file](https://developer.mozilla.org/en-US/docs/Learn/Server-side/Express_Nodejs/mongoose), go to [`models`](models). We currently only have one file.

Read through the comments and the code in [`models/student.js`](models/student.js).

## Using the Model
Go to [`index.js`](index.js). At the very top, there's a new import statement:
```JavaScript
// Importing the model
const studentModel = require('./model/student');
```
This is needed so that we can use the functions of the model.

## Querying All Students
Next up is the `/students` route. In the previous example, we retrieved all data from the database and passed it to the `handlebars` template ([`views/students.hbs`](views/students.hbs)).

Now, we're doing the same but we're using the `studentModel` object to retrieve data from the mongodb database.
```JavaScript
// Students route
app.get('/students', function(req, res) {
  studentModel.find({}).sort({ name: 1 }).exec(function(err, result) {
    var studentObjects = [];

    result.forEach(function(doc) {
      studentObjects.push(doc.toObject());
    });

    res.render('students', { title: 'Students', students: studentObjects });
  });
});
```

In the file, you can read through the comments in [`index.js`](index.js) for each part of this code block. Note that the `forEach` loop is to be able to bypass the [`handlebars` error](https://dev.to/abourass/how-to-solve-the-own-property-issue-in-handlebars-with-mongoose-2l7c). You can try replacing the last line with this:
```JavaScript
res.render('students', { title: 'Students', students: studentObjects });
```

This will cause the [Students](http://localhost:9090/students) page to show nothing and the console to log an error.

## Adding a Student
Next up is the `/addStudent` API enpoint. In this chunk, we create an instance of the `studentModel` using the data from the request body. Read through the comments in [`index.js`](index.js).

```JavaScript
// Inserts a student in the database
app.post('/addStudent', function(req, res) {
  var student = new studentModel({
    name: req.body.name,
    id: req.body.id,
    img: `img/${req.body.gender}.png`
  });

  student.save(function(err, student) {
    var result;

    if (err) {
      console.log(err.errors);

      result = { success: false, message: "Student was not created!" }
      res.send(result);
      // throw err;
    } else {
      console.log("Successfully added student!");
      console.log(student);

      result = { success: true, message: "Student created!" }
      res.send(result);
    }
  });
});
```

## Finding a Student
The `/searchStudents` API endpoint is pretty much the same as the mongodb example. It's just a lot less shorter because we don't need to keep connecting to the database anymore.

```JavaScript
// Finds the students matching the name query from the database and returns the array
app.post('/searchStudents', function(req, res) {
  var pattern = "^" + req.body.name;

  studentModel.find({ name: { $regex: pattern } }, function(err, students) {
    console.log(students);
    res.send(students);
  });
});
```

## Updating a Student
For updating, try this in [Postman](https://www.postman.com/). There shouldn't be any changes anymore to the configuration from what you've already set up from the mongodb sample.

Using `findOneAndUpdate`, the response is the actual updated document. Play around with the configuration and change `{ new: true }` to **`{ new: false }`** and see what the difference is in the result.

```JavaScript
app.post('/updateStudent', function(req, res) {
  var query = {
    name: req.body.name
  };

  var update = {
    $set: { id: '109' }
  };

  studentModel.findOneAndUpdate(query, update, { new: true }, function(err, user) {
    if (err) throw err;
    console.log(user);
    res.send(user);
  });
});
```

#### TRY THIS!
Replace the `studentModel.findOneAndUpdate(...)` code block with the code below. Restart the server and send the Postman request again!
```JavaScript
studentModel.updateOne(query, update, function(err, result) {
  if (err) throw err;
  console.log(result);
  res.send(result);
});
```

What's the result provided? Is it the same as before?
