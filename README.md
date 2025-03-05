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


