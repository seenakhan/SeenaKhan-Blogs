# Steps to generate Azure DevOps work items with Power Automate
Hello all Power enthusiasts, welcome to my another blog. In today’s fast-paced development environment, automating repetitive tasks can significantly boost productivity. One such task is creating work items in Azure DevOps. By integrating Canvas App/ Microsoft Forms with Power Automate, you can streamline this process. This blog helps you to do the automation by using Canvas app.

## Objectives:-
### Tasks
1. Create Canvas App with appropriate controls and publish it.
2. Create Power Automate Flow - Automated Cloud Flow.
3. Integrate Canvas App and Azure Devops with Power Automate.
4. There are 2 Actions created in the Automated Cloud Flow.
   * Create from blank.
   * Create a Work-item in Azure Devops.
5. Create Azure Devops Work-items by running the canvas app.

### Prerequisites:-
* Access to Power Platform with Premium connection.
* Access to Microsoft Power Automate.
* Azure DevOps Premium connection in Microsoft Power Automate.
* Azure DevOps Organisation and Project

Here’s a step-by-step guide to help you set up this automation by using Canvas App, Power Automate and Azure DevOps.

#### Step 1: Create a Canvas App with proper controls and publish it.
1. Log in to Microsoft Power platform.
2. Select **Apps** from the left and select **Start with a Page Design** from the **+ New App** dropdonwn.
![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/an5n3qx4tdijfpntseqq.jpg)

3. Select **Blank Canvas** from **Select a page design to start your app**.
![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/hb5hgzsa42d0tsj79xcy.jpg)

4. Insert three text labels, two text boxes, one drop down list and a submit button.
![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/d72cnkty0gpuysp3g9b3.jpg)
5. Publish the app.

Step 2: Create a Table 
1. Select Data>Add data>Create new table
![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/rr1b04avlnajn86tx9lc.jpg)  
2. Select **Start with a blank table** from **Create a new table** screen.
3. Add three columns named, **Title** with Single Plain Text as data type, **Description** with Multiple Plain Text as data type and **NewWorkItem** with Single Plain Text as data type. Provide any name to the table.
![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ia7hoyv94o0zky7lmqd1.jpg)
4. Add a Patch() to add data to multiple records. In Power Apps, the Patch() function is used to create or update records in a data source. It’s a versatile function that allows you to modify specific fields without affecting other properties.

```
Patch('New tables', Defaults('New tables'), {Title:TextInput1.Text, Description:TextInput1_1.Text, NewWorkItem:Dropdown1.SelectedText.Value})
```
#### Step 3: Create a Power Automate Flow
1. From the left side of the Power App studio, Select Power Automate and select **Create new flow**.
![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/x50tbkwb4g2ov2ae9woq.jpg)

2. Name your flow and select **Create from blank**. After add a next step by Selecting Azure DevOps and Create a new item. When it asks for a SignIn, please enter your credentials and get signed in.
![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/bzhqh3lvgpxum44yppg0.jpg)
![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/1wz806tit83oi0oigwpv.jpg)
3. On the Create a new item step enter the following details:
   * Organization Name: Your Azure DevOps organization.
   * Project Name: Your Azure DevOps project.
   * Work Item Type: Tasks.
   * Title: FromPowerApps.
   * Description: FromPowerApps.
Then select **Save**.
4. Enter the following code on the Submit button's Onselect method.
```
DevOpsWorkItemflow.Run(TextInput1.Text, TextInput1_1.Text)
```
The two controls are for title and description. Publish the canvas app again.
You can run the Canvas app and submit a workitem into Your DevOps Project successfully.
You can use Microsoft Forms as well instead of Canvas App. In that case you dont need to configure a Dataverse table. For title and description you can take from the Forms parameters.

Hope you enjoy the session!!!

Thanks
