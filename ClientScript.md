Hello all Power enthusiasts, welcome to my another blog. The purpose of this blog is to go over how to implement standard user experience automation methods using Client Script API. You should use this particular client scripting API to implement your data interaction, form content changes, or app behavior updates. While writing your logic in JavaScript, keep in mind that, even if the form is built with standard HTML, direct manipulation of the form content is not supported. Client scripting creates an object model and methods for interacting with the various form components. This method assures that any changes to the layout or specific HTML used in form rendering do not disrupt your business logic. 

## Objectives:-
### Tasks
1. Prepare solution with the form.
2. Build the client script.
3. Upload the script.
4. Edit form.
5. Test.

### Prerequisites:-
* Access to Power Platform with Premium connection.
* Access to Power platform environment with sample apps enabled
* Basic understanding of Microsoft Power Platform and experience in 
  software development against the Microsoft stack and Visual Studio 
  code.
* Experience in administering solutions in Microsoft Azure is preferred.

Here’s a step-by-step guide to help you set up to implement Client script API in your model-driven applications in power platform.

#### Task 1: Prepare solution with the form.
In this task, you create a solution, create a model-driven app, add an existing table to the app, and prepare the main form of the table you added to the app.
* Log in to Microsoft Power platform.
* Select **Solutions** from the left and select **+ New Solution**.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/dgz20v9xhgw50mj5msa8.jpg)

* Enter the details as per the below image and click **Create**.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/g6c62ab37surg4vw1wkw.jpg)

* The soluiton will be created and open. Add a model-driven app by clicking on **+ New** and Select **App** then select Model-driven app.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/nlvp5x1temes62l1okpc.jpg)
* Enter the name as **ClientAPIApp** and then click on **Create**.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/676ds6f45ufihpiv7d5p.jpg)

* After creating the app, please select **Data**, then select **Apppointment** from the 'In your app' section then click on the elipsis and select **+ Add to app**.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/mi7ry5v3b3dyyrt26ngf.jpg)
Now Appointment data has been added to your model-driven app named ClientAPIApp.
* After adding the table select **Pages** and then select **Appointment form** for reviewing the form.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/p0j0ev4lsxwpjojxiz8z.jpg)
 You can see multiple sections and columns there in the form.
* Select **Appointment** main form from Appointment Forms section, then edit icon will appear, click on the edit icon. You will be redirected to Power Apps studio to edit the form.
* Select **Tree View** to identify the multiple sections and tabs in the form.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ucqvlbuxup42gty38jqr.jpg)
* Expand the Scheduling Information from the Tree view and select **Start Time**. Go to the properties pane and click on the information icon given. From there copy the logical name and paste in a notepad for the furture use.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/69nz6cdzh2cgwl4kst9l.jpg)

* Select the Description section from the Tree view and go to the properties then copy the name value and keep in a notepad for future use. Also check the **Hide** option. Then Select **Save and Publish** from the top bar.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/qcblyav51m2awvhzh0o5.jpg)

#### Task 2: Build the client script.

In this task, you create a script that shows/hides the Description section based on the Appointment start date.
Hide the Description section. If the Appointment start date is empty or in the past, otherwise show the Description section.

* Start a new instance Visual Studio Code or use your favorite code 
  editor. 
* Select Open Folder.
![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/4uu1r68ie4utbnybs8i2.png)

* Create a folder in your Documents folder and name it ClientScriptLab.

* Select the ClientScriptLab folder you created and Select Folder.

* Hover over the CLIENTSCRIPTLAB folder and select New File.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/c6mxrqiw9uznaghow02x.png)

* Name the file FormTeamProject.js.

Add the below functions to FormTeamProject.js. Your functions should have either unique names or use a namespace to ensure uniqueness.

JavaScript

```
function LearnLab_handleTeamProjectOnLoad(executionContext) {

}
function LearnLab_handleProjectStatusOnChange(executionContext) {

}
function LearnLab_hideOrShowStatusSection(formContext) {

}
```
* Add the below script to the OnLoad function. Notice the Appointment start column name here scheduledstart. This is the logical name you saved earlier. This code registers an onChange event handler and calls a common function to show/hide the section. You need to handle on change in case an appointment start date input changes the hide/show requirement.

JavaScript

```
var formContext = executionContext.getFormContext();
formContext.getAttribute('scheduledstart').addOnChange(LearnLab_handleProjectStatusOnChange);
LearnLab_hideOrShowStatusSection(formContext);
```

* Add the below script to the OnChange function. This code simply gets the formContext and then calls the common function to hide/show.

JavaScript
```
var formContext = executionContext.getFormContext();
LearnLab_hideOrShowStatusSection(formContext);
```
* Add the below script to the hideOrShowStatusSection function. Notice the tab name **appointment**, the section name **appointment description**, and column name **scheduledstart**.

JavaScript

```
var tabGeneral = formContext.ui.tabs.get('appointment');
var sectionStatus = tabGeneral.sections.get('appointment description');
var startDate = formContext.getAttribute('scheduledstart').getValue();
var CurrentDate = new Date();
if (startDate == null || startDate < CurrentDate) {
  sectionStatus.setVisible(false);
} else {
  sectionStatus.setVisible(true);
}
```
Your script should now look like this image.


![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/rrlsa9wyae9ecnclmmaf.jpg)

* Select File and Save.

#### Task3 : Upload the script.

In this task, you load the script you created into your environment.

* Navigate to Power Apps maker portal and make sure you are in the 
  correct environment.

* Select Solutions and open the ClientScriptingAI solution.

* Select **+ New** and then select **More | Web resource**.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/pu1eurfyfel8482hgnxf.jpg)

* Click on Choose file and select the Javascript file you have created in the previous task and then click **Save**. Automatically Display Name, Name and Filetype will be filled.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/33kl5dir2h2m51s8nez9.jpg)

Your solution should now have the Model-driven app, Appointment table, Appointment form and the FormTeamsProject.js web resource.

Don't navigate away from this page.

#### Task 4: Edit form.
In this task, you add JavaScript library to the Appointment main form and add an event handler for the On Load event.

Make sure you're still in the ClientScriptingAI solution.

* Open the model-driven app named ClientAPIApp.

* Select Appointment Forms and then edit the main Appointment form.

* Go to the Properties pane, select the Events tab, and select + Event Handler under OnLoad.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/qlwizf8p5vfk08904az8.jpg)

* From the Javascript library select the file you have added as a web resource in the previous task. Select FormTeamProject.js, and select Add.

* Select the library you added just now and Enter LearnLab_handleTeamProjectOnLoad for Function, check the Pass execution context as first parameter checkbox, and select Done.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/i3jo62r3qbbgmeiw662k.jpg)

* Select Save and publish and wait for your changes to be saved.
* Select the Back button.
* Select Publish in the Model-driven app and wait for the publishing to 
  complete.
* Go to Solution and select Publish all customizations and wait for the 
  publishing to complete.

#### Task 5: Testing your application.

In this task, you are going to test your appointment form in the model-driven app.

* Navigate to Power Apps maker portal and make sure you are in the 
  correct environment.

* Select Apps and play the ClientAPIApp.

* Select **Appointment** from the top bar.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/zcdi4r8yvmvedmq6ol07.jpg)

Under Scheduling information section Select Start date and provide any date from the past dates.You can see the Description section is not visible.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/gp2pjkq7c8bb9o0lovaw.jpg)

Press calendar icon next to the start date and select any future date. The Description section should become visible.


![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/nqzcjwotkadui2hb8lfl.jpg)

The Status section should now become visible.

You have now utilized JavaScript and the Client API to implement business requirements that cannot be implemented using declarative choices such as business rules.

Hope you enjoy the session!!!

Thanks

