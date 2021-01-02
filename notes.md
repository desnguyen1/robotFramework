# Robot Framework General Notes

A generic test automation framework for acceptance testing

Acceptance test-driven development (ATDD)

utilizes keyword-driven testing approach

Essentially, the script that is written in the IDE will be given to a webdriver which will then connect with the web for testing the script

Note: for pycharm IDE we need to install Intellibot plugin

## Setup:

> * Install python
>   * Download python from python.org
>   * On Windows, go to c: drive and find the download python folder (most likely in Program Files x86 folder)
>   * Go to the scripts folder inside and copy the file path
>   * Right click on 'This PC' > click on properties
>   * Click on advanced system settings > Advanced tab > Environment variables
>   * Under 'System Variables' click on 'Path' > edit > new 
>   * Past the copied file path and click 'Ok' to exit all windows
>   * Pip should be installed with python, to check if python and pip is properly installed, go to terminal and type in 'python --version' and 'pip --version' which should give us the version numbers for each
> * Install Pycharm IDE
> * Install Selenium - optional
>   * `pip install selenium` 
> * Install robot framework
>   * `pip install robotframework` 
> * Install robot framework selenium library
>   * `pip install robotframework-seleniumlibrary` 
>
> Note: we can check if these are installed by typing in `pip list` which will show a list of python packages installed 
>
> Inside pycharm, create a project
>
> * Go to file > settings > Project: 'name_of_project' > Python interpreter 
> * Click on the '+'
> * Search for selenium (if installed), robotframework, and robotframework-seleniumlibrary and install those packages
>
> Note: for every new project created, we need to do this step if we want to use robotframework
>
> Now go to plugins
>
> * Install 'Intellibot @Selenium...'

Note: for test cases using this framework will be `.robot`

## Multiple Sections  (Multiple Test Cases)

First section is the settings: `*** Settings ***`

> Here we add libraries by importing
>
> Ex: `Library SeleniumLibrary` 

Next section is variables: `*** Variables ***`

> Here we defined variables that are commonly used in each test case
>
> Ex: `${var_name} <tab> value` 
>
> `${browser}	chrome`

Test case section: `*** Test Cases ***`

> Here we can write multiple test cases
>
> Layout:
>
> ```python
> *** Test Cases ***
> name_of_test_case
> 	create webdriver browser <tab> executable_path="path_of_driver_on_local_machine\driver_name"
> 	keyword <tab space>	parameter <tab space> browser <tab> 
> ```
>
> Note: for browser, if using chrome, firefox, edge, etc. We need to download driver from selenium's website > https://www.selenium.dev/downloads/ 
>
> > should keep a drivers folder and store the different drivers in there
>
> Note: instead of adding `create webdriver broser....` to every test case, we can add the `.exe` file of the webdriver to the python/scripts folder to avoid writing that line (but we must make sure that we added the PATH in our PC from the setup stage)
>
> Ex:
>
> ```python
> *** Test Cases ***
> LoginTest
> 	#if we did NOT add the driver to our Python/scripts folder, otherwise we can ignore it
> 	create webdriver chrome	executable_path="C:\drivers\chromedriver.exe"
>     open browser 	https://www.nopcommerce.com/en/demo	chrome
>     click link	xpath://a[contains(text(),'Log in')] #get the xpath from inspection
>     input text id:Email	pavanoltraining@gmail.com #get id from inspection
>     input text id:Password	Test@123 #get id from inspection
>     click element xpath://body/div[6]/section[1]/div[1]/div[1]/div[1]/div[1]/div[1]/div[2]/div[1]/div[2]/form[1]/div[2]/div[4]/input[1]
>     close browser #closes the browser
> 
> ```
>
> Note: to get xpath, we need to inspect the page and copy the xpath url link (easier way is to get the chropath extension)
>
> For testing text boxes (username, password, etc) we use `input text` keyword

keywords section: `*** Keywords ***`

> Here we defined our own keywords
>
> Ex: 
>
> ```python
> new_keyword
> 	#we can add steps to a test case
> #ex
> loginToApp
> 	#if we did NOT add the driver to our Python/scripts folder, otherwise we can ignore it
> 	create webdriver chrome	executable_path="C:\drivers\chromedriver.exe"
>  click link	xpath://a[contains(text(),'Log in')] #get the xpath from inspection
>  input text id:Email	pavanoltraining@gmail.com #get id from inspection
>  input text id:Password	Test@123 #get id from inspection
>  click element xpath://body/div[6]/section[1]/div[1]/div[1]/div[1]/div[1]/div[1]/div[2]/div[1]/div[2]/form[1]/div[2]/div[4]/input[1]
> 
> 
> #now we can do 
> *** Test Cases ***
> LoginTest
> 	open browser ${url}	${browser}
>  loginToApp
>  close browser
> 
> ```
>
> Note: think of keywords as functions in programming 
>
> More selenium keywords in references



## Running the test case 

To run our test cases, we go in the terminal and type in `robot directory\filename.robot` 

> More detailed:
>
> `robot -d nameOfFolderToStoreResults <path>\nameOfFile.robot` 
>
> ex:
>
> `robot -d results testCases\websiteTest.robot`
>
> This will store the results (log and report.html files) in a 'results' folder and run the test case

We can see a report of our results from our test cases by going into our 'venv' folder and open the 'report.html' in the browser

## Working with Text Box/Input Box

### Testing visibility of  input box

> `element should be visible` and `element should be enable` 
>
> Ex:
>
> ```python
> testingInputBox
> 	open browser ${url}	${browser}
>     title should be	titleOfPage
>     #creating a variable
>     ${"email_txt"}	set variable	id:email
>     
>     element should be visible	${"email_text"}
>     element should be enable	${"email_text"}
>     
>     #initializing the variable
>     input text	${"email_txt"}	someemail@gmail.com
> ```
>
> Note: we also have `element should not be visible/enable` 

## Notes on `set variable` 

Note: go to ex in Working with text box/input box section to see the usage of `set variable`

> We can think of `${"email_txt"} set variable	id:email` in terms of c++ as:
>
> > `email email_txt` or as `varType varName` 
>
> Then initializing `input text	${"email_txt"}	someemail@gmail.com` in terms of c++:
>
> > `email_txt = someemail@gmail.com` 

## Selecting Radio Buttons & Check Boxes

`select radio button` keyword

> Get the name and the value by inspecting page
>
> `select radio button	name	value` 
>
> ex:
>
> `select radio button 	sex	Female` 

`select checkbox`

> Get name/id of checkbox element
>
> `select checkbox	name/id`
>
> ex:
>
> `select checkbox	here` 
>
> Note: if it is already checked, then it will do nothing

`unselect checkbox`

> same concept as checking checkbox but we just use the `unselect` keyword



## Keywords

### title should be

> `title should be <tab>	<title_of_page>` 

> Need to inspect page and get <title>  element
>
> Verifies the title of the page

### maximize browser window

> maximizes the browser

### sleep	value

> `sleep	5`
>
> this will put a pause for 5 seconds before continuing to the next test step

### set selenium speed time

> `set selenium speed time` will set a pace for each step being executed
>
> ex:
>
> `set selenium speed 2seconds` will set a 2 second pace for each statement



## References

Robot framework BuiltIn Documentation: https://robotframework.org/robotframework/2.1.2/libraries/BuiltIn.html

Link to see selenium keywords: http://robotframework.org/SeleniumLibrary/SeleniumLibrary.html#Keywords