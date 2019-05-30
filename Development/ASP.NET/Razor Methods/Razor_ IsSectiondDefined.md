# Razor Methods - IsSectionDefined()  

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
