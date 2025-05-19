# Benefits of using Docker

- Anyone can clone this project and `docker-compose up`.
  - No need to setup VMs/LAMP, virtual hosts, SSL, etc.
- Ease of testing different PHP and MySQL versions.
  - Just change version numbers in `/docker/Dockerfile` and `/docker-compose.yml`!

# Getting IMathAS up and running

- Get a copy of IMathAS.  If you are just playing around, you can
  download a zip from https://github.com/drlippman/imathas.  If you
  are planning on doing any development, you should fork the repo on
  Github, then use git to clone the repo on your computer.
- Install Docker. (see below: Docker Installation)
- Edit `docker-compose.yml` and edit the path `/c/IMathAS`
  to point to your copy of IMathAS.
- In the root of this project, run `docker-compose up`.
- In a web browser, go to `https://localhost/install.php`. In that, use:
  - Database server: db
  - Database name: imathasdb
  - Database username: imathas
  - Database password: imathas
  - You can leave the rest of the options as defaults, or adjust
    to your liking.
- Done!

## Things to know

- Ports 80 and 443 are functional. Yes, SSL will work! 
  (self-signed cert, of course)
- MySQL will be accessible via `127.0.0.1`, port `3305`.
- MySQL data files can be found in `$HOME/docker-data/mysql-imathas`.
- PHPMyAdmin can be accessed via `http://localhost:8081`

# Getting Vue dev server running

- Open the CLI for your Docker app
- Install npm by running `apt-get install npm`
- Disable ssl checking by running `npm config set strict-ssl false`
- Upgrade npm: `npm install npm@latest -g`
- Close and restart the CLI
- Change into the vue-src directory: `cd assess2/vue-src`
- Install dependencies: `npm install`
- Edit your config.php and add these lines:
  - `$CFG['assess2-use-vue-dev'] = true;`
  - `$CFG['assess2-use-vue-dev-address'] = 'http://localhost:8080';`
- Create the file `assess2/vue-src/.env.local` with the following contents:
  - `VUE_APP_IMASROOT=http://localhost`
  - `VUE_APP_PROXY=http://localhost`
  
Then you can start the development server: `npm run serve`.  

If you restart you computer or close Docker, you will need to run `npm run serve` 
again to restart the development server.


# Docker installation

Direct download links, because loginwall:
- Mac: https://download.docker.com/mac/stable/Docker.dmg
- Windows: https://download.docker.com/win/stable/Docker%20for%20Windows%20Installer.exe

Loginwall discussion: https://github.com/docker/docker.github.io/issues/6910

