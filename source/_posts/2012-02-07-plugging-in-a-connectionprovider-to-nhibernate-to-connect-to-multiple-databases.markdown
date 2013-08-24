---
author: David Hogue
comments: true
date: 2012-02-07 14:53:04+00:00
layout: post
slug: plugging-in-a-connectionprovider-to-nhibernate-to-connect-to-multiple-databases
title: Plugging a ConnectionProvider in to NHibernate to connect to multiple databases
wordpress_id: 901
categories:
- Software Development
tags:
- nhibernate
---

I recently had a scenario where I needed to connect to a variety of databases depending on context. The databases all shared the same schema, the contents were just partitioned out based on customer.

I’d originally done this with many SessionFactories ([like this post does](http://codebetter.com/karlseguin/2009/03/30/using-nhibernate-with-multiple-databases/).)

After a while I ran into memory usage issues (See [this post about debugging with WinDbg](https://davidhogue.com/blog/2011/12/some-windbg-notes-for-troubleshooting-excessive-memory-usage/).)

So that’s when I started looking for another option. What I wanted to do was use one factory and supply it with connections to the right databases.

### The Provider




    
    
    /// <summary>
    /// Connection provider that will override the default connection string and use one that's
    /// been specified for this thread.
    /// </summary>
    public class DbSpecificConnectionProvider : DriverConnectionProvider
    {
        /// <summary>
        /// Returns a new connection using the connection string set in ThreadConnectionString.
        /// </summary>
        public override IDbConnection GetConnection()
        {
            var connection = Driver.CreateConnection();
            try
            {
                connection.ConnectionString = GetConnectionStringFromContext();
                connection.Open();
            }
            catch (DbException)
            {
                connection.Dispose();
                throw;
            }
            return connection;
        }
    }
    




This isn’t too complex really. It inherits from the default provider of DriverConnectionProvider and overrides the GetConnection function. It then gets a connection from the driver, sets the connection string and opens the connection. If there are any errors it’ll cleanup the connection before exiting.




### Additional bits




You’ll also need to edit your configuration to tell it about the new provider:



    
                                        
    <property name="connection.provider">
      My.Namespace.DbSpecificConnectionProvider, MyAssembly
    </property>
    




And if you are using second level caching, you might need to implement a caching provider so that the cache doesn’t get cross-contaminated.

Now this hasn’t had that much testing yet, so I’m still being a little cautious with it. But if it works, it’s a nice clean solution to my specific problem.
