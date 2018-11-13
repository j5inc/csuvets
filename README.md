# Project 7 - WordPress Pentesting

Time spent: Approximately 4 hours.

> Objective: Find, analyze, recreate, and document **five vulnerabilities** affecting an old version of WordPress

## Pentesting Report

1. Large File Upload Error XSS
  - [X] Summary: 
    - Vulnerability types: XSS
    - Tested in version: 4.2
    - Fixed in version: 4.2.15
  - [X] GIF Walkthrough:  ![](Attack1.gif)
  - [X] Steps to recreate: 
     -We need to create a file that is 20 MB or larger. The file name should have the payload script embedded in it.      Example file ~26MB: uploadme<img src=x onerror=alert(1)>.png  
     -The next goal would be to trick an admin of the site to upload the file into the site.  
     -Since the file is larger than 20MB, WordPress reads the file name and executes the script that is embedded.  
     -Report found in WPScan: https://hackerone.com/reports/203515  
  - [X] Affected source code:
    [Link 1] (https://core.trac.wordpress.org/browser/trunk/src/wp-includes/script-loader.php)

2. Unauthenticated Stored Cross-Site Scripting  
  - [X] Summary: 
    - Vulnerability types: XSS
    - Tested in version: 4.2
    - Fixed in version: 4.2.1
  - [X] GIF Walkthrough:  ![](Attack2.gif) 
  - [X] Steps to recreate:    
        -Post a comment wtih HTML tags and some type of script. It is important to note that the comment must be                     larger than 64KB.  
       -Example snippit:  
        HTML
        <a title='xxx onmouseover=alert(unescape(/this%20is%20bad/.source))             style=position:absolute;left:0;top:0;width:5000px;height:5000px  XXXXXXXX...(50k X's to ensure 64KB...XXXXX'></a>
      
  - [ ] Affected source code:
    I could not find affected source code, but there is amplifying information found at:  
    [Link 1] (https://packetstormsecurity.com/files/131644/)
    
3. WordPress User Enumeration
  - [ ] Summary: 
    - Vulnerability types: User Enumeration
    - Tested in version: 4.2
    - Fixed in version: It is unclear to me when this type of enumeration was patched. One way to fix this in all versions is to apply a plugin. 
  - [ ] GIF Walkthrough: 
  - [ ] Steps to recreate:  We can enumerate in this version by simply trying username and password combos. As you can see, in the GIF, when I put in invalid usernames it says "Invalid Username". As soon as I do a valid username with an incorrect password, we are given: "The password you entered for the username enumtestuser is incorrect". By automating something like this, a hacker could potentially guess a valid username.
  
  - [ ] Affected source code:  I was not able to locate the exact code responsible. I did find a plugin called "Unified Login Error Messgages" that outputs the message "Invalid username/password combination" when a valid username is entered.
    
1. (Optional) Vulnerability Name or ID
  - [ ] Summary: 
    - Vulnerability types:
    - Tested in version:
    - Fixed in version: 
  - [ ] GIF Walkthrough: 
  - [ ] Steps to recreate: 
  - [ ] Affected source code:
    - [Link 1](https://core.trac.wordpress.org/browser/tags/version/src/source_file.php)
1. (Optional) Vulnerability Name or ID
  - [ ] Summary: 
    - Vulnerability types:
    - Tested in version:
    - Fixed in version: 
  - [ ] GIF Walkthrough: 
  - [ ] Steps to recreate: 
  - [ ] Affected source code:
    - [Link 1](https://core.trac.wordpress.org/browser/tags/version/src/source_file.php) 

## Assets

20MB+ file with embedded script for attack #1.

## Resources

- [WordPress Source Browser](https://core.trac.wordpress.org/browser/)
- [WordPress Developer Reference](https://developer.wordpress.org/reference/)

GIFs created with [LiceCap](http://www.cockos.com/licecap/).

## Notes

Describe any challenges encountered while doing the work

## License

    Copyright 2018 Jonathan Neronde

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
