# How to contribute

Before you contribute start with a bit of research. Check if ther are any rules for what you're about to add. If there's no rule, let's get started. 
You can see the entire rules set in https://github.com/EitanWo/findNfix/tree/main/rules 

### 1. Select a rule name and create your contribution folder
In the "contributions" folder create a folder with the name of your new rule.

Eg. You're planning to create a rule for docker commands that warns you when you're runing something ```--privileged```. 
We'll name it ```dockerPrivileged``` 
Once you picked a name create a folder called same thing as your rule name under ```contributions```.
Then create a json file with your rule name where you'll store your rule logic and a few files we can use for tests. We'll use 1 file called ```dockerPrivilegedTest1.sh``` 

Your final folder structure should look something like this: 
```
|-- contributions
|   `-- dockerPrivilege.                  <-- Folder where the rule and test files goes
|       |-- dockerPrivilege.json          <-- JsonFile with the rules and Fix
|       `-- dockerPrivilegeTest1.sh.      <-- Test files 
```

### 2. Create your rule 
The rule that will find the vulnerability will be created in the JSON file. 
There are 2 ways of creating a rule. Depending on how skilled you are with regex you can either: 
- Create a regex rule that will identify the rule and report back the vulnerable code constructs
- Describe your rule and what the problem is with a brief paragraph 

To start building your rule in the .json file use the following keys followed by either regex or a short description:
- ```"rule":"--priviledged"``` - If you know how to create your regex. In our case we're specifically looking for the --priviledged flag so there's no need to create a complex regex. 
- ```"rule_explained":"the --priviledged flag in docker run commands can be dangerous"``` - If you do not know the regex formula explain what the rule should look for. One of the project contributors will look at the submission and create the rule. A good place to work on your regex is here [RegexGenerator](https://regex-generator.olafneumann.org/?sampleText=2020-03-12T13%3A34%3A56.123Z%20INFO%20%20%5Borg.example.Class%5D%3A%20This%20is%20a%20%23simple%20%23logline%20containing%20a%20%27value%27.&flags=i&onlyPatterns=false&matchWholeLine=true&selection=) 

### 3. Create your fix 
After the rule is created you need to provide a fix. The fix is optional, but highly recommended. Automatically fixing a vulnerability can make the life of developers a lot easier. 

Similar to the rule, you can either use a regex formula to decide how to change it or explain with your own words how to change it. 

To create your fix, in the .json file use the following keys followed by either regex or a short description:
- ```"fix":""``` - In this case we'll simply remove the --privileged flag. However, you can have more complex formulas in here to create your fix. 
- ```"fix_explained":"the --priviledged flag should be removed from the docker run command"``` - If you do not know how to construct the fix, explain in your own words what's expected behaviour. 

### 4. Fill in the finding details
You final rule should look something like this: 
```
{
    "CodingLanguage":["Angular","JavaScript"],
    "rule":"\\S+_rule",
    "fix":"fix_rule",
    "cwe":"89",
    "findingType":"SQL Injection",
    "severity":"High",
    "ApplicationType":"web",
    "ContributorID":"123",
    "RuleType":"FindNFix",
    "FixType":"Interactive",
    "ArticleID":"12"
}
```
