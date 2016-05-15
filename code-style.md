#Coding Style of the HTML,JS and CSS/SASS  
*this document aims at improving collaboration,code quality and enabling supporting infrastructure.*
***
## 1. General style rules
**1.1 file and resource names: follow the same naming conventions**

* minus(-) sign as the separating parts in a file name
* lower case letter sign as the file name where possible 
* special sign as the file name in special cases
    *  versions in the post-fix as outlined in the post-fix note
    *  flag file for a special purpose(underscore for compass to ignore a certain file for direct css compilation)
* post- or pre-fixes or extensions (i.e. .min.js, .min.css) or reeving which includes some pre-fixes (i.e. file hashes like 3fa89b.main.min.css). In those cases we recommend to use dot's to separate the clear purpose of this additional meta-data in a filename.

 **Recommended**
 ```
 my-script.js
 my-camel-case-name.css
 i-love-underscores.html
 thousand-and-one-scripts.js
 my-file.min.css
 ```
 **Not recommended**
 ```
 MyScript.js
 myCamelCaseName.css
 i_love_underscores.html
 1001-scripts.js
 my-file-min.css
 ```

**1.2 Protocol**

* Omit the protocol portion(`http:`,`https:`) from embedded resources unless the respective files are not available over both protocols.
* makes URL relative,prevents mixed content issues and results in minor file size savings
 
 **Recommended**
 ```
 <script src="//cdn.com/foundation.min.js"></script>
 .example {
   background: url(http://static.example.com/images/bg.jpg);
 }
 ```
 **Not recommended**
 ```
 <script src="http://cdn.com/foundation.min.js"></script>
 .example {
   background: url(http://static.example.com/images/bg.jpg);
 }
 ```

**1.3 Text Coding**

* Indent by 2 spaces at a time.
* semicolon(;) sign added to the end of the line.
* Comments:
    -  don't comment what's coded
    -  comment why it was coded this way and comment the thinking behind.
    -  include links in your comments to open issues, specifications etc.
* use [JSDoc](http://usejsdoc.org/) or [YUIDoc](http://yui.github.io/yuidoc/) for JS annotation
* code checking: [JSLint](http://www.jslint.com/) or [JSHint](http://jshint.com/)
 ```
    <ul>
      <li>Fantastic</li>
      <li>Great</li>
      <li>
        <a href="#">Test</a>
      </li>
    </ul>

    @media screen and (min-width: 1100px) {
      body {
        font-size: 100%;
      }
    }

    (function(){
      var x = 10;

      function y(a, b) {
        return {
          result: (a + b) * x
        }

      }
    }());
 ```

## 2. HTML style ruleste
**2.1 Document type**

* HTML5 (HTML syntax) is preferred for all HTML documents: <!DOCTYPE html>.

**2.2 HTML validity**

* Use valid HTML codess unless that is not possible due to otherwise unattainable performance goals regarding file size.

* Use tools such as the W3C HTML validator to test.

* Using valid HTML is a measurable baseline quality attribute.
* I just have 