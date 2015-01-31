#XO Signin Client Library#

A simple client library, and an example application which uses it.

Simply put, the XO App exposes a services (Called getDataJson), this, simply Returns a json string with the current logged in user, or null if no user is currently logged in.

We've wrapped this up in a library that you *should* be able to simply drop into your application. See the 'example' project's MainActivity, for sample code on how to call the API. I've also included the relevant snippet below
```java
    xoDataProvider = new XoDataProvider(this);
    
    xoDataProvider.requestStudentData(new XoDataProvider.DataCallback() {
      @Override
      public void onDataAvailable(final String data) {
	// Parse JSON and do something
      }
      
      @Override
      public void onError(final String description) {
	// Handle error. Recommended approach is a screen with a big button, asking
        // users to login, which when clicked, launches the XO App.
      }
    });
```

The data returned will be nested in a top-level 'student' or 'teacher' field, depending on the kind of the current user. The schema between the two are slightly different. Here are two examples below:

## Student JSON Example ##

```javascript
{
  "student": {
     "id": "123",                    // Unique across all students
     "name": "Jeeva Suresh",
     "avatar": "http://id.one-education.org/path/to/small/avatar",
     "avatar_large": "http://id.one-education.org/path/to/large/avatar",
     "gender": "male",
     "verified": true,              // Has the student account been verified
     "token": "1903iolajfklasdjf-9" // Token to access any API services
  }
}
```

The following fields *may* be null, and as such missing from the returned JSON
 - avatar
 - avatar_large

## Teacher JSON Example ## 

```javascript
{
  "teacher": {
     "id": "123",             // Unique across all teachers
     "title": "Mr",	 
     "first_name": "Jeeva",
     "last_name": "Suresh",
     "avatar": "http://id.one-education.org/path/to/small/avatar",
     "avatar_large": "http://id.one-education.org/path/to/large/avatar",
     "verified": true,			// Has the teacher account been verified
     "token": "1903iolajfklasdjf-9"	// Token to access any API services
  }
}
```

The following fields *may* be null, and as such missing from the returned JSON
 - avatar
 - avatar_large
