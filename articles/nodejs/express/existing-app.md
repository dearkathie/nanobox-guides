# Existing Express App
Part of what makes Nanobox so useful is you don't even need Nodejs or Express installed on your local machine to use them.

## Setup

#### cd into your Express app
Change into an existing project folder:

```bash
cd my-express-app
```

**HEADS UP**: All `nanobox` commands *must* be run from within your project folder.

#### Add a boxfile.yml
Nanobox uses a <a href="https://docs.nanobox.io/boxfile/" target="\_blank">boxfile.yml</a> to configure your app's environment.

At the root of your project create a `boxfile.yml` telling Nanobox you want to use the Nodejs <a href="https://docs.nanobox.io/engines/" target="\_blank">engine</a>:

```yaml
run.config:
  engine: nodejs
```

## Configure Express

#### Listen on 0.0.0.0
To allow connections from the host machine into the app's container, you'll need to configure your app to listen on all available IP's (0.0.0.0) by modifying the `bin/www`:

```javascript
server.listen(port, '0.0.0.0');
```

#### Add local DNS
Add a convenient way to access your app from the browser:

```bash
nanobox dns add local express.dev
```

## Run the app
**HEADS UP**: If your app uses a database, you'll need to [add and configure it](/nodejs/express/add-a-database) before your app will run.

```bash
nanobox run npm start
```

Visit your app at <a href="http://express.dev:3000" target="\_blank">express.dev:3000</a>

## Explore
With Nanobox, you have everything you need develop and run your express app:

```bash
# drop into a Nanobox console
nanobox run

# where nodejs is installed,
node -v

# npm is installed,
npm -v

# and your code is mounted
ls

# exit the console
exit
```

## Now what?
Whats next? Think about what else your app might need and hopefully the topics below will help you get started with the next steps of your development!

* [Add a Database](/nodejs/express/add-a-database)
* [Frontend Javascript](/nodejs/express/frontend-javascript)
* [Local Environment Variables](/nodejs/express/local-evars)
* [Back to Express overview](/nodejs/express)
