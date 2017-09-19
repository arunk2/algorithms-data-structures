Databases - Running multi-line scripts from command line
==================================
In a typical application using Database, it is natural all the changes for fixing bugs or new features are sent as SQL scripts. 
In most of the cases we have single line scripts (DDL / DML statements). 

But there are some scenarios we need to run multi-line scripts like creating and running some procedures / functions / triggers.

### Problem
We cannot them directly run them as a command line script as the semicolon (;) available seperating lines in them are considered 
as end of lines and resulting in syntax error for SQL statement.

### Solution
To overcome this we can temporarily change the terminal symbol from semicolon (;) to some thing else and reset it back to semicolon (;) 
later. For example, we can change it to hash (#) symbol and reset back to semicolon (;) with the script below.


      set term #;

      execute block (...)
      as
      begin
        statement1#
        statement2#
      end
      #

      set term ;#
     
     
