# Phoenix from Scratch
Part of what makes nanobox so useful is you don't even need Elixir or Phoenix installed on your local machine to use them.

## Create a Phoenix project
Create a project folder and change into it:

```bash
mkdir nanobox-phoenix && cd nanobox-phoenix
```

**HEADS UP**: All `nanobox` commands *must* be run from within your project folder.

#### Add a boxfile.yml
Nanobox uses a <a href="https://docs.nanobox.io/boxfile/" target="\_blank">boxfile.yml</a> to configure your app's environment.

At the root of your project create a `boxfile.yml` telling Nanobox you want to use the Elixir <a href="https://docs.nanobox.io/engines/" target="\_blank">engine</a>. You'll also want to add `inotify-tools` as a development package so it'll be available in your local dev environment:

```yaml
run.config:
  # elixir runtime
  engine: elixir
  
  # we need nodejs in development
  # ensure inotify exists for hot-code reloading
  dev_packages:
    - nodejs
    - inotify-tools
    
  # cache node_modules
  cache_dirs:
    - node_modules
    
  # add node_module bins to the $PATH
  extra_path_dirs:
    - node_modules/.bin
    
  # enable the filesystem watcher
  fs_watch: true

# add postgres as a data component
data.db:
  image: nanobox/postgresql
```

**NOTE**: In the proceeding `boxfile.yml`, Nanobox is told to include nodejs and run a postgres database as this is the most common configuration. Feel free to modify your configuration for your specific needs.

## Generate a Phoenix App
```bash
# drop into a nanobox console
nanobox run

# install Phoenix
# Phoenix Framework 1.2
mix archive.install https://github.com/phoenixframework/archives/raw/master/phoenix_new.ez

# Phoenix Framework 1.3
mix archive.install https://github.com/phoenixframework/archives/raw/master/phx_new.ez

# generate our new phoenix application

# cd into the /tmp dir to create an app
cd /tmp

# generate the phoenix app (Use your own app name)

# Phoenix Framework 1.2
mix phoenix.new app (Do not fetch dependencies at this moment)

# Phoenix Framework 1.3
mix phx.new app (Do not fetch dependencies at this moment)

# cd back into the /app dir
cd /app
  
# copy the generated app into the project
cp -a /tmp/app/* .

# exit the console
exit
```

## Configure Phoenix

#### Modify the config/dev.exs and config/test.exs

If your app is using a database, you'll need to modify the config to use environment variables generated by Nanobox:

Go to your project folder and modify the file: config/dev.exs as follows:

```elixir
# Configure your database
config :app, App.Repo,
  adapter: Ecto.Adapters.Postgres,
  username: System.get_env("DATA_DB_USER"),
  password: System.get_env("DATA_DB_PASS"),
  hostname: System.get_env("DATA_DB_HOST"),
  database: "app_dev",
  pool_size: 10
```

Go to your project folder and modify the file: config/test.exs as follows:

```elixir
# Configure your database
config :app, App.Repo,
  adapter: Ecto.Adapters.Postgres,
  username: System.get_env("DATA_DB_USER"),
  password: System.get_env("DATA_DB_PASS"),
  hostname: System.get_env("DATA_DB_HOST"),
  database: "app_test",
  pool_size: 10
```
#### Install NPM
In your desktop, got to your project folder
 
```bash
nanobox run
cd assets && npm install
```

#### Still at the nanobox console, lets create and migrate the Database
```bash
cd /app
mix ecto.create
```

## Fetch your Dependencies
Inside of your Nanobox console, fetch your app's dependencies:

```bash
mix deps.get
```
#### Lets exit the nanobox console 
```bash
exit
```

## Run the app
In your desktop, got to your project folder

#### Phoenix Framework 1.2
```bash
nanobox run mix phoenix.server
```

#### Phoenix Framework 1.3
```bash
nanobox run mix phx.server
```

#### Lets add a DNS record to access your applications
In your desktop, got to your project folder

```bash
nanobox dns add local phoenix.dev
```

Visit your app at <a href="http://phoenix.dev:4000" target="\_blank">phoenix.dev:4000</a>

## Explore
With Nanobox, you have everything you need develop and run your Phoenix app:

```bash
# drop into a Nanobox console
nanobox run

# where elixir is installed
elixir -v

# your packages are available
mix list

# and your code is mounted
ls

# exit the console
exit
```

## Now what?
Whats next? Think about what else your app might need and hopefully the topics below will help you get started with the next steps of your development!

* [Add a Database](/elixir/phoenix/add-a-database)
* [Frontend Javascript](/elixir/phoenix/frontend-javascript)
* [Local Environment Variables](/elixir/phoenix/local-evars)
* [Back to Phoenix overview](/elixir/phoenix)
