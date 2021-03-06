# NPM Package For JIRA (Service Desk) REST API

<!-- [![Build Status](https://travis-ci.org/Chetan07j/build-jira.svg?branch=master)](https://travis-ci.org/Chetan07j/build-jira) -->
[![HitCount](http://hits.dwyl.io/chetan07j/build-jira.svg)](http://hits.dwyl.io/chetan07j/build-jira)
[![Generic badge](https://img.shields.io/badge/code%20style-standard-brightgreen.svg)](https://standardjs.com)
[![GitHub license](https://img.shields.io/github/license/chetan07j/build-jira.svg)](https://github.com/Chetan07j/build-jira/blob/master/LICENSE)
[![GitHub contributors](https://img.shields.io/github/contributors/chetan07j/build-jira.svg)](https://github.com/Chetan07j/build-jira/graphs/contributors/)
[![GitHub issues](https://img.shields.io/github/issues/chetan07j/build-jira.svg)](https://github.com/Chetan07j/build-jira/issues/)
[![GitHub issues-closed](https://img.shields.io/github/issues-closed/chetan07j/build-jira.svg)](https://github.com/Chetan07j/build-jira/issues?q=is%3Aissue+is%3Aclosed)

[![NPM](https://nodei.co/npm/build-jira.png?downloads=true&downloadRank=true&stars=true)](https://nodei.co/npm/build-jira/)

A node.js module, which provides an object oriented wrapper for the JIRA REST API.

This library is built to support version `3.9.1` of the JIRA Service Desk API.

JIRA Service Desk API documentation can be found [here](https://docs.atlassian.com/jira-servicedesk/REST/3.9.1/)

[Service Desk Public REST API](https://developer.atlassian.com/cloud/jira/service-desk/rest/)

<!-- This package is written using [Javascript Standard Style](https://standardjs.com/rules.html) -->

## Installation

Install with the node package manager [npm](http://npmjs.org):

```shell
$ npm install build-jira
```

## How To Use?

### Create the JIRA client

```javascript
const JiraApi = require('build-jira').jira;

const jira = new JiraApi({
  host: <your-jira-host>,
  username: <jira-user>,
  password: <jira-user-password>
});
```

### Get Service Desk Information

```javascript
/* For servicedeskInfo input is not required, hence first parameter is null in this call. */

jira.serviceDeskInfo(null, (error, body) => {
  console.log('RESPONSE: ', error, body);
});
```

### Get All Service Desks

```javascript
/* If start and limit is not passed, then default values 0 and 10 will get applied respectively */

jira.getAllServiceDesks({ start: 0, limit: 10 }, (error, body) => {
  console.log('RESPONSE: ', error, body);
});
```

### Get Service Desk By Id

```javascript
jira.getServiceDeskById(<service-desk-id>, (error, body) => {
  console.log('RESPONSE: ', error, body);
});
```

### Create New Ticket In Service Desk

```javascript
let input = {
  serviceDeskId: <service-desk-id>,
  requestTypeId: <request-queue-id>,
  summary: <your-ticket-title>,
  description: <explanation-about-ticket>
};

jira.createServiceDeskTicket(input, (error, body) => {
  console.log('RESPONSE:', error, body);
});
```

### Get Customer Requests(Tickets)

```javascript
/* If start and limit is not passed, then default values 0 and 10 will get applied respectively */

/*
  NOTE: HERE input IS NOT MANDATORY
  IF YOU PASS IT THEN IT WILL RETURN DATA ACCORDINGLY
  ELSE IT WILL RETURN DEFAULT DATA
*/

let input = {
  start: <start-index>,
  limit: <number-of-records-to-return>,
  requestOwnership: <ticket-ownership-type>,
  requestStatus: <request-ticket-status>,
  searchString: <string-to-get-matching-records>,
  serviceDeskId: <servicedeskid-to-get-records>
};

jira.getAllRequestsOfCustomer(input, (error, body) => {
  console.log('RESPONSE:', error, body);
});
```

### Get Customer Request By Id

```javascript
jira.getCustomerRequestById(<issue-id-key>, (error, body) => {
  console.log('RESPONSE: ', error, body);
});
```

### Create Attachment For Issue/Ticket/Request In Service Desk

```javascript

let input = {
  serviceDeskId: <service-desk-id>,
  issueId: <issue-id-to-add-attachment>,
  file: [<array-of-file-paths-to-attach>],
  comment: <comment-to-add-for-attachment-if-any>
};

jira.createCustomerAttachment(input, (error, body) => {
  console.log('RESPONSE:', error, body);
});
```

### Add Comment On Customer Issue/Ticket/Request In Service Desk

```javascript

let input = {
  issueId: <issue-id-to-add-attachment>,
  comment: <comment-to-add>
};

jira.addCommentOnCustomerRequest(input, (error, body) => {
  console.log('RESPONSE:', error, body);
});
```

### Get All Comments On Customer Issue/Ticket/Request In Service Desk

```javascript
/* If start and limit is not passed, then default values 0 and 10 will get applied respectively */

let input = {
  start: <start-index>,
  limit: <number-of-records-to-return>,
  issueId: <issue-id-to-add-attachment>
};

jira.getCommentsOnCustomerRequest(input, (error, body) => {
  console.log('RESPONSE:', error, body);
});
```

### Get Customer Issue/Ticket/Request Status

```javascript
/* If start and limit is not passed, then default values 0 and 10 will get applied respectively */

let input = {
  start: <start-index>,
  limit: <number-of-records-to-return>,
  issueId: <issue-id-to-add-attachment>
};

jira.getCustomerRequestStatus(input, (error, body) => {
  console.log('RESPONSE:', error, body);
});
```

## Options

jiraApi options: <!-- * `protocol<string>`: Typically 'http:' or 'https:' -->

- `host<string>`: The hostname for your jira server
- `user<string>`: The username to log in with
- `password<string>`: Keep it secret, keep it safe

## Implemented APIs

- Service Desk

  - Infomation
  - Get All Service Desks
  - Get Service Desk By Id
  - Create New Ticket In Service Desk
  - Get All Requests Of Customer
  - Get Customer Request By Id
  - Create Attachment To Customer Request
  - Add Comment on Customer Request
  - Get All Comments On Customer Request
  - Get Customer Request Status (Current And History)

## Changelog


- _1.0.8 addCommentOnCustomerRequest, getCommentsOnCustomerRequest, getCustomerRequestStatus functions added, and other changes_
- _1.0.6 createCustomerAttachment function added_
- _1.0.5 getAllRequestsOfCustomer, getCustomerRequestById functions added and Javascript Standard Style Guid applied_
- _1.0.4 README updated_
- _1.0.3 createServiceDeskTicket function added_
- _1.0.2 serviceDeskInfo parameter corrected_
- _1.0.1 READEME file added_
- _1.0.0 Initial version_
