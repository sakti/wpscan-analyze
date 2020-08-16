# wpscan-analyze

Analyzes wpscan json output and checks for vulnerabilities

[![Linux and macOS Build Status](https://travis-ci.org/lukaspustina/wpscan-analyze.svg?branch=master)](https://travis-ci.org/lukaspustina/wpscan-analyze) [![codecov](https://codecov.io/gh/lukaspustina/wpscan-analyze/branch/master/graph/badge.svg)](https://codecov.io/gh/lukaspustina/wpscan-analyze) [![GitHub release](https://img.shields.io/github/release/lukaspustina/wpscan-analyze.svg)](https://github.com/lukaspustina/wpscan-analyze/releases) [![](https://img.shields.io/crates/v/wpscan-analyze.svg)](https://crates.io/crates/wpscan-analyze) [![MIT licensed](https://img.shields.io/badge/license-MIT-blue.svg?label=License)](./LICENSE)

[wpscan](https://wpscan.org) checks WordPress installation for outdated versions, plugins, and themes. `wpscan-analyze` analyses `wpscan`'s JSON output and signals results via exit status, JSON and human readable output.


## Basic Usage

`wpscan-analyze` needs an input file in JSON format generated by a run of `wpscan` against a WordPress installation.

### Run wpscan

`wpscan --url https://lukas.pustina.de --update --output wpscan.json --format json`

### Run wpscan-analyze

```bash
> wpscan-analyze -f wpscan.json
wpscan-analyze version=0.0.2, log level=Level(Warn)
+--------------------------+---------+---------------+--------------------+------------+------------+
| Component                | Version | Version State | Vulnerabilities    | Processing | Result     |
+--------------------------+---------+---------------+--------------------+------------+------------+
| WordPress                | 4.9.10  |    Latest     | No vulnerabilities |     Ok     |     Ok     |
| Main Theme               | 3.2.1   |    Latest     | No vulnerabilities |     Ok     |     Ok     |
| Plugin: wp-super-cache   | 1.6.3   |   Outdated    | No vulnerabilities |     Ok     |  Outdated  |
| Plugin: wp-super-cache   | -       |    Unknown    | No vulnerabilities |     Ok     |  Unknown   |
| Plugin: jm-twitter-cards | 9.4     |   Outdated    | No vulnerabilities |     Ok     |  Outdated  |
+--------------------------+---------+---------------+--------------------+------------+------------+
Analyzer result summary: outdated=2, unknown=1, vulnerabilities=1, failed=0
```

#### Exit codes
```
> echo $?
11
```

Ok => 0  
Error => 1 or other  
Vulnerable => 11  
Outdated => 12  
Failed => 13  
Unknown => 14  

### Help

`man 1 wpscan-analyze`

## Installation

### Ubuntu [x86_64]

Please add my [PackageCloud](https://packagecloud.io/lukaspustina/opensource) open source repository and install `wpscan-analyze` via apt.

```bash
curl -s https://packagecloud.io/install/repositories/lukaspustina/opensource/script.deb.sh | sudo bash
sudo apt-get install wpscan-analyze
```

### Install script

**Simply run:**  
```bash
curl -s https://raw.githubusercontent.com/lukaspustina/wpscan-analyze/master/install.sh | sh
```
The script will ask you if you want to install `wpscan-analyzer` from source OR from binaries from [release page](https://github.com/lukaspustina/wpscan-analyze/releases) (Linux binary is compilied with Ubuntu). 

If you don't use Ubuntu linux or MacOs , you'll probably have to build the software from source.  
If you use a non x86_64 processor, you'll have to build the software from source.

### Docker

Please install [docker](https://docs.docker.com/get-docker/) and run:

```bash
git clone https://github.com/lukaspustina/wpscan-analyze
cd wpscan-analyze
docker image build -t wpscan-analyze .
```

Adjust volume mapping as your convinience.  
For exemple, with relative paths, run it with: 

```bash
docker run -it -v "$(pwd):/wpscan-analyze/" wpscan-analyze -f wpscan.json
```

Or share a temp dir:

```bash
docker run -it -v "/tmp/:/tmp/" wpscan-analyze -f /tmp/wpscan.json
```

## Postcardware

You're free to use `wpscan-analyze`. If you find it useful, I would highly appreciate you sending me a postcard from your hometown mentioning how you use `wpscan-analyze`. My work address is

```
Lukas Pustina
CenterDevice GmbH
Rheinwerkallee 3
53227 Bonn
German
