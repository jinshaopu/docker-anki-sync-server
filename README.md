# Anki Sync Server with Docker - and it works!

A quick and ergonomic way to setup a (reasonably) up-to-date instance of Anki Sync Server, without the hassle.

> Based on tsudoko's [`ankisyncd`](https://github.com/tsudoko/anki-sync-server)

**For detailed tutorials, visit [ankicommunity.github.io](https://ankicommunity.github.io/)**

We're also happy to help you on [Gitter](https://gitter.im/ankicommunity/community).

## News

* 2020-10-17: moved most of the Tutorials to the recently created [Wiki](https://ankicommunity.github.io/)

* 2020-09-21:

  Follow us on Gitter to learn the current progress of supporting newer versions of Anki!

  https://gitter.im/ankicommunity/community

  Special thanks for the work of the server contributors, among them to [AntonOfTheWoods](https://github.com/AntonOfTheWoods) and [VikashKothary](https://github.com/VikashKothary)!

  Learn more about the common problem here:

  * [SyncRedirector can support earlier versions of anki](https://github.com/kuklinistvan/docker-anki-sync-server/issues/16#issuecomment-626304807)
  * [Will it work on newest version on of Anki desktop? (unlikely for now)](https://github.com/ankicommunity/docker-anki-sync-server/issues/5)
  * [Unable to login on Anki 2.1.23-1](https://github.com/kuklinistvan/docker-anki-sync-server/issues/15)
  * ["Your client is using unsupported sync protocol (10, supported version: 9) ](https://github.com/kuklinistvan/docker-anki-sync-server/issues/14)
  * [Dont work on ARM CPU (Raspberry pi)](



## Technical

### Tested and works on

|    Date    | AnkiDesktop version | AnkiDroid version |                      ankisyncd version                       | Tester       |
| :--------: | :-----------------: | :---------------: | :----------------------------------------------------------: | ------------ |
| 2020-02-06 |       2.1.19        |       2.9.1       | [2.1.0 + 2bfccf7f](<https://github.com/kuklinistvan/anki-sync-server/tree/docker-release>) | kuklinistvan |

[Learn more about what "tested" means here.](Testing.md)

* * https://github.com/ankicommunity/docker-anki-sync-server/issues/9)


### About this Docker image

* As of yet, it lives on DockerHub at [kuklinistvan/anki-sync-server:latest](https://hub.docker.com/r/kuklinistvan/anki-sync-server).
* It was built for `x86_64` CPU architecture.

An example setup with docker-compose:

```
version: "3"

services:
    anki-container:
        image: kuklinistvan/anki-sync-server:latest
        container_name: anki-container

        restart: always
        ports:
        - "27701:27701"
        volumes:
        - data:/app/data

volumes:
data:
```

#### Rebuilding the image

Enter the Docker directory and alter `build.sh` to suit your use case. Run it to build the image on the current platform.

### Tested client downloads

|                            | Main                                                         | Mirror                                                       | Size     | SHA256                                                       |
| -------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | -------- | ------------------------------------------------------------ |
| AnkiDesktop  for GNU/Linux | [2.1.19](https://apps.ankiweb.net/downloads/current/anki-2.1.19-linux-amd64.tar.bz2) | [2.1.19](https://mega.nz/file/lVxRgRwI#Oqohl1M0Ju9RrYa7D6uV5SOtwgqVxkxPKqNYxcOh858) | 127.7 MB | `ada59237b8b3774712d6309821db4b6cb1d2c625284302aa09bc7313ada76fc0` |
| AnkiDroid APK for Android  | [2.9.1](https://fdroid.tetaneutral.net/fdroid/archive/com.ichi2.anki_20901300.apk) | [2.9.1](https://mega.nz/file/YFoFER5S#BiMMDxyhdl_u9I1TC-v_bBYakM5DTTM5CybJb4pu4oY) | 10.7 MB  | `511ef65b8dcb65a7f99f9942c4fcee5134f137ce23c677cf1ea3b26c7c3f34c5` |
| AnkiDesktop for Windows  | [2.1.19](https://apps.ankiweb.net/downloads/current/anki-2.1.19-windows.exe) | [2.1.19](https://mega.nz/file/5MwhxLjT#TLGA03KMbnRmDiHO3A-Yfm-y6xNgW3eiDUgEk-TXYyU) | 97,3 MB  | `90be6a3e5a6f4373ba3342bd3dfbe61e9013bb2a4acced2fcdd594b4c651a665` |
| AnkiDesktop for Mac OS X | [2.1.19](https://apps.ankiweb.net/downloads/current/anki-2.1.19-mac.dmg) | [2.1.19](https://mega.nz/file/dc4HXbKZ#m17YAdB5-SZ_rET23g8VT12Y-ECMB6rd1UIUfmKMEHg) | 127,5 MB | `9be3e3bdf884f865e15f308e72b1ed0213c061d27102f80d01897d5355eef8e7` |

### Administration interface is reachable through the container shell

    # docker exec -it anki-container /bin/sh
    /app/anki-sync-server # ./ankisyncctl.py --help
    usage: ./ankisyncctl.py <command> [<args>]
    
    Commands:
      adduser <username> - add a new user
      deluser <username> - delete a user
      lsuser             - list users
      passwd <username>  - change password of a user
    /app/anki-sync-server # ./ankisyncctl.py adduser kuklinistvan
    Enter password for kuklinistvan:
    /app/anki-sync-server #

## Does not work? Submit an issue!

I highly encourage you contacting me if you feel it is "broken again" - it frustrates me too and I'd like to take the effort to fix the bugs on my side.

Even if it is not a bug but rather something to be clarified, I'm happy to answer questions (if I can), so if you have one, just submit an issue.
