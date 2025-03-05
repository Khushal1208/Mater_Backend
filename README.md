# Mater_Backend


# Backend Cheat Codes (Express.js, EJS, File Handling)

## 🚀 Basic Server Setup
```js
const express = require("express");
const app = express();
const path = require("path");

app.use(express.urlencoded({ extended: true }));
app.use(express.json());

app.set("view engine", "ejs");
app.use(express.static(path.join(__dirname, "public")));

app.listen(3000, () => console.log("Server running on port 3000"));
```
📌 **Note:** This setup is used in **90% projects**. Only routes and logic change.

---

## 🌐 Dynamic Routing (Params & Query)
```js
app.get("/user/:id", (req, res) => {
  res.send(`User ID: ${req.params.id}`);
});
```
🔹 **Params:** `req.params.<name>`  
🔹 **Query Params:** `req.query.<name>`

Example: `/user/123?name=khushal`
```js
app.get("/user/:id", (req, res) => {
  res.send(`User ID: ${req.params.id}, Name: ${req.query.name}`);
});
```

---

## 📩 Handling Forms & Data (POST Requests)
```js
app.post("/submit", (req, res) => {
  console.log(req.body); // Form data
  res.send("Form Submitted");
});
```
📌 **Tip:** Form data is accessed using `req.body`.

---

## 📂 File Handling (fs module)
```js
const fs = require("fs");

// Create File
fs.writeFileSync("data.txt", "Hello, World!");

// Read File
const data = fs.readFileSync("data.txt", "utf-8");
console.log(data);

// Rename File
fs.renameSync("data.txt", "newdata.txt");

// Delete File
fs.unlinkSync("newdata.txt");
```
📌 **Note:**  
- `writeFileSync()` → **Creates a file**  
- `readFileSync()` → **Reads file data**  
- `renameSync()` → **Renames a file**  
- `unlinkSync()` → **Deletes a file**  

---

## 🛠 Middleware (req, res, next)
```js
const logger = (req, res, next) => {
  console.log(`${req.method} ${req.url}`);
  next();
};

app.use(logger);
```
📌 **Tip:** Middleware is used to **modify requests or log data** before reaching the route.

---

## 🎨 Serving Static Files (CSS, JS, Images)
```js
app.use(express.static(path.join(__dirname, "public")));
```
📌 **Tip:** Files inside **public/** can be accessed directly without defining routes.

---

## 🖥 Rendering EJS Files
```js
app.get("/", (req, res) => {
  res.render("index", { name: "Khushal" });
});
```
📌 **Tip:**
- `res.render("filename", {dataObject})` sends data to **EJS template**.
- `<%= name %>` inside EJS file prints data.

---

## 🔀 Redirects & 404 Pages
```js
app.get("/google", (req, res) => {
  res.redirect("https://www.google.com");
});

app.use((req, res) => {
  res.status(404).send("Page Not Found");
});
```
📌 **Tip:**
- `res.redirect(URL)` → Redirects user to another page.
- `res.status(404).send("Page Not Found")` → Handles **404 errors**.

---

## ⚡ Pro Tips to Write Backend Code Faster
1. **Create your own templates** (Save a `serverTemplate.js` file for quick use).
2. **Use Boilerplate Code snippets** (Save commonly used code in VS Code snippets).
3. **Organize routes** (Use separate files like `routes/user.js`, `routes/auth.js`).
4. **Use Postman for testing APIs**.
5. **Always log `req.body`, `req.params`, `req.query`** for debugging. 🚀

🎯 **Practice these 10-15 times** and you’ll be writing backend code at lightning speed! 🔥



<footer>------------------------------------------------------------</footer>


#usermodel.js
```
const mongoose = require('mongoose')

const mongoPort = "127.0.0.1:27017"
const dbName = "mongopractice"

mongoose.connect(`mongodb://${mongoPort}/${dbName}`)

const userSchema = mongoose.Schema({
    name: String,
    username : String,
    email: String
})

module.exports = mongoose.model("user",userSchema)
```


<footer>--------------------------------</footer>
.
# app.js

````
const express = require("express");
const userModel = require("./usermodel");

const app = express();

app.get("/", (req, res) => {
  res.send("hey");
});

app.get("/create", async (req, res) => {
  let createduser = await userModel.create({
    name: "Mahak Garg",
    username: "Mahakssss",
    email: "khushal@gmail.com",
  });
  res.send(createduser);
});

app.get("/update", async (req, res) => {
  let updateduser = await userModel.findOneAndUpdate(
    { name: "khushal" },
    { username: "khushal" },
    { new: true }
  );
  res.send(updateduser);
});

app.get("/read", async (req, res) => {
  let users = await userModel.find()  //READS ALL USERS
//   let users = await userModel.find({ username: "Mahakssss" }); // it gives in array form
  // findOne({username:'Mahakssss'}) gives you in object form
  res.send(users);
});

app.get('/delete',async(req,res)=>{
    let user = await userModel.findOneAndDelete({username:'Mahakssss'})
    res.send(user)
})

app.listen(3000);
````




### **Learnings from MongoDB, Mongoose, and Database Management**

#### **1. Setting Up MongoDB Connection**
- Used **Mongoose** to connect with MongoDB:  
  ```js
  mongoose.connect(`mongodb://${mongoPort}/${dbName}`)
  ```
- `mongoPort` is `127.0.0.1:27017`, meaning the database is running locally.
- `dbName` is `"mongopractice"`, which is the name of the database.

#### **2. Defining a Schema and Model**
- Created a **Schema** (`userSchema`) to define the structure of user documents.
- Used `mongoose.model("user", userSchema)` to create a model named `"user"` that maps to a MongoDB collection.

#### **3. CRUD Operations Using Mongoose**
- **Create (`.create()`)**  
  - Inserted a new user document into MongoDB.
  - Example:
    ```js
    let createduser = await userModel.create({
        name: "Mahak Garg",
        username: "Mahakssss",
        email: "khushal@gmail.com",
    });
    ```
- **Read (`.find()`, `.findOne()`)**  
  - Retrieved all users using `.find()`.
  - Retrieved a specific user using `.findOne({ username: "Mahakssss" })`.

- **Update (`.findOneAndUpdate()`)**  
  - Updated a document where `name: "khushal"` and changed its `username` to `"khushal"`.
  - `{ new: true }` ensures the updated document is returned.

- **Delete (`.findOneAndDelete()`)**  
  - Deleted a user document where `username: "Mahakssss"`.

#### **4. Express.js Integration**
- Used Express.js to handle different routes (`/create`, `/read`, `/update`, `/delete`).
- Each route interacts with the MongoDB database through Mongoose.

#### **5. MongoDB Database Management**
- **Database is automatically created** when inserting the first document.
- **Collections are dynamically created** when the first document is added.
- **MongoDB is schema-less**, but Mongoose enforces schema validation.

#### **6. Understanding Async/Await**
- Used `async/await` for database operations to handle asynchronous behavior properly.
- Example:
  ```js
  let users = await userModel.find();
  res.send(users);
  ```

#### **7. Running the Server**
- Used `app.listen(3000);` to start the Express.js server on port `3000`.

---

These are the core learnings from working with **MongoDB**, **Mongoose**, and **Database Management** in this project. 🚀
