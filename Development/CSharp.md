# C\# / Razor / .Net

- [C# Reference](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/index)  
  This section provides reference material about C# keywords, operators, special characters, preprocessor directives, compiler options, and compiler errors and warnings.

## [Create a nested group](https://docs.microsoft.com/en-us/dotnet/csharp/linq/create-a-nested-group)  
  posted on November 20, 2016

## [Grouping data with LINQ and MVC](https://ole.michelsen.dk/blog/grouping-data-with-linq-and-mvc.html)  
  Article by Ole Michelsen posted on November 20, 2011  
  
  Create a list in a controller:  
  
  ```
  using System.Collections.Generic;
  using System.Linq;
  using System.Web.Mvc;
  using LinqGrouping.Models;
  
  namespace LinqGrouping.Controllers
  {
      public class GroupingController : Controller
      {
          public ActionResult Index()
          {
              var books = new List<Book>();
  
              // Add test data
              books.Add(new Book { Author = "Douglas Adams", Title = "The Hitchhiker's Guide to the Galaxy", Genre = "Fiction", Price = 159.95M });
              books.Add(new Book { Author = "Scott Adams", Title = "The Dilbert Principle", Genre = "Fiction", Price = 23.95M });
              books.Add(new Book { Author = "Douglas Coupland", Title = "Generation X", Genre = "Fiction", Price = 300.00M });
              books.Add(new Book { Author = "Walter Isaacson", Title = "Steve Jobs", Genre = "Biography", Price = 219.25M });
              books.Add(new Book { Author = "Michael Freeman", Title = "The Photographer's Eye", Genre = "Photography", Price = 195.50M });
  
              // Group the books by Genre
              var booksGrouped = from b in books
                                 group b by b.Genre into g
                                 select new Group<string, Book> { Key = g.Key, Values = g };
  
              return View(booksGrouped.ToList());
          }
      }
  }
  ```  
  
  
  The grouping is handled with the LINQ group by statement, and here we choose the Genre field as our key to group by. Now we select our subsets into the Group object, which will consist of a key and a collection of each book which matches this key. The end result is a List<Group<string, Book>>, which makes it easy for us to output as HTML:  
  ```
  @using LinqGrouping.Models
  @model List<Group<string, Book>>
  
  @{
      ViewBag.Title = "LINQ Grouping";
  }
  
  <h2>Grouping books by Genre</h2>
  
  <table>
  <thead><tr><th>Author</th><th>Title</th><th>Price</th></tr></thead>
  <tbody>
  @foreach (var group in Model)
  {
      <tr><th colspan="3">@group.Key</th></tr>
      foreach (var book in group.Values)
      {
          <tr><td>@book.Author</td><td>@book.Title</td><td>@book.Price.ToString("c")</td></tr>
      }
  }
  </tbody>
  </table>
  ```  
  
