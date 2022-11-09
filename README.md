# local-library
A project following MDN's express tutorial

## Challenges
### Conditional in the .pug file
In order for bookinstance form page to completely pull all information into the form fields, I wanted to add a way to select an `<option>` tag by default. In this case, I used a conditional like this:
```javascript
option(value='Maintenance' selected=(status === 'Maintenance' ? true : false)) Maintenance
```

This can be found in '/views/bookinstance_form.pug'

### Hiding the MongoDB account
I accidentally pushed my MongoDB account and password to GitHub, which is not good. I think there's a way to hide the account and password by creating a file (I think it's called .env) and placing it in .gitignore but for now I have to remember to remove the account and password details on my app.js file for now.

### Converting to the right date format for form fields
[According to the MDN guide](https://developer.mozilla.org/en-US/docs/Learn/Server-side/Express_Nodejs/forms), the Author and Book Instance date fields are in the wrong format for the form. I had to convert the date from the database to "YYYY-MM-DD". To resolve this, I imported Luxon to my controller with:

```javascript
const { DateTime } = require('luxon');
```

Then, when I render the date variable to the .pug file, I use one of Luxon's built-in commands to convert it to the right format:

```javascript
res.render("bookinstance_form", {
  title: "Create Book Instance",
  book_list: [ bookinstance.book ],
  imprint: bookinstance.imprint,
  due_back: DateTime.fromJSDate(bookinstance.due_back).toISODate(),
  status: bookinstance.status
})
```