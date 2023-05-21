# AzureML-Nanodegree-Udacity-Project2
Operationalizing machine learning on the bankmarketing dataset

# Operationalizing Machine Learning

The goal of the project was two train a machine learning model to understand if the product (term deposit) being marketed by a bank would be subscribed or not. Therefore, it is a classification problem
Two different approaches were adopted. The first involved training an AutoML model on the bankmarketing dataset and deploying it via the AzureML GUI.
The other approach involved creating, publishing, and running and AutoML pipeline

## Architectural Diagram
Approach 1 (Via AzureML GUI)

![image](https://github.com/soumyadiptapete/AzureML-Nanodegree-Udacity-Project2/assets/20270621/adb4674e-833f-4224-827a-bff9609b24e7)



Approach 2 (Via pipeline in Jupyter notebook)

![image](https://github.com/soumyadiptapete/AzureML-Nanodegree-Udacity-Project2/assets/20270621/92c12cc1-1951-41e5-8b53-daa64f2f1bef)



## Future Improvements
1)	Deep learning can be included in the AutoML classification task to check if AUC improves
2)	Banks usually do not want complicated models as it hinders in the regulatory process. Therefore, a simple logistic regression model could be optimized via hyperdrive and deployed 

## Key Steps
First Approach (via GUI):
1)	Upload dataset and register it

![image](https://github.com/soumyadiptapete/AzureML-Nanodegree-Udacity-Project2/assets/20270621/3de514d9-294f-4110-b4a6-3239bbbb903d)




2)	Create and submit an AutoML run
![image](https://github.com/soumyadiptapete/AzureML-Nanodegree-Udacity-Project2/assets/20270621/c8f9820f-b9e4-4555-8ca9-e526b1f40f2d)




3)	Check the best model in the AutoML run in terms of AUC
![image](https://github.com/soumyadiptapete/AzureML-Nanodegree-Udacity-Project2/assets/20270621/407ccb09-b575-4c4f-8b7d-b9492010de0e)



4)	Deploy the best model as a webservice using ACI and authentication enabled

Note- I deployed both the best model and another model. The best model deployment takes a lot of time and deployment state was healthy momentarily and then changed to unhealthy. Therefore, I used the one of the other models from the AutoML run , with comparable AUC as the best model, in the subsequent steps

5)	Enable Application insights in the deployed model by running logs.py script in CLI

6) ![image](https://github.com/soumyadiptapete/AzureML-Nanodegree-Udacity-Project2/assets/20270621/3cd54c25-0978-4b3f-92fc-96eb8d294a95)



7)	Download the swagger.json file from the endpoints section of the deployed model. Visualize the methods in the file by using swaggerUI
![image](https://github.com/soumyadiptapete/AzureML-Nanodegree-Udacity-Project2/assets/20270621/8a6a4300-d0a1-43ee-9044-da8a26e14d15)




8)	Test the deployed model by using the endpoint.py where a JSON payload is sent to the deployed model and yes/no responses are sent back

![image](https://github.com/soumyadiptapete/AzureML-Nanodegree-Udacity-Project2/assets/20270621/8daedadd-b855-4315-9a69-10abf3144cd2)




9) Benchmark the model using the apache benchmark tool using the benchmrk.sh script. IT basically sends multiple scoring requests to the deployed mdoel and returns a set of metrics for these multiple calls 

![image](https://github.com/soumyadiptapete/AzureML-Nanodegree-Udacity-Project2/assets/20270621/296a91a3-5f81-4acc-8ff2-8a8d5bdd8a19)


Second Approach (via pipeline in Jupyter notebook)
1) get workspace
2) Create compute cluster or use existing one
3) Load dataset and check the columns of the data
4) Create an AutoML step. The AutoML step will contain outputs in form of metrics of AutoML runs and the best model by AutoML
5) Create a Pipeline and include the AutoML step as the pipeline steps
6) Run the pipeline
![image](https://github.com/soumyadiptapete/AzureML-Nanodegree-Udacity-Project2/assets/20270621/18189ca0-37c2-44fb-b9c1-ca822b277ce4)

7) Visualize the metrics for all runs
8) Retrieve the best model and test it.
9) Publish the pipeline
![image](https://github.com/soumyadiptapete/AzureML-Nanodegree-Udacity-Project2/assets/20270621/8084d559-e2b1-4516-999c-659616f4ebd0)

10) Get the rest endpoint of the published pipeline and authentication header 
![image](https://github.com/soumyadiptapete/AzureML-Nanodegree-Udacity-Project2/assets/20270621/419bc762-5ee5-4281-9f9f-2032e1812f13)


11) Call the rest endpoint to submit the pipeline run as a new experiment

12) Get the run id of the new pipeline and check the run details
![image](https://github.com/soumyadiptapete/AzureML-Nanodegree-Udacity-Project2/assets/20270621/ff9312f2-363d-4f4b-b881-2fb96e2ed461)

RunDetails of pipeline run
![image](https://github.com/soumyadiptapete/AzureML-Nanodegree-Udacity-Project2/assets/20270621/07d2bdc2-e43f-42e1-ae79-4a33190b4074)

Completion of automl run in RunDetails
![image](https://github.com/soumyadiptapete/AzureML-Nanodegree-Udacity-Project2/assets/20270621/78297f5e-0ba3-46a3-9fdd-845d23efe69e)





13) check the new run in the AzureML studio. Shown in red box in below screenshot
![image](https://github.com/soumyadiptapete/AzureML-Nanodegree-Udacity-Project2/assets/20270621/e719c22b-09d7-45ce-a383-6f1468759a7d)


## Screen Recording
https://www.youtube.com/watch?v=oTWYkGNgnvs
## Future Improvements
1)	Do further exploratory analysis of the data to find out the important features correlated with the outcome
2)	A hyperdrive run on the dataset choosing some of the best models produced by AutoML to further finetune the hyperparameters
3)	Create a pipeline for a hyperdrive run for a simple logistic regression model or any other model that had high metrics from AutoML. The AutoML best model is an ensemble of various models which reduces examinability which in turn is not preferred by banks


