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
>     open browser 	https://www.nopcommerce.com/en/demo	chrome
>     click link	xpath://a[contains(text(),'Log in')] #get the xpath from inspection
>     input text id:Email	pavanoltraining@gmail.com #get id from inspection
>     input text id:Password	Test@123 #get id from inspection
>     click element xpath://body/div[6]/section[1]/div[1]/div[1]/div[1]/div[1]/div[1]/div[2]/div[1]/div[2]/form[1]/div[2]/div[4]/input[1]
>     close browser #closes the browser
>     
> #now we can do 
> *** Test Cases ***
> LoginTest
> 	open browser ${url}	${browser}
>     loginToApp
>     close browser
>   
> ```
>
> Note: think of keywords as functions in programming 

Link to see selenium keywords: http://robotframework.org/SeleniumLibrary/SeleniumLibrary.html#Keywords

To run our test cases, we go in the terminal and type in `robot directory\filename.robot` 

We can see a report of our results from our test cases by going into our 'venv' folder and open the 'report.html' in the browser

## Working with Text Box/Input Box

`maximize browser window` keyword will maximize browser

