# How to contribute

Before you contribute start with a bit of research. Check if ther are any rules for what you're about to add. If there's no rule, let's get started. 
You can see the entire rules set under [Issues](https://github.com/CrowdQ/rules/issues)

### 1. Create your submission ticket
Navigate to the `Issues` page https://github.com/CrowdQ/rules/issues/new/choose and create a new issue using the `Issue sumbmission form`. Click on ***Get Started*** and let's begin!  

### 2. Find a vulnerability to create a rule for
If you're just getting started, a good place to start with your investigation is [**OWASP top 10**](https://owasp.org/www-project-top-ten/). 

Read about the vulnerabilities that exist and pick one you like best. After you picked a vulnerability it's time for you to pick a language and see if your selected vulnerability exists in said language. 

In this case we're going to look at at `A7:2017-Cross-Site Scripting XSS` and the languages I'm interested are JavaScript(JS) and Java & JSPs. 

### Vulnerability Type
I now know the vulnerability type I'm after: `Cross Site Scripting (XSS)`. Use this for the Vulnerability Typ field. 

### CWE
The second thing you'll want is the CWE value. Head over to [CWE](https://cwe.mitre.org/) and look for the vulnerability type and you'll quickly find the number you are after. You'll find that for XSS the value is 79. If you're unsure don't fill in the CWE Value. 

### Explain the Vulnerability you are tring to find
After a bit of research about how JavaScript and JSP can lead to XSS I found out that if I print out a parameter that was sent to my application without cleaning it out it can execute the JavaScript code embedded in there. 
As sources you can use blogs, research documents, OWASP is always a good source. 

`[Important]` Do not plagiarise other sources. While it's useful to read blogs and look at what others are doing, plagiarism will not be accepted. 

After you explained birefly the vulnerability, explain how someone could find this vulnerability. 

### How can we find the vulnerable code? 
Explain for what someone should look for if they want to find this vulnerability. Be as explicit as you can and include some code samples. Using the example above I know that we can print something out in JS with `document.write`. 

Within a JSP I can get a user input (or parameters) using `<%request.getParameter(parameterId)%>` 

This means that if someone will print that value without sanitizing it, they could become vulnerable to XSS.

```javascript
<script>
document.write(<%request.getParameter("userid")%>) 
</script>
```

### How can we fix this vulnerability?
Now that we know about how the vulnerability looks in code, we will want to understand how someone can fix this vulnerability.

This step is not mandatory, but having a strong fix (and a way to fix automatically) will strongly improve the addoption and usage of the rule. 
In the case above we can get the parameter in an encoded format wich will simply print out instead of being executed. The method we need to use is `getEncodedParameter` 

I can now write a snippet of code which shows how to fix the vulnerability:
```javascript
<script>
document.write(<%request.getEncodedParameter("userid")%>) 
</script>
```

### What apps are affected by the vulneraility 
Select from the list the type of apps that are affected by this vulnerability. If you think there's a different type of app that is not in the list, mention this in the further reading section. 

### Further reading 
In this section you will want to ad links ot external sources. In our case there's intheresting information about this in places like OWASP, the CWE article, and links to other blogs that explain what `getEncodedParameter`does and when it should be used instead of `getParameter` 

# 3. Select your issue title
At the top of the form you'll see something like this:
`[Rule&Fix]: <Vulnerability Name> - <Severity> - CWE <number>`

If you have both a detection Rule advisory and a way to fix it, user `Rule&Fix` otherwise simply use `Rule`. 
Select your vulnerability name. It can always be changed later if you don't like it. 
The select a severity and a CWE value. 
If you don't know what severity to use or what it means, use `Unknown`. A simple way of selecting a severity is to think about how much damage this vulnerability can do if exploited. If it's really bad, select Critical and go down to High, Medium, Low or Informational. 

# 4. Get started 
As a general advice you'll want to target at list items from the [OWASP Top 10](https://owasp.org/www-project-top-ten/) list or [2021 CWE Top 25 Most Dangerous Software Weaknesses](https://cwe.mitre.org/top25/archive/2021/2021_cwe_top25.html)
Don't be worried if what you want to create a rule for is not part of the list. Code is used in a lot of places nowadays, Infrastructure, internet of things, etc. Add your rule and a fix and it will make a lot of people's software more secure .


