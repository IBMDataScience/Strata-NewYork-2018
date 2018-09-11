# Sales Product-Line Prediction

## Goal
Identify customers for marketing campaigns that are most likely to buy the targeted product-lines.


## Get Watson Studio

###  Create an account.

1.  Go to [https://www.ibm.com/cloud/watson-studio](https://www.ibm.com/cloud/watson-studio)

2.  Click the Start Your Free Trial button.

> <img src="https://github.com/IBMDataScience/Strata-NewYork-2018/blob/master/Sales%20Product-Line%20Prediction/Images/Get%20Watson%20Studio.png" width="624" height="300">


## Data
We will be using GoSales data from Watson Studio community to build this model. Below is the description of each column:

1. **GENDER**: Customer gender
2. **AGE**: Customer age
3. **MARITAL_STATUS**: "Married", "Single", or "Unspecified"
4. **PROFESSION**: General category of the customer's profession, such "Hospitality" or "Sales",or simply "Other"
5. **IS_TENT**: Whether or not the customer bought a tent
6. **PRODUCT_LINE**:(Target) The product category in which the customer has been most interested
7. **PURCHASE_AMOUNT**: The average amount of money the customer has spent on each visit to the store


### Step 1
Go to the [Watson Studio community](https://datascience.ibm.com/community).
 You can also navigate to the community from Watson Studio by clicking the _Community_ tab on the top panel.



### Step 2
Select the data set from the community and click the add (**+**) icon on the community card. Select your project and click Add.


After you add the data set to your project you can find it in the Data assets section under the _Assets_ tab.

## Tools
Watson Studio offers different options for working with your data. To model this problem and understand the user behavior to predict the sales product-line purchase, we will use IBM SPSS Modeler Flow in Watson Studio.
IBM SPSS Modeler Flow is a graphical interface to create different machine learning flows.

## Create SPSS Modeler Flow

#### Step 1
To create an SPSS Modeler Flow, go to the _Assets_ tab as shown above and click the _new flow_ icon under the SPSS Modeler Flow section.

#### Step 2
Give a name and description to the flow and select the _IBM SPSS Modeler runtime_.

 Once you are in SPSS modeler canvas you can drag and drop the node into the canvas and right-click to take further actions such as open, preview, or run.

## Load Data
To start working on the problem, first we need to get data into the canvas.
Select _Data Asset_ node from _import_ section of nodes and add _data file_ to the node by opening node.
To preview the file, right-click on a node and select preview.

## Data Audit
Before starting working on the data let’s learn more about our data.
We can use _Data Audit_ node to render the data summary statistics.

1. Drag the _Data Audit_ node and connect it with the _data_ node.
2. Right click on the node and select _open_ option to change settings or give a custom name. Hit _save_ button at the bottom to save all changes.
3. Right click on the node and select _run_ option. After running the node you can see your audit report on right side panel.

##  Drop Columns
We don't need IS_TENT column. Let's drop that column by using _Filter_ node
1. To drop columns drag and drop Filter node on the canvas and connect it with data node.
2. Right click and open the node. Select column name under filter section
 and hit save button.

Once our data is clean, we can set our PRODUCT_LINE variable as the target variable using the _Type_ node.
It will help our model to distinguish between input and target features.

1. Drag and drop the _Type_ node on the canvas, connect it the _Filter_ node, right click and open the node.
2. Click on configure types. Select column name PRODUCT_LINE, change role to target hit ok and then save.

## Exploring data through Graphs
Lets understand the interaction of the various attributes in the dataset.

Drag and drop Histogram Node from _Graphs_ section and select age in field and product_line in panel to get view to how people from different age groups by different product-line items.

We can work with different nodes from Graph section and get more insight into data.
Here is one more example - spending pattern of users based on age.

## Data Partition

One more step before building the classification model is to divide data into train and test sets. We will use the _Partition_ node for this.

1. Select Partition node and connect it with Type node.
2. Open the node and provide 80 and 20 values to training and testing partition respectively. It will divide 80% of the data for training and 20% for testing.



## Model Building - Classification

Now let’s fit the classification model. We will be using a C5.0 algorithm to build a decision tree. A C5.0 model works by splitting the data based on the field that provides the maximum information gain.You can see node C5.0 under the Modeling section of the nodes palette.

1. Drag and drop C5.0 node on canvas, connect it with partition node and open it to change settings.
2. Under build options select custom and provide model name as Decision Tree. Check Cross-Validate checkbox and enter number of folds 5.
3. Hit save button and run the node.

While building this model we don’t have to specify input and output variables. We have already done that in the Type node.
Once you run your decision tree model you will be able to see your model in a golden color node.


## View Model

Right-click on the golden color node and view the model. You can see predictor importance, tree diagram, and other model information here.

## Model Evaluation

1. Select _Analysis_ node from the _Output_ section of the node palette and connect it with the model.
2. Right click to run the node and open results from right hand side panel.

Similarly, use the Table node to view data in a table format with predicted labels and confidence.


## Save Model

Now it’s time to save our model. Right click on a _Model_ node (C5.0 Node) in the flow, click on save branch as a model option and provide model name to save this SPSS model to the project.
You can find this saved model in your project Asset tab under Watson Machine Learning Model section.

## Deploy Model
1. Find the saved model in project assets under Watson Machine Learning Model section. Click on the three vertical dots in front of your model under actions and select deploy option.
2. click (+) icon for add deployment, give name and description and hit save button at bottom.

You can find deploy status for your model under deployment tab in model.

You can open deployed model to get view details about deployment, find code snippets for API specifications in different languages and test your model.

Learn more about [SPSS Modeler](https://dataplatform.cloud.ibm.com/docs/content/analyze-data/ml-canvas.html?audience=wdp) here.
