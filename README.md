# Perry (testing)
> This is where we pre-release Perry. This branch is mainly used for testing Perry for stability and error checks before final commits are merged to the master branch.

[![forthebadge made-with-python](http://ForTheBadge.com/images/badges/made-with-python.svg)](https://www.python.org/)
[![ForTheBadge built-with-love](http://ForTheBadge.com/images/badges/built-with-love.svg)](https://GitHub.com/Naereen/)

[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)
[![Codacy Badge](https://app.codacy.com/project/badge/Grade/ac5b62f098ca476098e3e4e92b9a149c)](https://www.codacy.com/manual/marchingon12/Perry?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=marchingon12/Perry&amp;utm_campaign=Badge_Grade)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat)](http://makeapullrequest.com)
[![Actively Maintained](https://img.shields.io/badge/Maintenance%20Level-Actively%20Maintained-green.svg)](https://gist.github.com/cheerfulstoic/d107229326a01ff0f333a1d3476e068d)

![logo](https://telegra.ph/file/39c9eb2839d62825da531.png)


A modular Telegram Python bot running on python3 with an sqlalchemy database.

Starting of as a simple group management bot with multiple admin features, it has evolved, becoming extremely modular and
simple to use. Note that this project uses well-known Telegram-bot of it's time @BanhammerMarie_bot from Paul Larson as it's base.
This bot is now used mainly for the finf group.

Can be found on Telegram as [Perry](https://t.me/PlatapusBot).

Join the [news channel](https://t.me/FinfBotNews) if you just want to stay in the loop about new features or
announcements.

## Credits

Skittbot for Stickers module and memes in extras module.

1maverick1 for many stuffs.

AyraHikari for weather modules and some other stuffs.

RealAkito for reverse search modules.

MrYacha for connections module.

ATechnoHazard for many stuffs.

corsicanu and nunopenim for android modules.

starryboi for packing it all into Skylee and python-markdown2 fork.

Any other missing credits can be seen in commits!

## Starting the bot

Once you've setup your database and your configuration (see below) is complete, simply run:

`python3 -m perry`


## Setting up the bot (Read this before trying to use!)

Please make sure to use python3.6, as I cannot guarantee everything will work as expected on older python versions!
This is because markdown parsing is done by iterating through a dict, which are ordered in v3.6 by default.

You may be using a server where sudo and superuser rights are not permitted by the admins and can only access the server using ssh. If this is the case, you may want to use [tmux](https://github.com/tmux/tmux/wiki), so that when you disconnect from your ssh session the bot will be kept alive.

Quick example:
- Start a new session:

  `tmux new-session -s perrybot`

- Move into Perry/perry and start the bot:

  `cd Perry/perry && python3 -m perry`

- Detach session:

  `Ctrl+b+d`

Now Perry should be running in the background within a tmux session.

### Configuration

There are two possible ways of configuring your bot: a config.py file, or ENV variables.

The prefered version is to use a `config.py` file, as it makes it easier to see all your settings grouped together.
This file should be placed in your `perry` folder, alongside the `__main__.py` file .
This is where your bot token will be loaded from, as well as your database URI (if you're using a database), and most of
your other settings.

It is recommended to import sample_config and extend the Config class, as this will ensure your config contains all
defaults set in the sample_config, hence making it easier to upgrade.

An example `config.py` file could be:
```python
from perry.sample_config import Config


class Development(Config):
    OWNER_ID = 894380120 # your telegram ID; easiest way is to search and start 'userinfobot' from Telegram directory
    OWNER_USERNAME = "austinsama"  # your telegram username; if you don't have one, set one
    API_KEY = "your bot api key"  # bot api token, as provided by the botfather (yes, daddy)
    SQLALCHEMY_DATABASE_URI = 'postgresql://username:password@localhost:5432/database'  # sample db credentials
    MESSAGE_DUMP = -1234567890 # group-chat/channel id; dumps logs as messages in dedicated room
    USE_MESSAGE_DUMP = True # set true/false to log or not
    SUDO_USERS = [13130992, 29831388]  # List of id's for users which have sudo access to the bot.
    LOAD = [] # choose which modules to load
    NO_LOAD = [] # choose which modules to exclude
    TELETHON_HASH = "None" # api_hash from my.telegram.org
    TELETHON_ID = "None" # api_id from my.telegram.org
```

### Python dependencies

Install the necessary python dependencies by moving to the project directory and running:

`pip3 install -r requirements.txt`.

This will install all necessary python packages.

### Database

If you wish to use a database-dependent module (eg: locks, notes, userinfo, users, filters, welcomes),
you'll need to have a database installed on your system. I am currently using ElephantSQL, but Postgresql is the recommended choice for optimal compatibility if you have sudo/superuser rights.

#### ElephantSQL Setup

For those who do not have access to sudo and superuser rights of the server you want to host Perry on, ElephantSQL is a good enough alternative with a limited free plan. In comparison to Postgresql, ElephantSQL hosts the database on a different server, whereas by using Postgresql you are directly creating and using the database in the host server as a system user. This method requires less steps than the Postgres method, but you are putting your trust into the service provider (ElephantSQL - services currently available are: Google Cloud, AWS, Azure. Last checked: September 12th 2020).

1. Sign up for an account.

2. Choose your plan. You will get options to choose which region and which company to host the database server on.

3. Create your instance.

4. Copy the URL and paste it where`SQLALCHEMY_DATABASE_URI =` lies in your `config.py` file.


#### Postgres Setup
In the case of Postgres, this is how you would set up a the database on a debian/ubuntu system. Other distributions may vary.

- Install postgresql:

  - Debian/Ubuntu:
<<<<<<< HEAD

    `sudo apt-get update && sudo apt-get install postgresql`

  - Arch Linux:

=======

    `sudo apt-get update && sudo apt-get install postgresql`

  - Arch Linux:

>>>>>>> f6f615e7e35eb6db9fa0c1987593a61c31225e2c
    `sudo pacman -Syu && sudo pacman -S postgresql`

- change to the postgres user:

  `sudo su - postgres`

- create a new database user (change YOUR_USER appropriately):

  `createuser -P -s -e YOUR_USER`

This will be followed by you needing to input your password.

- create a new database table:

  `createdb -O YOUR_USER YOUR_DB_NAME`

Change YOUR_USER and YOUR_DB_NAME appropriately.

- finally:

  `psql YOUR_DB_NAME -h YOUR_HOST YOUR_USER`

This will allow you to connect to your database via your terminal.
By default, YOUR_HOST should be 0.0.0.0:5432.

You should now be able to build your database URI. This will be:

`sqldbtype://username:pw@hostname:port/db_name`

Replace sqldbtype with whichever db youre using (eg postgres, mysql, sqllite, etc)
repeat for your username, password, hostname (localhost?), port (5432?), and db name.

## Modules
### Setting load order.

The module load order can be changed via the `LOAD` and `NO_LOAD` configuration settings.
These should both represent lists.

If `LOAD` is an empty list, all modules in `modules/` will be selected for loading by default.

If `NO_LOAD` is not present, or is an empty list, all modules selected for loading will be loaded.

If a module is in both `LOAD` and `NO_LOAD`, the module will not be loaded - `NO_LOAD` takes priority.

### Creating your own modules.

Creating a module has been simplified as much as possible - but do not hesitate to suggest further simplification.

All that is needed is that your .py file be in the modules folder.

To add commands, make sure to import the dispatcher via

`from Perry import dispatcher`.

You can then add commands using the usual

`dispatcher.add_handler()`.

Assigning the `__help__` variable to a string describing this modules' available
commands will allow the bot to load it and add the documentation for
your module to the `/help` command. Setting the `__mod_name__` variable will also allow you to use a nicer, user
friendly name for a module.

The `__migrate__()` function is used for migrating chats - when a chat is upgraded to a supergroup, the ID changes, so
it is necessary to migrate it in the db.

The `__stats__()` function is for retrieving module statistics, eg number of users, number of chats. This is accessed
through the `/stats` command, which is only available to the bot owner.
