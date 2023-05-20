# AzureML-Nanodegree-Udacity-Project2
Operationalizing machine learning on the bankmarketing dataset

# Operationalizing Machine Learning

The goal of the project was two train a machine learning model to understand if the product (term deposit) being marketed by a bank would be subscribed or not. Therefore, it is a classification problem
Two different approaches were adopted. The first involved training an AutoML model on the bankmarketing dataset and deploying it via the AzureML GUI.
The other approach involved creating, publishing, and running and AutoML pipeline

## Architectural Diagram
Approach 1 (Via AzureML GUI)

![image](https://github.com/soumyadiptapete/udacity-azureml-project2/assets/20270621/ca449807-ab0e-40c2-94f9-6c508a4d3c1b)


Approach 2 (Via pipeline in Jupyter notebook)

![image](https://github.com/soumyadiptapete/udacity-azureml-project2/assets/20270621/22854337-3739-40fd-ba9b-6127889b3a4f)


## Future Improvements
1)	Deep learning can be included in the AutoML classification task to check if AUC improves
2)	Banks usually do not want complicated models as it hinders in the regulatory process. Therefore, a simple logistic regression model could be optimized via hyperdrive and deployed 

## Key Steps
First Approach (via GUI):
1)	Upload dataset and register it

![image](https://github.com/soumyadiptapete/udacity-azureml-project2/assets/20270621/bf925db2-0678-466c-9006-adfeed438150)


2)	Create and submit an AutoML run
![image](https://github.com/soumyadiptapete/udacity-azureml-project2/assets/20270621/47b781f6-b178-410e-9f65-7328759fd18a)



3)	Check the best model in the AutoML run in terms of AUC
![image](https://github.com/soumyadiptapete/udacity-azureml-project2/assets/20270621/5489b42e-994c-47c1-bcdb-deb6b195e6b2)

4)	Deploy the best model as a webservice using ACI and authentication enabled

Note- I deployed both the best model and another model. The best model deployment takes a lot of time and deployment state was healthy momentarily and then changed to unhealthy. Therefore, I used the one of the other models from the AutoML run , with comparable AUC as the best model, in the subsequent steps
5)	Enable Application insights in the deployed model by running logs.py script in CLI
6)	![image](https://github.com/soumyadiptapete/udacity-azureml-project2/assets/20270621/904b3c4b-116a-4560-936c-102650e1ed74)

7)	Download the swagger.json file from the endpoints section of the deployed model. Visualize the methods in the file by using swaggerUI
![image](https://github.com/soumyadiptapete/udacity-azureml-project2/assets/20270621/910cc193-5f31-46bd-b00a-f956326cecf4)

8)	Test the deployed model by using the endpoint.py where a JSON payload is sent to the deployed model and yes/no responses are sent back

![image](https://github.com/soumyadiptapete/udacity-azureml-project2/assets/20270621/fe89cec5-e63c-446b-8444-d5c27f5a6815)



9) Benchmark the model using the apache benchmark tool using the benchmrk.sh script. IT basically sends multiple scoring requests to the deployed mdoel and returns a set of metrics for these multiple calls 

![image](https://github.com/soumyadiptapete/udacity-azureml-project2/assets/20270621/4eb60438-d70d-476d-95b6-1b1c3add4f8a)

Second Approach (via pipeline in Jupyter notebook)
1) get workspace
2) Create compute cluster or use existing one
3) Load dataset and check the columns of the data
4) Create an AutoML step. The AutoML step will contain outputs in form of metrics of AutoML runs and the best model by AutoML
5) Create a Pipeline and include the AutoML step as the pipeline steps
6) Run the pipeline
![image](https://github.com/soumyadiptapete/udacity-azureml-project2/assets/20270621/d1d6b894-89b7-449e-8232-2c7355066396)


7) Visualize the metrics for all runs
8) Retrieve the best model and test it.
9) Publish the pipeline
![image](https://github.com/soumyadiptapete/udacity-azureml-project2/assets/20270621/9a07e970-b431-4a57-b61e-e29079849688)

10) Get the rest endpoint of the published pipeline and authentication header 
 ![image](https://github.com/soumyadiptapete/udacity-azureml-project2/assets/20270621/6fbe602c-6a96-43f0-9b33-f1453f76056c)

11) Call the rest endpoint to submit the pipeline run as a new experiment

12) Get the run id of the new pipeline and check the run details
 ![image](https://github.com/soumyadiptapete/udacity-azureml-project2/assets/20270621/3f5cedae-4f12-4332-ad36-a502525a1fbc)

RunDetails of pipeline run
![image](https://github.com/soumyadiptapete/udacity-azureml-project2/assets/20270621/e2abbc5b-7703-4f33-aa6c-ff643c31163c)
Completion of automl run in RunDetails
![image](https://github.com/soumyadiptapete/udacity-azureml-project2/assets/20270621/680377aa-3647-4891-a08b-820d62c297e0)





13) check the new run in the AzureML studio. Shown in red box in below screenshot
![image](https://github.com/soumyadiptapete/udacity-azureml-project2/assets/20270621/46ce9bc1-2b4d-443e-b1eb-79b789ef26fe)


## Screen Recording
https://www.youtube.com/watch?v=oTWYkGNgnvs
## Future Improvements
1)	Do further exploratory analysis of the data to find out the important features correlated with the outcome
2)	A hyperdrive run on the dataset choosing some of the best models produced by AutoML to further finetune the hyperparameters
3)	Create a pipeline for a hyperdrive run for a simple logistic regression model or any other model that had high metrics from AutoML. The AutoML best model is an ensemble of various models which reduces examinability which in turn is not preferred by banks


