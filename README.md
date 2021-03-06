# react-smart-data-table
[![npm version](https://badge.fury.io/js/react-smart-data-table.svg)](https://badge.fury.io/js/react-smart-data-table)

A smart data table component for React.js meant to be configuration free

## About

This is meant to be a _zero configuration_ data table component for React.js
in the spirit of _plug and play_.

Just feed it an array of equal JSON objects and it will create a template free
table that can be customized easily with any framework (or custom CSS).

It currently supports:
  1.  Humanized column names based on object keys
  2.  Sortable columns
  3.  Results filtering
  4.  Search term highlight in the results
  5.  Column visibility toggles
  6.  Automatic pagination
  7.  Server-side data

## Installation

```
$ npm install react-smart-data-table
```

## Props

| Name        | Default             | Type                | Description                                            |
| :---------- | :------------------ | :------------------ | :----------------------------------------------------- |
| data        | []                  | {array&#124;string} | An array of plain objects (can be nested) or a URL     |
| dataKey     | 'data'              | {string}            | The object key where the async data is available       |
| name        | reactsmartdatatable | {string}            | The name for the table                                 |
| footer      | false               | {boolean}           | Copy the header to the footer                          |
| sortable    | false               | {boolean}           | Makes the columns of the table sortable                |
| withToggles | false               | {boolean}           | Enables the column visibility toggles                  |
| withLinks   | false               | {boolean}           | Converts e-mails and url addresses to links            |
| withHeaders | true                | {boolean}           | Can be used to disable the rendering of column headers |
| filterValue | ''                  | {string}            | Filters all columns by its value                       |
| perPage     | 0                   | {number}            | Paginates the results with the value as rows per page  |

## Examples

### Async data loading (fetch)

By passing a string to the `data` prop, the component will interpret it as an
URL and try to load the data from that location using _fetch()_. If a successful
request is returned, the data will be extracted from the `data` key in the
response object. If it's in a different key, you can specify it with the
`dataKey` prop.

`response`
``` json
{
  "status": "success",
  "message": "",
  "data": [ { "id": 0, "other": "..." }, { "id": 1, "other": "..." }, "..." ]
}
```

``` javascript
<SmartDataTable
  data='/api/v1/data'
  dataKey='data'
  name='test-table'
/>
```

### Simple sortable table (with Semantic UI)

``` javascript
import React from 'react'
import ReactDOM from 'react-dom'
import faker from 'faker'
import SmartDataTable from 'react-smart-data-table'

var testData = []
var numResults = 100

for (var i=0; i<numResults; i++) {
  testData.push({
    _id: i,
    fullName: faker.name.findName(),
    'email.address': faker.internet.email(),
    phone_number: faker.phone.phoneNumber(),
    address: {
      city: faker.address.city(),
      state: faker.address.state(),
      country: faker.address.country()
    }
  })
}

ReactDOM.render(
  <SmartDataTable
    data={testData}
    name='test-table'
    className='ui compact selectable table'
    sortable
  />,
  document.getElementById('app')
)
```

## Demos

You can try _react-smart-data-table_ with different UI libraries in the demo
pages below. You can experiment with different features as well.

* [Semantic UI: All Features](https://joaocarmo.github.io/react-smart-data-table/examples/semantic-ui/)
* [Bootstrap: Sortable](https://joaocarmo.github.io/react-smart-data-table/examples/bootstrap/)


## Forking / Contributing

If you want to fork or contribute, it's easy to test your changes. Just run the
_test_ compilation command and, if all goes well, run the _start_ command to
start an HTTP server (requires _Python_) in the root folder where you can easily
access the test subfolder from your browser.

```
$ npm run build

$ npm test

$ npm start

http://localhost:3000/test/
```
