# neko-rooms

<p align="center">
  <img src="https://img.shields.io/github/v/release/m1k1o/neko-rooms" alt="release">
  <img src="https://img.shields.io/github/license/m1k1o/neko-rooms" alt="license">
  <img src="https://img.shields.io/docker/pulls/m1k1o/neko-rooms" alt="pulls">
  <img src="https://img.shields.io/github/issues/m1k1o/neko-rooms" alt="issues">
  <a href="https://discord.gg/3U6hWpC" ><img src="https://discordapp.com/api/guilds/665851821906067466/widget.png" alt="Chat on discord"></a>
</p>

Simple room management system for [n.eko](https://github.com/m1k1o/neko). Self hosted rabb.it alternative.

<div align="center">
  <img src="https://github.com/m1k1o/neko-rooms/raw/master/docs/rooms.png" alt="rooms">
  <img src="https://github.com/m1k1o/neko-rooms/raw/master/docs/new_room.png" alt="new room">
  <img src="https://github.com/m1k1o/neko-rooms/raw/master/docs/neko.gif" alt="n.eko">
</div>

## How to start

You need to have installed `Docker` and `docker-compose`. You need to have custom domain pointing to your server's IP.

You can watch installation video provided by *Dr R1ck*:

https://www.youtube.com/watch?v=cCmnw-pq0gA

### Installation guide

You only need `.env.example`, `docker-compose.yml` and `traefik/`.

You don't need to have traefik as your entrypoint reverse proxy. In that case you can use `docker-compose.http.yml` that will expose this service to `APP_PORT`.

### Step 1

Copy `.env.example` to `.env` and customize.

```bash
cp .env.example .env
```

### Step 2

Create `usersfile` with your users:

```bash
touch traefik/usersfile
```

And add as many users as you like:

```bash
echo $(htpasswd -nb user password) >> traefik/usersfile
```

### Step 3

Create `acme.json`

```bash
touch traefik/acme.json
chmod 600 traefik/acme.json
```

Update your email in `traefik/traefik.yml`.

### Download images / update

You need to pull all your images, that you want to use with neko-room. Otherwise you might get this error: `Error response from daemon: No such image:` (see issue #1).

```sh
docker pull m1k1o/neko:latest
docker pull m1k1o/neko:chromium
# etc...
```

If you want to update neko image, you need to pull new image and recreate all rooms, that use old image. To update neko rooms, simpy run:

```sh
docker-compose pull
docker-compose up -d
```

### Roadmap:
 - [x] add GUI
 - [x] add HTTPS support
 - [x] add authentication provider for traefik
 - [x] allow specifying custom ENV variables (TODO: FE.)
 - [ ] allow mounting direcotries for persistent data
 - [ ] add upgrade button
 - [ ] auto pull images, that do not exist
 - [ ] add bearer token to for API
 - [ ] add docker ssh / tcp support
 - [ ] add docker swarm support
 - [ ] add k8s support
