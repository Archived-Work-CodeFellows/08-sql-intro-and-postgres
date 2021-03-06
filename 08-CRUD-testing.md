## Lab 8 - Testing CRUD operations in the console

### Steps to test Create, Read, Update and Delete operations once server.js is complete.
---
### Create a record (POST)

Go into the **psql** shell and enter `SELECT COUNT(*) from articles;` to view the current number of records in the table. Then, in the browser console:

```
let newArticle = new Article({
  title:'Flibbity goes Jibbiting',
  author:'Flibbity Jibbit',
  authorUrl:'flibbity.jibbit.com',
  category:'jibbits',
  publishedOn:'01-01-2217',
  body:'Flibbity Jibbit and the Key Keeper'
});
```

`newArticle.insertRecord();`

You can now go into the **psql** shell and see that the `SELECT COUNT(*) from articles;` value has increased by 1.

The new article should appear in the blog on page refresh.

---

### Destroy a record (DELETE)

Go into the **psql** shell and enter `SELECT COUNT(*) from articles;` to view the current number of records in the table.

Inspect the Flibbity Jibbit article we created by entering `Article.all[0]` in the console. We can delete it by entering:

`Article.all[0].deleteRecord()`

After calling this method, the article will still be in the browser memory although it has been deleted from the database. You can verify this by entering `Article.all[0]` in the console, and see that the article is still there... but... go into the **psql** shell and enter `SELECT COUNT(*) from articles;` to see that the number of records has decreased by one!

On page refresh, the Flibbity Jibbit article will no longer appear in the browser.

---

### Destroy all records (DELETE)

You might want to save this for last.

`Article.truncateTable()`

Refresh the page: *NO MORE ARTICLES*.

Go into the **psql** shell and enter `SELECT COUNT(*) from articles;` to see that there are now *ZERO* articles in the DB.

After you do this, you'll need to restart the server to reload the DB. But then put the Flibbity article back in like you did above, and inspect it in the console with `Article.all[0]`, and take a look at the `article_id`! Whoa! The number is different!

If you want, you can `DROP TABLE articles` to reset the numbering of the records in the DB.
