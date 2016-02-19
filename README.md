"Wifi with me" is a webapp to inventory people's will to participate in a wireless ISP.

# Run from Docker

If you have docker-compose installed, the only command needed is :

```console
docker-compose up -d
```

If you only have the base Docker program, you can simply run :

``` console
docker run -d --name wifi-with-me -p 8080:8080 --restart=unless-stopped teleragno/wifi-with-me
```

**Warning :** for now, no data volume has been set, so be carefull that your data will be lost if the container is deleted.

# Run from sources

## Requirements

We use bottle micro-framework.

```console
apt-get install python-bottle
```

(current code works with debian-stable version of bottle)

or

```console
pip install bottle
```

## Running

```console
./backend.py
```


Then hit *http://localhost:8080*

To run in debug mode (auto-reload)

```console
DEBUG=1 ./backend.py
```

Bottle will reload on source change, but not on template change if you're using
an old version of bottle.

You can specify listening port and address by setting `BIND_PORT` and
`BIND_ADDR` env vars, ex:

```console
BIND_ADDR='0.0.0.0' BIND_PORT=8081 ./backend.py
```

Default is to listen on `127.0.0.0`, port `8080`.

You can also pass a `URL_PREFIX='/some_folder/'` if you don't want the app to be
served at the root of the domain.

## Create the DataBase

```console
python backend.py createdb
```

## Build GeoJSON files

```console
python backend.py buildgeojson
```

## Drop the database

```console
rm db.sqlite3
```

What else ?

## Customizing appearance

Wether you like or not balloons, you may want to override some templates and/or
static files.

You can mention a `CUSTOMIZATION_DIR` as environ variable. In that dir, you can
create *assets* and *views* subdirs, containing files with the name of the
original files you want to override from default *assets* and *views*.

For example to override only *main.css* and *base.tpl*, you would set
`CUSTOMIZATION_DIR=/home/alice/my-fancy-isp-theme` and use the following directory
layout :

    /home/alice/my-fancy-isp-theme/
    ├── assets
    │   └── main.css
    └── views
        └── base.tpl
