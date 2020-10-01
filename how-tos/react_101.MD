## React 101

### Base commands:

- Create project:

```bash
npx create-react-app <app name>
```

- Add dependency to project:

```bash
npm i <package name>
# Or go to root/package.json and add it on dependency field
```

- Start app:

```bash
npm start
```

### Install on linux:

```bash
# install NVM (version manager for node)
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.34.0/install.sh | bash
bash install_nvm.sh

# refresh terminal profile
source ~/.profile

# list all node version that can be installed
nvm ls-remote

# pick one version and install (replace X with version)
nvm install X

# use installed version (replace X with version)
nvm use X
```

### Usefull dependencies:

- Router dom: to have routes we have to use router.

```bash
npm i react-router-dom
```

- Material design: simple and responsive deisgned components

```bash
npm install @material-ui/core
npm install @material-ui/icons
```

### State Managment

```bash
npm i redux OR npm i recoil
```
