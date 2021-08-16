### Source

https://www.codeproject.com/Articles/16374/How-to-Write-a-Terminal-Services-Add-in-in-Pure-C

### Introduction
Sometimes you need to write an extension to Terminal Services (if you have used it). So why don't you write it in your favorite programming language (for me, it's C#)?

### Background
Why am I playing with TS? How it started? Well ...

In our firm, almost everyone (about 120+) work on TS. We have a third party ERP system installed on our servers and there is an export function using Excel automation. Now is the question: how to use this functionality without spending money on two licenses for Excel for every user (that's right, in this case, all users should have license on both the server and the workstation)? The answer is: write an application which can provide the same (or at least what they are using) automation as Excel, and can build Excel files and send them to the client. The first version I wrote is based on exporting source-code from the ERP's producent (good to have friends there), and it was sending files via SMTP to the client, and it was written in ATL/WTL. But I knew the export source-code so I knew which object from Excel they (ERP's producent) were using.

After a few months, I found a way to send files over RDP. The application worked for more than a year. ... and then they changed the export code. After reading a great article about Building COM Servers in .NET, I decided to move this application to .NET. I found a way to get to know what functions/methods and objects they were using (IExpando from .NET and COM's IDispatchEx) and how to implement them. I thought, why not move the whole project to .NET, not just the server side. Well, I tried.

So back to the topic ... this article will not be about how to write Excel-like automation stuff. But how to write server/client side add-ins in C#.

### What Should You Know?
What exactly will this sample application do?

The server side:

- picks up a text file
+ reads it
* compresses it using System.IO.Compression
- sends it over RDP

The client side:

- is ready for open RDP channels
- opens it
- reads data
- decompresses
- saves as text file
- and opens it in the default application for the TXT extension

You'll find it useful when:

- you know how to write such an extension in pure Win32 API
- you want to write this in C#

