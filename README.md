# HSharp
HSharp is a library used to analyse markup language like HTML easily and fastly. 

## Only Two Functions
* Deserialize and analyse Html
* Build HTML using C#

## How to install
#### Using Nuget
To install Aiursoft.HSharp, run the following command in the [Package Manager Console](https://docs.nuget.org/docs/start-here/using-the-package-manager-console)  
````bash
PM> Install-Package Aiursoft.HSharp
````
#### Download the dll
You can only download the dll from [https://aiursoft.com.cn](https://www.aiursoft.com.cn/) and add it to your project.
## Examples
### Deserialize HTML
Input some HTML and get the DOM of it.  
````csharp
var NewDocument = HtmlConvert.DeserializeHtml($@"
    <html>
        <head>
            <meta charset={"\"utf-8\""}>
            <meta name={"\"viewport\""}>
            <title>Example</title>
        </head>
    <body>
        <h1>Some Text</h1>
        <table>
            <tr>OneLine</tr>
            <tr>TwoLine</tr>
            <tr>ThreeLine</tr>
        </table>
    </body>
    </html>");

    Console.WriteLine(NewDocument["html"]["head"]["meta",0].Properties["charset"]);
    Console.WriteLine(NewDocument["html"]["head"]["meta",1].Properties["name"]);
    foreach (var Line in NewDocument["html"]["body"]["table"])
    {
        Console.WriteLine(Line.Son);
    }
````
Output:  
````html
    utf-8
    viewport
    OneLine
    TwoLine
    ThreeLine
````
### Build HTML
Create a simple HDoc and add some children to its body.  
````CSharp
var Document = new HDoc(DocumentOptions.BasicHTML);
Document["html"]["body"].AddChild("div");
Document["html"]["body"]["div"].AddChild("a", new HProp("href", "/#"));
var Result = Document.GenerateHTML();
````
Output:
````html
    <html>
    <head>
        <meta charset="utf-8"></meta>
        <title>
            Example
        </title>
    </head>
    <body>
        <div>
            <a href="/#"></a>
        </div>
    </body>
    </html>
````
**HSharp can also operate other Markup language like XML and XAML**