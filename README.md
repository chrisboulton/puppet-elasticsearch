# puppet-elasticsearch

A puppet module for managing elasticsearch nodes

http://www.elasticsearch.org/

[![Build Status](https://travis-ci.org/electrical/puppet-elasticsearch.png?branch=master)](https://travis-ci.org/electrical/puppet-elasticsearch)

## Usage

Installation, make sure service is running and will be started at boot time:

     class { 'elasticsearch': }

Removal/decommissioning:

     class { 'elasticsearch':
       ensure => 'absent',
     }

Install everything but disable service(s) afterwards:

     class { 'elasticsearch':
       status => 'disabled',
     }

For the config variable a hash needs to be passed:

     class { 'elasticsearch':
       config                   => {
         'node'                 => {
           'name'               => 'elasticsearch001'
         },
         'index'                => {
           'number_of_replicas' => '0',
           'number_of_shards'   => '5'
         },
         'network'              => {
           'host'               => $::ipaddress
         }
       }
     }

## Manage templates

### Add a new template

     elasticsearch::template { 'templatename':
       file => 'puppet:///path/to/template.json'
     }

### Delete a template

     elasticsearch::template { 'templatename':
       delete => true
     }

### Replace a template

     elasticsearch::template { 'templatename':
       file    => 'puppet:///path/to/template.json',
       replace => true
     }

### Host

  Default it uses localhost:9200 as host. you can change this with the 'host' and 'port' variables

     elasticsearch::template { 'templatename':
       host => $::ipaddress,
       port => 9200
     }
