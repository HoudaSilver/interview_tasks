
You need to create an automated test suite that automatically tests basic operations of d3a.io. The tests should use an precreated test user, in order to login to the website and test some basic operations of the website. The tests for these operations need to be defined as separate test cases. 
There are 3 main testcases that need to be created here: 
1. Login testcase. Validate that a precreated user is able to login to d3a.io
2. (Depends on testcase 1) Create a Project. Validate that a logged in user is able to create a project from this page https://www.d3a.io/projects (the page is also accessible via a link to the left panel, second icon from the top). Validate that the project is listed correctly after being created.
3. (Depends on testcase 2) Create a simulation. Validate that, if the project in testcase 2 has been created successfully, a logged in user can create a simulation (button "New Simulation" in the project view). The simulation can be empty, does not need to have any special setup. Also validate that the simulation is listed correctly.  

The automated test suite can be created either using Cypress or Selenium (ideally in Javascript or Python).

Extra points for writing the testcases in Gherkin syntax (given/when/then).


Solution :

Scripting TCs:

Scenario 1:


Given I am a precreated user on the website "d3a.io" 
When I click on login icon
And I enter "X@gmail.com" as email and "X2021!G@a" as password
When I click on Sign-in button
Then Login is successfully done


Scenario 2:

Given I am a logged-in user
When I Press the second icon from the top left of the page 
Then The Projects page is successfully displayed
When I create a project
Then The project is well created
And the project is correctly listed

Scenario 3:

Given I am a logged-in user
And I am on Projects page with a project already created and listed
And I press the "New simulation" button in the project view
Then The simulation is correctly launched
And The simulation is empty 

Automated test suite:

public class LoginSteps extends AbstractUISteps {
String userName = null;
@When("I am a precreated user on the website {string}")
public void am_on_website(string PageUrl) {
driver.navigate().to(PageUrl);
}
@When("I click on login icon")
public void i_click_on_login_icon() {
logInButton.click();
}
@And("I enter {string} as email and {string} as password")
public void i_enter_as_email(String email,String password) {

userName = email;

fillValueJs("//input[contains(@name,'email') ]","");

usernameField.sendKeys(userName);

fillValueJs("//input[contains(@name,'password') ]","");

passwordField.sendKeys( passWord);
}

@When("I click on sign-in button")
public void i_click_on_sign_in_button() {
signInButton.click();
}
@When("Login is successfully done")
public void isLoginSuccessed() {
Assert.assertTrue(

loginPrefix.getText().contains(userName))
}
}
@When("I am a logged-in user")

public void loggedInUser() {

Assert.assertTrue(

loginPrefix.getText().contains(email));

}

@When("I Press the second icon from the top left of the page ")

public void pressIcon() {

 secondIconButton..click();

}

@When("The Projects page is successfully displayed ")

public void projectPageisDisplayed() {

String url = driver.getCurrentUrl();

Assert.assertTrue(url.contains(« url of projet page »));

}
@When("I create a project")

public void createProject() {

createProjectButton.click();

}

@When("The project is well created")

public void projectIsCreated() {

Assert.assertTrue(ProjectName.contains(« name of project »));

}

@When("I am on Projects page with a project already created and listed")

public void projectPageAlreadyCreated() {

Driver.navigate.to(« url  to the page with a created project »);

}

@When("I press the "New simulation" button in the project view")

public void pressNewSimulation() {

 pressNewSimulationButton.click();

}

@When("The simulation is correctly launched")

public void simulationIsLanched() {

 Assert.assertTrue(logsText.isDisplayed());

}

When("The simulation is empty")

public void isSimulationEmpty() {

 Assert.assertFalse(StepsText.isDisplayed());

}

