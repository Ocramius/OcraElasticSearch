[![Build Status](https://secure.travis-ci.org/Ocramius/OcraElasticSearch.png?branch=master)](https://travis-ci.org/Ocramius/OcraElasticSearch) [![Dependency Status](https://www.versioneye.com/package/php--ocramius--ocra-elastic-search/badge.png)](https://www.versioneye.com/package/php--ocramius--ocra-elastic-search)

# OcraElasticSearch Module

**WIP**: this library is under heavy development - use it at your own risk until I tag a stable release!

This library is a small integration layer between Zend Framework 2, Doctrine's Object managers
(ORM/ODM being equally supported) and ElasticSearch.

The basic working concept can be summarized in the following graph:

![OcraElasticSearch basic working concept](http://yuml.me/diagram/scruffy;/class/[ObjectManager]writes->[ElasticSearch], [ElasticSearch]reads->[ObjectManager], [Zend Framework 2]consumes->[ObjectManager], [Zend Framework 2]consumes->[ElasticSearch].svg)
