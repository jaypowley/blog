@{
    Layout = "blogpost";
    Title = "Concatenating PDFs With F#";
    AddedDate = "2019-08-21T08:39:06";
    Tags = "F#, Scripts";
    Description = "";
}

## Concatenating PDFs with F#

At work today I needed to combine some pdfs together. Since I didn't have a license to Adobe Acrobat, nor MacOS (which has this functionality built in natively), I needed a quick solution using a third party library, in this case I used [PdfSharp](http://www.pdfsharp.net/). I also figured a quick F# script would do the trick. So below is what I whipped up in about 20 minutes to get the job done and have a reuseable solution in the future if the need arises.

```fsharp
#r "C:/Shared Resources/PdfSharp/PDFsharp.1.50.5147/lib/net20/PdfSharp.dll"

open System.IO
open PdfSharp.Pdf
open PdfSharp.Pdf.IO

let sourceDir = "C:/Users/Jason/Documents" // Or wherever your PDFs are
let targetFileName = Path.Combine(sourceDir, "Result.pdf") // Or whatever you want your output called
let pdfFiles = Directory.GetFiles(sourceDir, "*.pdf") |> Array.toList

// Gets all of the pages for a PDF document
let getPages (sourceFileName : string) =
    use source = PdfReader.Open(sourceFileName, PdfDocumentOpenMode.Import)
    [
      for i = 0 to source.PageCount - 1 do
        yield source.Pages.[i]
    ]

// Gets all of the pages for all of the PDFs
let getAllPages =
    List.collect getPages pdfFiles

// Adds all the pages to one document
let createDocFromPages pages =
    let targetDoc = new PdfDocument()  
    pages |> List.iter (targetDoc.Pages.Add >> ignore)
    targetDoc

// Creates the document and writes output to disk
let concatDocs =  
    let doc = createDocFromPages getAllPages
    doc.Save targetFileName
    doc.Dispose()

// Kicks it all off
concatDocs
```
