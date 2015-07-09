# OcraElasticSearch theory of operation

OcraElasticSearch provides basic logic to store POPO (Plain Old PHP Objects) into an
ElasticSearch type via listeners (for configured objects).

## Saving ElasticSearch documents from POPO

There's two approaches to store documents via ElasticSearch:

 1. Get an `OcraElasticSearch\Manager\ManagerInterface` instance
 2. Use the manager to save a document

Or

 1. Get an `OcraElasticSearch\Listener\ObjectSynchronizerInterface` and bind it to
    an event manager of a `Doctrine\Common\Persistence\ObjectManager` and to an
    `OcraElasticSearch\Manager\ManagerInterface`
 2. Persist objects via the connected `Doctrine\Common\Persistence\ObjectManager`

## Loading ElasticSearch documents

To load documents from ElasticSearch you can either:

 1. Get an `OcraElasticSearch\Repository\ElasticaTypeRepository`
 2. Call `$repository->matching($criteria);` with a `Doctrine\Common\Collections\Criteria`
    instance
 3. Retrieve a `Doctrine\Common\Collections\Collection` containing `Elastica\Document` objects

Or

 1. Get an `OcraElasticSearch\Repository\ObjectManagerBackedRepository`
 2. Call `$repository->matching($criteria);` with a `Doctrine\Common\Collections\Criteria`
    instance
 3. Retrieve a `Doctrine\Common\Collections\Collection` containing POPO objects managed
    by a `Doctrine\Common\Persistence\ObjectManager`

## Wrapping it up

Here is a pseudo-UML graph of the current architecture:

![OcraElasticSearch Architecture](http://yuml.me/e77eebb4.svg)

<!--
YUML syntax

[Client Application{bg:red}]reads/writes->[Doctrine.Common.Persistence.ObjectManager{bg:orange}],
[Client Application{bg:red}]reads->[OcraElasticSearch.Repository.ElasticaTypeRepository{bg:green}],
[Client Application{bg:red}]reads->[OcraElasticSearch.Repository.ObjectManagerBackedRepository{bg:green}],
[OcraElasticSearch.Manager.ManagerInterface{bg:green}]writes->[Elastica.Type{bg:blue}],
[OcraElasticSearch.Repository.ElasticaTypeRepository{bg:green}]reads->[Elastica.Type{bg:blue}],
[OcraElasticSearch.Repository.ObjectManagerBackedRepository{bg:green}]reads->[OcraElasticSearch.Repository.ElasticaTypeRepository{bg:green}],
[OcraElasticSearch.Repository.ObjectManagerBackedRepository{bg:green}]reads->[Doctrine.Common.Persistence.ObjectManager{bg:orange}],
[OcraElasticSearch.Listener.ObjectSynchronizerInterface{bg:green}]listens->[Doctrine.Common.Persistence.ObjectManager{bg:orange}],
[OcraElasticSearch.Listener.ObjectSynchronizerInterface{bg:green}]writes->[OcraElasticSearch.Manager.ManagerInterface{bg:green}],
[OcraElasticSearch.Manager.ManagerInterface{bg:green}]consumes->[OcraElasticSearch.Serializer.IdentifierExtractorInterface{bg:green}],
[OcraElasticSearch.Manager.ManagerInterface{bg:green}]consumes->[OcraElasticSearch.Serializer.SerializerInterface{bg:green}],
-->
