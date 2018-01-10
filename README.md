# MySQL Java Connector module for Puppet

[![Build Status](https://travis-ci.org/voxpupuli/puppet-mysql_java_connector.png?branch=master)](https://travis-ci.org/voxpupuli/puppet-mysql_java_connector)
[![Code Coverage](https://coveralls.io/repos/github/voxpupuli/puppet-mysql_java_connector/badge.svg?branch=master)](https://coveralls.io/github/voxpupuli/puppet-mysql_java_connector)
[![Puppet Forge](https://img.shields.io/puppetforge/v/puppet/mysql_java_connector.svg)](https://forge.puppetlabs.com/puppet/mysql_java_connector)
[![Puppet Forge - downloads](https://img.shields.io/puppetforge/dt/puppet/mysql_java_connector.svg)](https://forge.puppetlabs.com/puppet/mysql_java_connector)
[![Puppet Forge - endorsement](https://img.shields.io/puppetforge/e/puppet/mysql_java_connector.svg)](https://forge.puppetlabs.com/puppet/mysql_java_connector)
[![Puppet Forge - scores](https://img.shields.io/puppetforge/f/puppet/mysql_java_connector.svg)](https://forge.puppetlabs.com/puppet/mysql_java_connector)

#### Table of Contents

[![Build Status](https://travis-ci.org/voxpupuli/puppet-mysql_java_connector.svg?branch=master)](https://travis-ci.org/voxpupuli/puppet-mysql_java_connector)

1. [Overview](#overview)
1. [Module Description - What the module does and why it is useful](#module-description)
1. [Setup - The basics of getting started with mysql_java_connector](#setup)
    * [What mysql_java_connector affects](#what-mysql_java_connector-affects)
    * [Beginning with mysql_java_connector](#beginning-with-mysql_java_connector)
1. [Usage - Configuration options and additional functionality](#usage)
1. [Reference - An under-the-hood peek at what the module is doing and how](#reference)
1. [Limitations - OS compatibility, etc.](#limitations)
1. [Development - Guide for contributing to the module](#development)

## Overview

This module installs the upstream MySQL Java Connector (Connector/J).

## Module Description

Installs the upstream MySQL Java Connector (Connector/J). This is often required
as many operating systems either ship outdated or broken versions by default.

## Setup

### What mysql_java_connector affects

* Installs to /opt/MySQL-connector directory.
* Creates file /opt/MySQL-connector/latest/mysql-connector-java-VERSION-bin.jar

### Beginning with mysql_java_connector

```puppet
  include ::mysql_java_connector
```

## Usage

Create soft links to the mysql connector for use with applications:

```puppet
  class { 'mysql_java_connector':
    links  => [ '/opt/tomcat_app/lib', '/opt/jboss_app/lib' ]
  }
```

Most useful available parameters:

```puppet
  class { 'mysql_java_connector':
    links       => [ '/opt/tomcat_app/lib', '/opt/jboss_app/lib' ],
    version     => '4.99.111',
    installdir  => '/opt/custom',
    downloadurl => 'http://example.co.za',
  }
```

## Reference

### Classes

#### Public Classes

* `mysql_java_connector`: Main class, manages the installation.

#### Private Classes

* `mysql_java_connector::install`: Installs mysql_java_connector binary.

#### Private Definitions

* `mysql_java_connector::links`: Creates softlinks to application directories
  of the mysql_java_connector binary.

### Parameters

#### `ensure`

Ensure the MySQL connector is installed. Defaults to present.

#### `version`

Specifies the version of MySQL Java Connector you would like installed. Defaults
to '5.1.40'

#### `product`

Product name, defaults to 'mysql-connector-java'

#### `format`

The default file format of the MySQL Java Connector install file, defaults to tar.gz

#### `installdir`

Installation directory of the MySQL connector. Defaults to '/opt/MySQL-connector'

#### `downloadurl`

Defaults to `http://dev.mysql.com/Downloads/Connector-J`

#### `proxy_server`

Optional proxy server to use, with port number if needed. ie: https://example.com:8080.

#### `proxy_type`

Proxy server type (none|http|https|ftp)

#### `links`

Directories to create softlinks to mysql connector file for use within
applications. Defaults to an empty array. Must be an array.

## Limitations

This should be compatible with Linux distributions. Tested on:

* CentOS 6/7
* RedHat 6/7
* Ubuntu 12.04/14.04
* Debian 7

## Development

See CONTRIBUTING.md
