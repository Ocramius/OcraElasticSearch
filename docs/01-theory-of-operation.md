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

Here is apseudo-UML graph of the current architecture:

![OcraElasticSearch Architecture](http://yuml.me/6d6d9aa4.svg)

<!--
YUML syntax

[Client Application]reads/writes->[Doctrine.Common.Persistence.ObjectManager],
[Client Application]reads->[OcraElasticSearch.Repository.ElasticaTypeRepository],
[Client Application]reads->[OcraElasticSearch.Repository.ObjectManagerBackedRepository],
[OcraElasticSearch.Manager.ManagerInterface]writes->[Elastica.Type],
[OcraElasticSearch.Repository.ElasticaTypeRepository]reads->[Elastica.Type],
[OcraElasticSearch.Repository.ObjectManagerBackedRepository]reads->[OcraElasticSearch.Repository.ElasticaTypeRepository],
[OcraElasticSearch.Repository.ObjectManagerBackedRepository]reads->[Doctrine.Common.Persistence.ObjectManager],
[OcraElasticSearch.Listener.ObjectSynchronizerInterface]listens->[Doctrine.Common.Persistence.ObjectManager],
[OcraElasticSearch.Listener.ObjectSynchronizerInterface]writes->[OcraElasticSearch.Manager.ManagerInterface],
[OcraElasticSearch.Manager.ManagerInterface]consumes->[OcraElasticSearch.Serializer.IdentifierExtractorInterface],
[OcraElasticSearch.Manager.ManagerInterface]consumes->[OcraElasticSearch.Serializer.SerializerInterface],
-->