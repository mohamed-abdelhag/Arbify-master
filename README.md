

<div align="center">
<h1>Arbify</h1>
    
[![PHP workflow][php-workflow-badge]][php-workflow]


**Arbify is currently abandoned. Features that are already present should work without a problem, but no further support or development will be made here, at least for some time. Feel free to fork it!**

</div>


![Screenshot](resources/images/screenshot.png)

ARB files localization tool. Dedicated to [Flutter](https://flutter.dev) and its [intl](https://pub.dev/packages/intl) package.

## Installation

Firstly, copy the `.env.example` file to `.env` and fill it with the correct configuration for some of the services.

```bash
cp .env.example .env
nano .env # or vim or whatever you like :)
```

Commented lines are irrelevant, or you most probably shouldn't care about them. You may want to set `MAIL_*` variables
to use a proper SMTP server. Arbify logs the emails instead of sending them by default.

### Deploying

```bash
docker-compose build arbify
docker-compose up -d
docker-compose run --rm arbify docker/arbify/upgrade.sh
```

The `build` step and running the `upgrade.sh` script is required only after installing or updating the Arbify. You don't need to run it everytime.

After this you're ready to go to [http://localhost:8000](http://localhost:8000) and check out Arbify yourself!

The database is seeded with a pre-verified super administrator account `admin` with password `password`.

[php-workflow]: https://github.com/Arbify/Arbify/actions?query=workflow%3APHP
[php-workflow-badge]: https://img.shields.io/github/workflow/status/Arbify/Arbify/PHP

## Mohamed’s Mac mini: run steps (no rebuild, no upgrade)

Use this when you just want to start Arbify you already built before. No rebuilds, no upgrades.

Prerequisites:
- Docker Desktop installed on macOS and opened.

Every time you want to run Arbify:

1) Open Docker Desktop and wait until it shows “Docker Desktop is running”.

2) In a terminal, go to the project folder:

```sh
cd /Users/mohamedelobaid/baseet/Arbify-master
```

3) Start the containers (db, nginx, arbify):

```sh
docker-compose up -d
```

4) Give the database a few seconds to initialize. If the page shows a “Hold on!” or you get a 502, either refresh after ~10 seconds or restart Nginx:

```sh
docker-compose restart nginx
```

5) Open Arbify in your browser:

```sh
open http://localhost:8000
```

Login with:
- Username: `admin`
- Password: `password`

Stop the stack when you’re done:

```sh
docker-compose down
# or, to keep containers but stop them
docker-compose stop
```

Optional: view logs if something looks off

```sh
docker-compose logs -f nginx arbify db
```

Notes for Apple Silicon (M1/M2/M3):
- You might see a platform warning for the `arbify` container running as `linux/amd64`. That’s expected and okay; it runs under emulation.
- Do not run `docker-compose build` or the upgrade script unless you actually update the code. For daily use, steps above are enough.
