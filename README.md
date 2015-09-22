# Node JS client library for IDOL OnDemand
Basic library to help with calling IDOL OnDemand APIs [http://idolondemand.com](http://idolondemand.com).

## What is IDOL OnDemand?
IDOL OnDemand is a set of over 70 APIs for handling all sorts of unstructured data. Here are just some of our APIs' capabilities:
* Speech to text
* OCR
* Text extraction
* Indexing documents
* Smart search
* Language identification
* Concept extraction
* Sentiment analysis
* Web crawlers
* Machine learning

For a full list of all the APIs and to try them out, check out https://www.idolondemand.com/developer/apis

### Installation
To install, run the following command:
```
npm install iod-node
```
If you want to install the latest module directly from Github, use the following command:
```
npm install git+https://github.com/HP-IDOL-OnDemand/iod-node
```

### Include it

```js
var iod = require('iod-node')
client = new iod.IODClient('http://api.idolondemand.com','apikey')
```

### Callbacks

```js
var callback = function(err,resp,body){
  console.log(body)
}
```

We can define our callbacks as functions and pass them as arguments

```js
var data = {'text' : 'I like cats'}
client.call('analyzesentiment', callback, data)
```
Or, we can use the .on('data') hook to do the same thing.

```js
client.call('analyzesentiment',data).on('data',callback)
```

The order of the arguments after the API name don't matter when passed, so all of these are the equivalent.

```js
//1
client.call('analyzesentiment', data, callback)
//2
client.call(data, 'analyzesentiment', callback)
//3
client.call(data, callback, 'analyzesentiment')
```


### Async calls

While node will mostly deal with things asynchronously, IDOL OnDemand offers server side asynchronous call method which should be used with large files and slow queries. Pass a boolean for the async parameter.

```js
client.call('analyzesentiment', data, callback, true)
```

### Posting files

File posting is handled using the "file" parameter name which is used for all current file postings in IDOL OnDemand

```js
var data = {'file' : 'test.txt'}
client.call('analyzesentiment', data, callback)
```
