@{
    Layout = "blogpost";
    Title = "I Need Devops";
    AddedDate = "2019-03-20T08:30:57";
    Tags = "Devops";
    Description = "";
}

## I Need Devops (Part 1 of 3)

Clearly, my blog is all about the [beer](/beer) at this point. The site has been up for six odd months and I have accumulated one test code post and a billion beer posts so far. 😂

Very recently, the nuances of formulating a beer post had reached its tipping point and I could nearly finish a beer in the time it took to get a weeks’ worth of posts created, formatted, and uploaded (and I drink slowly). That is too long for me. So I started to focus on my devops, first by jotting down the dozen or so steps I take to create a single post. Second, by [bypassing the generation of posts one by one through the blogging engine](/blog/2019/03-22-i-need-devops-part-2). And third, by creating a [webscraper to get the data for me](/blog/2019/03-22-i-need-devops-part-3).

"DevOps" is an industry term that involves developers and operations managers to work together and create or employ tools to support the entire service lifecycle of a product, from design through the development process to production support. In other words, to write code for the back office operations, not just for the product or service. In my case, specifically, devops is just me writing code to make this blogging situation go faster.

## The Initial Thirteen

1. Download image(s) from onedrive
2. Rename with format to YYYY-MM-DD-beer-name.jpeg
3. Resize in Paint.net or script out (to do)
4. Open cmd prompt

    4a.
    ```
    cd "C:\Path\To\Source\Of\GitHub\FsBlog\Code"
    ```
    4b.
    ```
    fake new beer="Beer Name"
    ```
5. New beerpost created in C:\Path\To\Source\Of\BlogSource\beer\YYYY
6. Edit in VS Code

    6a. Add Tag(s)

    6b. Add content
7. cmd > fake generate
8. Open C:\Path\To\Source\Of\GitHub\FsBlog\Output

    8a. Delete layouts folder

    8b. Check assets/img, copy any missing images
9. Open another cmd prompt

    9a. run
    ```
    "C:\Program Files\IIS Express\iisexpress.exe" /path:"C:\Path\To\Source\Of\GitHub\FsBlog\Output"
    ```
10. Test posts and tags
11. Copy source to hosted site via FTP
12. Test live site - https://jasonpowley.com
13. Push updates to Github

To me, thirteen steps are way too many for a simple post of beer name, brewery name, picture of said beer, style of said beer, and a small write up about said beer from some authoritative source like the brewery or Untappd. I can honestly say right here and now, that I did not expect to go through thirteen steps in order to publish a beer post, or any type of post for that matter. I would not have started a blog, beer centric or otherwise, if I knew from the start that it would become that tedious. It shouldn't ever have been. But I was excited to finally have something up and "easily" updateable.

## The Initial Plan

Originally I started with the idea that I wanted to blog about all of the aspect of a "veteran .Net developer". Why? Because I read numerous blogs daily and feel that after 15 years as a developer I should be able to contribute back in a meaningful way. And if I couldn't keep to a tech/code centric blog, then at least I could supplement the tech posts with beer posts to keep me honest and active with the blog. Well, as anyone can see that ended up being all the beer and none of the code as initially intended. My bad. ¯\_(ツ)_/¯

Now I may eventually get back to that original idea, but with so much "legacy" experience in WebForms and VB.net, what would I actually be adding to the community that would be valuable? There is literally a dozen or more StackOverflow posts about anything I could ever possibly hope to cover. So I've shifted my focus to be more retroactive, of sorts. I've been (beer) blogging for a while now, so I'll soon recap the evolution of my devops in that respect. Covering my learning curve and continual use of F# that I am determined to use daily whether at work or for personal development (more on that later) in order to keep it fresh in my  mind and readily available in my toolbox (vs XAML knowledge, for example, which has evaporated from my brain stores from lack of use).

From there, I hope to cover a wide breadth of technologies since over the course of my career I've pretty much done it all in terms of .Net development. There's not much left in the "stack" that I haven't done. Not to say I'm an expert at any given one, but I've definitely stuggled and overcome many obstacles in VB.Net, C#, F#, Webforms, MVC 1-5, ADO.Net, Entity Framework, WCF, RIA Services, Silverlight (RIP), Winforms, the AJAX Control Toolkit, Typescript, SignalR, as well as the server technologies (IIS and SQL Server). Did I miss anything? Probably. There's also tech that I have zero experience in that I want to learn and cover as well, like Electon, Xamarin, .Net Core, and all the hip new js libraries that are all the rage lately.

I've gotten a little off track, but part two of this devops series will cover the desired intent and original concept of this blog. Stay tuned.
