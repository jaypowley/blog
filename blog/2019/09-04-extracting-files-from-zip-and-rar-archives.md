@{
    Layout = "blogpost";
    Title = "Extracting Files From Zip and Rar Archives";
    AddedDate = "2019-09-04T07:24:26";
    Tags = "F#, Scripts";
    Description = "";
}

## Extracting Files From a Zip Archive With F#

Today I needed to unzip some archives sent to me in different formats. Since I didn't have applications like WinZip, 7Zip, or WinRar installed on my work PC I figured I could whip up a quick extractor using the built in .Net library for PDFs and a third party library for Rar files, in this case I used [SharpCompress (Nuget)](https://www.nuget.org/packages/sharpcompress/).

```fsharp
open System
open System.IO
open System.IO.Compression

#r "System.IO.Compression"
#r "System.IO.Compression.FileSystem"

type Unzipper (?sourceDir : string, ?targetDir : string) =
    let mutable source =
        match sourceDir with
        | Some source1 -> source1
        | None -> Environment.CurrentDirectory
    let mutable target =
        match targetDir with
        | Some source1 -> source1
        | None -> Environment.CurrentDirectory

    let extractAll =
        Directory.EnumerateFiles(source, "*.zip")
        |> Seq.iter (fun zipPath -> printfn "Uncompressing %s" (Path.GetFileName(zipPath))
                                    let archive = ZipFile.Open(zipPath, ZipArchiveMode.Read)
                                    archive.ExtractToDirectory(target + "//" + Path.GetFileNameWithoutExtension(zipPath)))

    do extractAll

Unzipper (sourceDir = "C:/Users/powleyj/Downloads/", targetDir = "C:/Users/powleyj/Downloads/Uncompressed")
```

## Extracting Files From a Rar Archive With F#

```fsharp
#r "C:/Shared Resources/SharpCompress/SharpCompress.0.24.0/lib/net45/SharpCompress.dll"

open System.IO
open SharpCompress.Common;
open SharpCompress.Readers;
open SharpCompress.Readers.Rar;

let sourceFile = "C:/Users/powleyj/Downloads/SuperImportantArchive.rar"
let destDir = "C:/Users/powleyj/Downloads/Uncompressed"

let unpackRar =
    use reader = RarReader.Open(File.OpenRead(sourceFile))
    while reader.MoveToNextEntry() do
        let extractionOptions = ExtractionOptions()
        reader.WriteEntryToDirectory(destDir, extractionOptions)

unpackRar
```
