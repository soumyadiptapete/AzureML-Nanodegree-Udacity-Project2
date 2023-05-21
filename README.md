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

![image](https://github.com/soumyadiptapete/AzureML-Nanodegree-Udacity-Project2/assets/20270621/3f7b9e0a-530d-484f-98f0-a0dc73e05ac3)



2)	Create and submit an AutoML run
![image](https://github.com/soumyadiptapete/AzureML-Nanodegree-Udacity-Project2/assets/20270621/a9a0c49c-37d5-40ca-bf24-a77eed383449)



3)	Check the best model in the AutoML run in terms of AUC
![image](https://github.com/soumyadiptapete/AzureML-Nanodegree-Udacity-Project2/assets/20270621/3e67089f-c7f8-47ca-b8f3-516c29553d85)


4)	Deploy the best model as a webservice using ACI and authentication enabled

Note- I deployed both the best model and another model. The best model deployment takes a lot of time and deployment state was healthy momentarily and then changed to unhealthy. Therefore, I used the one of the other models from the AutoML run , with comparable AUC as the best model, in the subsequent steps
5)	Enable Application insights in the deployed model by running logs.py script in CLI
6)![image](https://github.com/soumyadiptapete/AzureML-Nanodegree-Udacity-Project2/assets/20270621/efef937b-2c56-4251-a131-392c0632e088)


7)	Download the swagger.json file from the endpoints section of the deployed model. Visualize the methods in the file by using swaggerUI
![image](https://github.com/soumyadiptapete/AzureML-Nanodegree-Udacity-Project2/assets/20270621/203687bf-dcb8-4feb-8ad3-5669fcbfae14)



8)	Test the deployed model by using the endpoint.py where a JSON payload is sent to the deployed model and yes/no responses are sent back

![image](https://github.com/soumyadiptapete/AzureML-Nanodegree-Udacity-Project2/assets/20270621/18af8304-8808-436f-a62e-bc01a58392a6)



9) Benchmark the model using the apache benchmark tool using the benchmrk.sh script. IT basically sends multiple scoring requests to the deployed mdoel and returns a set of metrics for these multiple calls 

![image](https://github.com/soumyadiptapete/AzureML-Nanodegree-Udacity-Project2/assets/20270621/bfddb280-7611-4a44-993c-b17dc672336a)

Second Approach (via pipeline in Jupyter notebook)
1) get workspace
2) Create compute cluster or use existing one
3) Load dataset and check the columns of the data
4) Create an AutoML step. The AutoML step will contain outputs in form of metrics of AutoML runs and the best model by AutoML
5) Create a Pipeline and include the AutoML step as the pipeline steps
6) Run the pipeline
![image](https://github.com/soumyadiptapete/AzureML-Nanodegree-Udacity-Project2/assets/20270621/abf7394c-9f1e-4e3e-94b3-8ebdcd6fcb96)

![image](https://github.com/soumyadiptapete/AzureML-Nanodegree-Udacity-Project2/assets/20270621/b0bf484a-5a71-43d4-915e-13da097d2ea6)

7) Visualize the metrics for all runs
8) Retrieve the best model and test it.
9) Publish the pipeline
![image](https://github.com/soumyadiptapete/AzureML-Nanodegree-Udacity-Project2/assets/20270621/94808603-4f86-48d0-a956-5a8b9c792d0e)

10) Get the rest endpoint of the published pipeline and authentication header 
![image](https://github.com/soumyadiptapete/AzureML-Nanodegree-Udacity-Project2/assets/20270621/de7e6260-1a2f-446c-a4b3-af72e9217831)

11) Call the rest endpoint to submit the pipeline run as a new experiment

12) Get the run id of the new pipeline and check the run details
![image](https://github.com/soumyadiptapete/AzureML-Nanodegree-Udacity-Project2/assets/20270621/bf99ea25-67f5-41ea-84a9-528dbce75cae)

RunDetails of pipeline run
![image](https://github.com/soumyadiptapete/AzureML-Nanodegree-Udacity-Project2/assets/20270621/efcb2de0-ecd6-4ec8-b049-d426aa90e916)
Completion of automl run in RunDetails
![image](https://github.com/soumyadiptapete/AzureML-Nanodegree-Udacity-Project2/assets/20270621/88730533-f6e4-4a0d-944f-d01473766b50)





13) check the new run in the AzureML studio. Shown in red box in below screenshot
![image](https://github.com/soumyadiptapete/AzureML-Nanodegree-Udacity-Project2/assets/20270621/84b69652-291f-4c28-81f2-996ece6726d7)


## Screen Recording
https://www.youtube.com/watch?v=oTWYkGNgnvs
## Future Improvements
1)	Do further exploratory analysis of the data to find out the important features correlated with the outcome
2)	A hyperdrive run on the dataset choosing some of the best models produced by AutoML to further finetune the hyperparameters
3)	Create a pipeline for a hyperdrive run for a simple logistic regression model or any other model that had high metrics from AutoML. The AutoML best model is an ensemble of various models which reduces examinability which in turn is not preferred by banks


