> The function listens for req.on(‘data’) and constructs req.body from the chunks of data it gets.
There are a bunch of different ways to format the data you POST to the server:
application/x-www-form-urlencoded
multipart/form-data
application/json
application/xml
maybe some others
```
app.use(bodyParser.json()); // for parsing application/json
app.use(bodyParser.urlencoded({ extended: true })); // for parsing application/x-www-form-urlencoded
app.use(multer()); // for parsing multipart/form-data
```
qs allows you to create nested objects within your query strings, by surrounding the name of sub-keys with square brackets []. For example, the string 'foo[bar]=baz'