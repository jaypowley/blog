@{
    Layout = "blogpost";
    Title = "Hello world...again";
    AddedDate = "2018-12-20T04:44:36";
    Tags = "General";
    Description = "";
}
## Testing blog posts with code

Testing out code posts.

```fsharp
open System
open System.Text.RegularExpressions

let postDate = new DateTime(2018, 11, 29) 
let unformattedName = "Canadian Breakfast Stout (CBS)"
let formattedDate = postDate.ToString "yyyy-MM-dd"
let replaceSpaceWithHyphen (x:string) = x.Replace(" ", "-")
let removeNonHtmlCharacters (x:string) = x.Replace("(", "-").Replace(")","-")
let removeMultipleHyphens (x:string) = Regex.Replace(x, "-+", "-")
let trimHyphen (x:string) = x.Trim('-')
let toLower (x:string) = x.ToLower()
let formatInput (x:string) = replaceSpaceWithHyphen x
                            |> removeNonHtmlCharacters
                            |> removeMultipleHyphens
                            |> trimHyphen
                            |> toLower

let formatPostName (date:string) (text:string) = formatInput (date + "-" + text) + ".jpeg"

formatPostName formattedDate unformattedName
```