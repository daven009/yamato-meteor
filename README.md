## Let the party begin @19/06/2014

- version 0.0.0

## 功能汇总 （Draft）
1.  租房(，搬家，家具买卖，家政)
2.  注册，登陆
3.  多样性搜索条(房间，价格，地域，类型)
4.  反向推送
5.  询问提示(邮件，短信)
6.  用户体验设计

===========================================================
Common files:
- `collections/validateionMessage.js` 
  - stores all error messages (non-chinese error message is currently not used in UI).
  - new error messages should be added to this file **ONLY**.
- `config/formOpts.js`
  - stores all the form options for `<selection>`, can be used in both 'Search' and 'Add property'to guarantee consistancy.
  - `Config` is a global variable defined here, use the defined 'get' functions to get options.
- `config/reactiveDS.js` (may consider another folder other than 'config')
  - `ReactiveDS` is a Session-like object. Example: 
  - <pre>
    ReactiveDS.set('mrtline', Config.getStationsByLine(mrtLine));
    ReactiveDS.get('mrtline');
    </pre>
- `helpers/handlebarHelpers.js`
  - handlerbar syntax extension, e.g `{{#arrayify}}`, for iterate a Object's properties. (Lastest Handlerbar.js support `@key`, but not in Meteor.js yet)

Reminder:
- `collections/images_col.js` is not using SimpleSchema because of CollectionFS

- Form error message placement is tightly coupled with `<div class="form-control">` using `id` attribute, and is mapped at the client-side JS file by `var formErrDivID` object. This is because SimpleSchema validation failure will return attribute name of the field with error, so that's the only clue to refer back to where the error occurs. So **Any changes to the div id in `<template name="addProperty">` requires updates on `var formErrDivID` too**

- Every new collection added should has a `subscribe` call in `client/subscriptions.js` and `publish` call in `server/publications.js`. 
  - Also remember to set permissions for the collection like below:
  <pre>
Images.allow({
  insert: function(userId) {
    return true;
  },
  update: function(userId) {
    return !!userId;
  },
  update: function(userId) {
    return !!userId;
  },
  remove: function(userId) {
    return !!userId;
  }
});
  </pre>
  - Actions like `insert`, `update`, `edit` will need Meteor.call() because these actions involving DB modification, thus can only be done on server-side

