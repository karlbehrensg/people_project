<div align="center">
  <h1>Vaccination System</h1>
</div>

<div align="center">
  <img src="readme-img/vaccination.png" width="80%">
</div>

# Content
- [Introduction](#Introduction)
- [How to use?](#How-to-use?)
- [Prerequisites](#Prerequisites)
    - [Windows](#Windows)
    - [macOS](#macOS)
    - [Linux](#Linux)
- [Install](#Install)
- [Run server](#Run-server)
    - [Local](#Local)
    - [Run server with public access](#Run-server-with-public-access)
    - [Run server in backgroud](#Run-server-in-backgroud)

# Introduction

This project was developed with `Django REST Framework` to keep track of _vaccinations_ and _drugs_ used through an API service. Here you can __create, read, update,__ and __delete__ __(CRUD)__ drugs and vaccinations.

The project was deployed publicly on AWS, so anyone can access it.

# How to use?

You can use the URL in your browser to interact with the API, but maybe is more useful do it with [Postman](https://www.postman.com/).

<div>
    <table>
        <tr>
            <th>URL</th>
            <th>Method</th>
            <th>Content Type</th>
            <th>Body values</th>
            <th>Restrictions</th>
            <th>Comment</th>
        </tr>
        <tr>
            <td>ec2-54-232-160-16.sa-east-1.compute.amazonaws.com:8000/drugs</td>
            <td>GET</td>
            <td></td>
            <td></td>
            <td></td>
            <td>List all registered drugs</td>
        </tr>
        <tr>
            <td>ec2-54-232-160-16.sa-east-1.compute.amazonaws.com:8000/drugs/:id</td>
            <td>GET</td>
            <td></td>
            <td></td>
            <td></td>
            <td>You get the detail of a drug.</td>
        </tr>
        <tr>
            <td>ec2-54-232-160-16.sa-east-1.compute.amazonaws.com:8000/drug</td>
            <td>POST</td>
            <td>application/json</td>
            <td>
                <p>name: string</p>
                <p>code: string</p>
                <p>descriptions: string</p>
            </td>
            <td>
                <p>Code can get max 10 chars and it's unique.</p>
                <p>Description can get max 255 chars.</p>
            </td>
            <td>Register a new drug.</td>
        </tr>
        <tr>
            <td>ec2-54-232-160-16.sa-east-1.compute.amazonaws.com:8000/drug/:id</td>
            <td>PUT</td>
            <td>application/json</td>
            <td>
                <p>name: string</p>
                <p>code: string</p>
                <p>descriptions: string</p>
            </td>
            <td>
                <p>Code can get max 10 chars and it's unique.</p>
                <p>Description can get max 255 chars.</p>
            </td>
            <td>Update a drug.</td>
        </tr>
        <tr>
            <td>ec2-54-232-160-16.sa-east-1.compute.amazonaws.com:8000/drug/:id</td>
            <td>DELETE</td>
            <td></td>
            <td></td>
            <td></td>
            <td>Delete a drug.</td>
        </tr>
        <tr>
            <td>ec2-54-232-160-16.sa-east-1.compute.amazonaws.com:8000/vaccinations</td>
            <td>GET</td>
            <td></td>
            <td></td>
            <td></td>
            <td>List all registered vaccinations</td>
        </tr>
        <tr>
            <td>ec2-54-232-160-16.sa-east-1.compute.amazonaws.com:8000/vaccinations/:id</td>
            <td>GET</td>
            <td></td>
            <td></td>
            <td></td>
            <td>You get the detail of a vaccination.</td>
        </tr>
        <tr>
            <td>ec2-54-232-160-16.sa-east-1.compute.amazonaws.com:8000/vaccinations</td>
            <td>POST</td>
            <td>application/json</td>
            <td>
                <p>rut: string</p>
                <p>dose: string</p>
                <p>date: string "yyyy-mm-dd"</p>
                <p>drug: drug id</p>
            </td>
            <td>
                <p>The verification digit will be validated, so need to be a valid rut (Chilean ID).</p>
                <p>Dose need to be 0.15 <= dose <= 1.0</p>
                <p>The drug ID need exist.</p>
            </td>
            <td>Register a new vaccination.</td>
        </tr>
        <tr>
            <td>ec2-54-232-160-16.sa-east-1.compute.amazonaws.com:8000/vaccinations/:id</td>
            <td>PUT</td>
            <td>application/json</td>
            <td>
                <p>rut: string</p>
                <p>dose: string</p>
                <p>date: string "yyyy-mm-dd"</p>
                <p>drug: drug id</p>
            </td>
            <td>
                <p>The verification digit will be validated, so need to be a valid rut (Chilean ID).</p>
                <p>Dose need to be 0.15 <= dose <= 1.0</p>
                <p>The drug ID need exist.</p>
            </td>
            <td>Update a vaccination.</td>
        </tr>
        <tr>
            <td>ec2-54-232-160-16.sa-east-1.compute.amazonaws.com:8000/vaccinations/:id</td>
            <td>DELETE</td>
            <td></td>
            <td></td>
            <td></td>
            <td>Delete a vaccination.</td>
        </tr>
    </table>
</div>
<br>

# Prerequisites

It's necesary install `MySQL` drivers and `Python>=3.6` to run this project.

## Windows

The easiest way to do in windows is installing `MySQL`, but there are some binary wheels you can install easily.

To install `Python` you can go to the [official page](https://www.python.org/).

## macOS

Install MySQL:

```zsh
$ brew install mysql
```

To install `Python` you can go to the [official page](https://www.python.org/).

## Linux

__Note that this is a basic step. I can not support complete step for build for all environment. If you can see some error, you should fix it by yourself, or ask for support in some user forum. Don't file a issue on the issue tracker.__

You may need to install the Python 3 and MySQL development headers and libraries:

Debian / Ubuntu
```
$ sudo apt update
$ sudo apt-get install python3-dev default-libmysqlclient-dev build-essential mysql-server
```

Red Hat / CentOS
```
% sudo yum install python3-devel mysql-devel
```

# Install

To install this project you need to clone this directory.
```zsh
$ git clone https://github.com/karlbehrensg/people_project.git
```

Now you need go into the project directory, create a virtual environment and install all its dependencies.

```zsh
$ cd people_project # Entry to project folder
$ python3 -m venv vevn # Create a virtual environment
$ source venv/bin/activate # Linux and macOS, to Windows use .\venv\Scripts\activate
$ pip install -r requirements.txt # Install all requirements.txt
```

If you do everything like the previews steps, your application will be connect with the database in AWS. If you want to use a personal database you can follow this steps.

Modify the settings.py file in `DATABASES` dictionary.

```py
...

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': BASE_DIR / 'db.sqlite3',
    }
}

...
```

This will change the database to a `sqlite` in your local machine.

# Run server

## Local

To run our server we need the terminal and execute the follow commands.

```zsh
$ python3 manage.py runserver
```

With this we can get access to API REST from our local machine. The valid URLS are:

<div>
    <table>
        <tr>
            <th>URL</th>
        </tr>
        <tr><td><a href="http://localhost:8000/drugs">http://localhost:8000/drugs</a></td></tr>
        <tr><td><a href="http://localhost:8000/drugs/2">http://localhost:8000/drugs/:id</a></td></tr>
        <tr><td><a href="http://localhost:8000/drug">http://localhost:8000/drug</a></td></tr>
        <tr><td><a href="http://localhost:8000/drug/2">http://localhost:8000/drug/:id</a></td></tr>
        <tr><td><a href="http://localhost:8000/vaccinations">http://localhost:8000/vaccinations</a></td></tr>
        <tr><td><a href="http://localhost:8000/vaccinations/1">http://localhost:8000/vaccinations/:id</a></td></tr>
    </table>
</div>

## Run server with public access

With this way you can run the server in your machine and get access from other devices. For this you need to know the IP address from the server machine.

Run the follow instruction in the terminal.

```zsh
$ python3 manage.py runserver 0.0.0.0:8000
```

<div>
    <table>
        <tr>
            <th>URL</th>
        </tr>
        <tr><td><a>yourIP:8000/drugs</a></td></tr>
        <tr><td><a>yourIP:8000/drugs/:id</a></td></tr>
        <tr><td><a>yourIP:8000/drug</a></td></tr>
        <tr><td><a>yourIP:8000/drug/:id</a></td></tr>
        <tr><td><a>yourIP:8000/vaccinations</a></td></tr>
        <tr><td><a>yourIP:8000/vaccinations/:id</a></td></tr>
    </table>
</div>

## Run server in backgroud

It's possible to run the server in background, on this way even when you close the terminal your server still running. For this we execute the server in a screen terminal.

```zsh
$ screen
$ python3 manage.py runserver 0.0.0.0:8000
```

To relese the terminal you need press `Ctrl+A` and after that press `D`, now you can close the terminal and the server still running.

If you want to stop the server you need to run in your terminal and know your the _screen id_ with:

```zsh
$ screen -ls
```

After you know the session id is you can kill it.

```bash
$ screen -XS [session id] quit
```

Example:

```zsh
screen -XS 20411 quit
```