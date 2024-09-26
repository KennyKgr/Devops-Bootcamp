# Flask API PROJECT

- This Exercise was meant to interact and test an api, understand how it works and get accostomed.

-Using my vscode I launched a **git bash** Terminal for my project 

-I used the series of commands to get the various results as follows

```

mkdir -p flask_api_project/{templates,static} && touch flask_api_project/app.py flask_api_project/
templates/index.html flask_api_project/static/style.css && python -m venv flask_api_project/venv

```

![start](/Project6/img/01_codes_at_work_setup_from_the_beginning.png)

- Install python and create the environment for flask

- when the environment was created I went ahead to paste the various codes

- app.py 

![app](/Project6/img/03_setup_app.py.png)

- setup the Index.html code

![index](/Project6/img/02_setup_index_file.png)

- style.css

![style](/Project6/img/04_setup_styles.png)

- I went ahead to creating a virtual environment and installing flask, with these commands

```

python -m venv venv
source venv/Scripts/activate
pip install Flask

```

![python](/Project6/img/05_Installing_Flask.png)

- Installed python as a path and updated pip version to 2.24

![python](/Project6/img/06_Install_python.png)

- I used **Flask run** to get the api running

![flask](/Project6/img/09_flask_run.png)

- accessed the api from my browser at **127.0.0.1:5000**

![flask](/Project6/img/07_accessed_flask_from_browser.png)

- Input my data and it was successful.

![ph](/Project6/img/08_input_my_info.png)

## Testing the Api

- I tested the api using postman 

- Created a **POST** request to my api address **http://127.0.0.1:5000/users.**

- selected the appropriate options in the body being **raw** and **json** and sent the request.

![request](/Project6/img/11_created_user_on_api_from_postman.png)

- Went to the api server and traffic showed the request

![request](/Project6/img/12_api_server_info.png)

### End Of Project