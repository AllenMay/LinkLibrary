# Razor template markup syntax  

- [ASP.NET Razor](https://en.wikipedia.org/wiki/ASP.NET_Razor) - Wikipedia

## Razor syntax: three basic rules  
(Jess Chadwick, ASP.NET MVC 4 Essential Training [Lynda.com](https://www.lynda.com))
 - just write code and markup - don't think about it  
 - @ indicates code  
 - standard language keywords  
 
## IsSectiondDefined() 
You can use this method to inspect whether a section has been defined in the referring view and act accordingly.

**_Layout.cshtml**
~~~
@Scripts.Render("~/bundles/jquery")
@* @RenderSection("scripts", required: false) *@
@if (IsSectionDefined("scripts"))
{
  @RenderSection("scripts")
}
@
~~~

## Razor "keywords"
 - Code  
   - @  
   - @()  
   - @{}  
 - Content  
   - @:  
   - <text> </text>  - Indicates multiple lines of content
 - Comments  
   - @*  *@  
