---
permalink: ef-plus 
---

## Definition

**Entity Framework Plus** is a library that Improve Entity Framework performance and overcome limitations with **MUST-HAVE** features.

## Features

- Batch Operations
  - [Batch Delete](/batch-delete)
  - [Batch Update](/batch-update)
- LINQ
  - LINQ Dynamic
- Query
  - [Cache](/cache)
  - [Query Deferred](/deferred-query)
  - Query DbSetFilter
  - [Query Filter](/filter)
  - [Query Future](/future)
  - [Query IncludeFilter](/include-filter)
  - [Query IncludeOptimized](/include-optimized)
- Audit
  - [Audit](/audit)

## Batch Operations

Batch Operations method allow to perform **UPDATE** or **DELETE** operation directly in the database using a LINQ Query without loading entities in the context.

Everything is executed on the database side to let you get the best performance available.

{% include template-example.html %} 
{% highlight csharp %}
// using Z.EntityFramework.Plus; // Don't forget to include this.

// DELETE all users which has been inactive for 2 years
ctx.Users.Where(x => x.LastLoginDate < DateTime.Now.AddYears(-2))
         .Delete();

// DELETE using a BatchSize
ctx.Users.Where(x => x.LastLoginDate < DateTime.Now.AddYears(-2))
         .Delete(x => x.BatchSize = 1000);

{% endhighlight %}


### Audit

Allow to easily track changes, exclude/include entity or property and auto save audit entries in the database.

{% include template-example.html %} 
{% highlight csharp %}
// using Z.EntityFramework.Plus; // Don't forget to include this.

var ctx = new EntityContext();
// ... ctx changes ...

var audit = new Audit();
audit.CreatedBy = "ZZZ Projects"; // Optional
ctx.SaveChanges(audit);

// Access to all auditing information
var entries = audit.Entries;
foreach(var entry in entries)
{
    foreach(var property in entry.Properties)
    {
    }
}

{% endhighlight %}

AutoSave audit in your database

{% include template-example.html %} 
{% highlight csharp %}
AuditManager.DefaultConfiguration.AutoSavePreAction = (context, audit) =>
    (context as EntityContext).AuditEntries.AddRange(audit.Entries);

{% endhighlight %}

## Requirements

### Entity Framework Version

 - Entity Framework Core 2.x
 - Entity Framework 6.x
 - Entity Framework 5

[Learn more](http://entityframework-plus.net/)