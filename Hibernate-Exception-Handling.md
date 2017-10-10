## Hibernate Exception Handling - SQL Errors

Some people often forget to pay attention (like me) to trivial things, while building application on some ORM frameworks. 
In my case I used hibernate ORM and the exception handling part never gave appropriate SQL error messages and SQL error codes.

Later realized that it is the generic Exception catch block could not retrive detailed information with e.getMessage() method. 
Then did some googling and found some useful references, but none served my purpose. 
So thought of making a post for this exclusively.


The following skeleton structure is self explianatory

```
try {


  //Hibernate operations


}
catch (HibernateException e) {

 if (e.getCause() != null && e.getCause() instanceof SQLException) {             

  //we have a SQL Exception - get detailed sql exception with error code
  SQLException sqlException = (SQLException) e.getCause();
  String message = sqlException.getErrorCode() + sqlException.getMessage();
  throw new customException(message);

 }
 else {

  //Don't ignore other hibernate exceptions
  throw e;

 }

}
```
