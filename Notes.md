MLOps:

1. Create a virtual environment:
	- python -m venv <v_name>
	- source <v_name>/bin/activate		

2. Microservice Boilerplate
	- cmd	: pip install cookiecutter
	- cmd	: cookiecutter https://github.com/drivendata/cookiecutter-data-science

3. Inside the PROJECT folder:
	CREATE: 
	    1. Folders: Data_Set & saved_models
	    2. dvc.yaml
	    3. params.yaml
	    4. src/ get_data.py
	    5. src/ create_folder.py
	- cmd	:	dvc init
	- snapshot into git

	BackEnd:
	Data_Set Folders	: place the dataset
	get_data			: connecting params.config to get_data
						(which will select data from the Data_Set)

Note:
	in Params.yaml:
		training: False
		reason: if its true, it will train again so, whenever we are trying with new model
		make it true and then change it to false.
	IN Mlfow:
		to track the log of the model:
				-  for deep learning : mlflow.keras
				- for Machine learning: mlflow.sklearn.log.model

4. Create 
	1. Split.py
	2. model_train.py
	3. Evaluate.py

	BackEnd:
	split.py 		- split the dataset into train and test
	model_train.py 	- train the model
	evaluate.py 	- evaluates the trained model

5. Creating a MLFlow:
	UPDATE:
		1. params.yaml
	CREATE:
		1. Folder: artifacts
		2. src/ model_mlflow.py
		3. add mlflow in requirements.

		5. Run the server and run the model_mlflow.py
	
	To run MLFlow server:
		mlflow server --backend-store-uri sqlite:///mlflow.db --default-artifact-root ./artifacts --host 127.0.0.1 -p 5000


6. Setting up an automation, in which it will choose the best model:
	UPDATE:
		1. dvc.yaml
	CREATE:
		1. src/ log_production.py

7. Hosting in AWS:
	CREATE:
		1. .github/workflows
		2. Procfile
	
8. Creating django:
		1. cmd:	django-admin startproject webapp
		2. Create the main app called firstApp inside the webapp.
			Reason: This is were manage.py exists. Django uses manage.py to run the app
		3. cmd:	django-admin startapp firstApp
	CREATE:
		1. FOLDER: template, media, static
		2. Inside template: create an index.html
	UPDATE:
		1. webapp/webapp/settings.py
		2. webapp/webapp/urls.py
		3. webapp/firstApp/views.py

	***NOTE***
		Run the MLflow server first and then run the django server
	***TroubleShoot***
		Train the model_train.py again	

	To run the firstApp, need to be in the webapp directory
	1. cmd: mlflow server --backend-store-uri sqlite:///mlflow.db --default-artifact-root ./artifacts --host 127.0.0.1 -p 5000
	2. cmd: python manage.py runserver

Future Scope:
1. Find a way to use the latest production stage model into the Django App


Notes:
	Web Server Gateway Interface (WSGI) server runs Python code to create a web application.
	csrf token: its an added feature of django, which will check for the vulnerability of the file
	
Errors Faced
1. .DS_Store -> go to directory: find . -name '.DS_Store' -type f -delete
2. kill the server: npx kill-port 5000
