# Infinity Feedback

This Project adds the Ability to OBS to propagate scene changes and send them to connected Smartphones. Infinity Feedback consists of four main parts: The OBS Plugin, the Android app, a React Webapp and a Node.JS Server. The App relies on Webspckets for fast communication between Server and Client. The Server can be installed prettymuch anywhere, therfore the App can be installed in a local network or on the Internet.

## Usage
Infinity Feedback uses keys to identify a session. Those keys can be created in the React Webapp or in its PHP predecessor. The keys have to be pasted into the plugin as well as into the apps.

The Plugin is pretty straight forward. It captures OBS interaction and sends the data to the server. It is possible to send P2P messages to the Clients. Those won't be stored.

TODO: add Client desription

## Installation
### Server
The server can be cloned directly from this repo. Please change the `.env` file accordingly. 
You will need a mysql Database with the following Table Structure.

```
CREATE TABLE `church_streams` (
  `id` bigint(20) NOT NULL AUTO_INCREMENT,
  `start` timestamp NOT NULL DEFAULT current_timestamp() ON UPDATE current_timestamp(),
  `key_id` bigint(20) NOT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=27 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci

CREATE TABLE `church_scenes` (
  `id` bigint(20) NOT NULL AUTO_INCREMENT,
  `name` varchar(255) COLLATE utf8mb4_unicode_ci NOT NULL,
  `key_id` bigint(20) NOT NULL,
  `active` int(11) NOT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=2791 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci

CREATE TABLE `church_keys` (
  `id` bigint(20) NOT NULL AUTO_INCREMENT,
  `key` varchar(255) COLLATE utf8mb4_unicode_ci NOT NULL,
  `name` varchar(255) COLLATE utf8mb4_unicode_ci NOT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=11 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci

```

To install the Server move to the servers directory and run `npm install`. After that you can launch the server with `npm start`. To keep the server up, I recommend using `forever`. You can install that with `npm install -g forever` and launch the server with `forever start index.js`.  


### Plugin
The Plugin consists of a OBS Custom Browser Dock and a Python Script. Both must be added to your OBS installation. Please note, that in order to run a Python Script you need to install Python and add the Python Path to OBS. OBS currently only supports Python v3.6. The Plugin can be installed via the `installer.bat`. This Program will leave you with two paths. Those are the files that need to be integrated in OBS.
