# Software-2.0, ML project lifecycle, MLOps

![Software 1.0 vs 2.0](/screenshots/software-1.0-vs-2.0.png)

https://datacom.com/au/en/discover/articles/blog-adopting-ai-to-unlock-software-development-2-0

The “classical stack” of **Software 1.0** is what we’re all familiar with — it is written in languages such as Python, C++, etc. It consists of explicit instructions to the computer written by a programmer. By writing each line of code, the programmer identifies a specific point in program space with some desirable behavior.

In contrast, **Software 2.0** is written in much more abstract, human unfriendly language, such as the weights of a neural network. No human is involved in writing this code because there are a lot of weights (typical networks might have millions).

https://karpathy.medium.com/software-2-0-a64152b37c35

![Machine Learning project lifecycle](/screenshots/ML-project-lifecycle.png)

One of the most exciting moments of any machine learning project is when you get to deploy your model, but what makes deployment hard? There are two major categories of challenges in deploying a machine learning model. First, are the machine learning or the **statistical issues, and second, are the software engineering issues**. https://www.deeplearning.ai/


![Machine Learning Infrastructure](/screenshots/ML-infrastructure.png)

Only a small fraction of real-world ML systems is composed of the ML code, as shown by the small orange box in the middle. The required **surrounding infrastructure is vast and complex**. 
https://www.deeplearning.ai/



MLOps: It was born at the intersection of **DevOps**,  **Software Engineering,** **Data Engineering,** and **Machine Learning**, and it’s a similar concept to DevOps**,** but the execution is different. ML systems are experimental in nature and have more components that are significantly more complex to build and operate.
https://neptune.ai/blog/mlops

![MLOps level 0](/screenshots/MLOps-level-0.png)

- This is generally script or notebook driven for the most part and every training step is manual.This process is usually driven by **experimental code** that is written and executed in notebooks by data scientists interactively until a workable model is produced. 
- This creates a **disconnect between the ML and operations teams**. Among other things, this opens the door for **potential training serving skew**. To better understand what's going on here, let's assume data scientists and over a trained model to the engineering team to deploy it on their infrastructure per serving or batch prediction. This form of manual handoff could include putting the trained model in a file system somewhere, checking the model object into a code repository, or uploading it to a model registry.  
- Engineers who deploy the model need to **make the required input features available in production**, potentially for low latency serving, which can lead to training serving skew. 
- Because of fewer code changes, continuous integration or CI, and often even unit testing is totally ignored. 
- Experiment steps are often source controlled, and they produce artifacts such as trained models, evaluation metrics, and visualizations. Also, because there **aren't many model versions** that need to be deployed, continuous deployment or **CDs isn't even considered**
-  do not track or log the model predictions and actions which are required in order to detect model **performance degradation** and other **model behavioral drifts**

![Model decay](/screenshots/model-decay.png)

https://www.deeplearning.ai/


**Concept drift** occurs when the patterns the model learned no longer hold. The properties of the target variables may have shifted between the static training data and real-world dynamic data. The context has changed, but the model doesn’t know about the change. Its learned patterns do not hold anymore. **The cause of the relationship change is some kind of external event or process.** For example, we try to predict life expectancy using geographic regions as input. As the region’s development level increases (or decreases) region loses its predictive power, and our model degrades. https://deepchecks.com/data-drift-vs-concept-drift-what-are-the-main-differences/


**Data drift is the situation where the model’s input distribution changes**.  It weakens performance because the model receives data on which it hasn’t trained enough.
![Data drift](/screenshots/data-drift.png)

https://deepchecks.com/data-drift-vs-concept-drift-what-are-the-main-differences/

**Gradual or incremental drift** is the one we expect. No individual change is dramatic. Each might affect only a tiny segment. But eventually, they add up.
- Competitors launch new products. Consumers have more choices, and their behavior changes. As should sales forecasting models.
- Mechanical wear of equipment. Under the same process parameters, the patterns are now slightly different. It affects quality prediction models in manufacturing.

External changes might be more sudden or drastic. These are hard to miss. 
Almost overnight, the mobility and shopping patterns shifted. It affected all sorts of models.

![MLOps level 1](/screenshots/MLOps-level-1.png)

- One of the key goals of level one is to **perform continuous training of the model**, by **automating the training pipeline.** This lets you achieve **continuous delivery of train models to your model prediction service**. 
- To automate the process of using new data to retrain models in production, you need to introduce **automated data and model validation steps to the pipeline, as well as pipeline triggers and metadata management**. 
- Models are automatically retrained using fresh data based on live pipeline triggers
- The pipeline implementation that is used in the development or experimentation environment is also used in the pre production and production environment, which is a key aspect of MLOps practice for unifying the DevOPS effort. To construct ML pipelines components need to be reusable, composable, and potentially shareable across pipelines. Therefore, while ploratory data analysis code can still live in notebooks, the source code for components must be modularized.

![MLOps level 2](/screenshots/MLOps-level-2.png)

- This diagram presents one of the current architectures, which is **focused on enabling rapid and reliable update of the pipelines in production.** 
- This **requires robust automated CI/CD** to rapidly explore new ideas.
- They can implement these ideas and **automatically build test, and deploy new pipeline components** to the target environment. These MLOps setup includes components like source code control,  test and build services, deployment services, a model registry, a feature store, a metadata store, and a pipeline orchestrator.

![DevOps vs MLOps](/screenshots/DevOps-vs-MLOps.png)

https://neptune.ai/blog/mlops
DevOps and MLOps have fundamental similarities because MLOps were derived from DevOps principles. But they’re quite different in execution:
- Unlike DevOps, **MLOps is much more experimental in nature**. Data Scientists and ML/DL engineers have to tweak various features – hyperparameters, parameters, and models – while also keeping track of and managing the data and the code base for reproducible results.
-  **Testing** an ML system involves [model validation](https://link.medium.com/GxMQJqdQvbb), model training, and so on – in addition to the conventional code tests, such as unit testing and integration testing.
- **Automated Deployment**: you can’t just deploy an offline-trained ML model as a prediction service. You’ll need a multi-step pipeline to automatically retrain and deploy a model.
- **Production performance degradation of the system due to evolving data profiles or simply Training-Serving Skew**

[MLOps and DevOps](https://www.datasciencecentral.com/profiles/blogsmlops-vs-devops-the-similarities-and-differences) are **similar when it comes to continuous integration of source control, unit testing, integration testing, and continuous delivery of the software module or the package.** 

However, in ML there are a few notable differences:

-   **Continuous Integration** (CI) is no longer only about testing and validating code and components, but also **testing and validating data, data schemas, and models**.
-   **Continuous Deployment** (CD) is no longer about a single software package or service, **but a system (an ML training pipeline) that should automatically deploy another service (model prediction service) or roll back changes from a model.**
-   **Continuous Testing** (CT) **is a new property, unique to ML systems, that’s concerned with automatically retraining and serving the models.**