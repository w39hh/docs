.. Project-FiFo documentation master file, created by
   Heinz N. Gies on Fri Aug 15 03:25:49 2014.

**************
API - Datasets
**************

.. http:get:: /datasets

   Lists all datasets.

   **Related permissions**

      cloud -> datasets -> list

   **Example request**:

      .. sourcecode:: http
  
        GET /datasets HTTP/1.1
        host: cloud.project-fifo.net
        accept: applicaiton/json
        x-snarl-token: 1b2230af-03bb-4bf7-ab49-86fab503bf16

   **Example response**:

      .. sourcecode:: http
  
       HTTP/1.1 200 OK
       vary: Accept
       content-type: application/json
       x-snarl-token: 1b2230af-03bb-4bf7-ab49-86fab503bf16
  
       ["b7c658e0-2ddb-46dd-8973-4a59ffc9957e"]


   :reqheader accept: the accepted encoding, valid is ``application/json``
   :reqheader x-snarl-token: the snarl token for this session
   :reqheader x-full-list: true - to get a full list instead of UUIDs
   :reqheader x-full-fields: fields to include in the full list - please see: :http:get:`/datasets/(uuid:dataset)`
   :resheader content-type: the returned datatype, usually ``application/json``
   :resheader x-snarl-token: the snarl token for this session
   
   :status 200: the dataset list is returned
   :status 403: user is not authoriyed
   :status 503: one or more subsystems could not be reached

.. http:post:: /datasets

   Imports a dataset from dsapi endpoint.

   **Related permissions**

    cloud -> datasets -> import

.. http:get:: /datasets/(uuid:dataset)

   Returns dataset with given *uuid*.

   **Related permissions**

      datasets -> UUID -> get

   **Example request**:

      .. sourcecode:: http
  
       GET /datasets/b7c658e0-2ddb-46dd-8973-4a59ffc9957e HTTP/1.1
       host: cloud.project-fifo.net
       accept: applicaiton/json
       x-snarl-token: 1b2230af-03bb-4bf7-ab49-86fab503bf16

   **Example response**:

      .. sourcecode:: http
  
       HTTP/1.1 200 OK
       vary: Accept
       content-type: application/json
       x-snarl-token: 1b2230af-03bb-4bf7-ab49-86fab503bf16
  
       {
        "uuid": "b7c658e0-2ddb-46dd-8973-4a59ffc9957e",
        "type": "kvm",
        "status": "imported",
        "imported": 1,
        "requirements": [],
        "metadata": {},
        "description": "",
        "disk_driver": "virtio",
        "homepage": "",
        "image_size": 12345,
        "name": "example",
        "networks": {"net0":"public"},
        "nic_driver": "virtio",
        "os": "linux",
        "users": ["root", "admin"],
        "version": "0.1.0"
       }

   :reqheader accept: the accepted encoding, valid is ``application/json``
   :reqheader x-snarl-token: the snarl token for this session
   :resheader content-type: the returned datatype, usually ``application/json``
   :resheader x-snarl-token: the snarl token for this session

   :status 200: the dataset information is returned
   :status 403: user is not authoriyed
   :status 404: the dataset was not found
   :status 503: one or more subsystems could not be reached

   :>json string UUID: UUID of the dataset
   :>json string type: type of the dataset
   :>json string status: import status of the dataset (pending / importing / imported / failed)
   :>json integer imported: percentage of dataset imported (0 .. 1)
   :>json array requirements: requirements for the dataset
   :>json object metadata: metadate associated witht he dataset
   :>json string description: description of the dater set
   :>json string disk_driver: disk driver to use for kvms
   :>json string homepage: homepage of the dataset
   :>json integer image_size: size of the image
   :>json string name: name of the dataset
   :>json object networks: networks/interfaces the dataset requires
   :>json string nic_driver: nic driver to use for kvms
   :>json string os: dataset OS
   :>json array users: users provided by the dataset
   :>json string version: version # of the dataset

.. http:put:: /datasets/(uuid:dataset)

   Cahnges parameters of dataset with given *uuid*.

   **Related permissions**

      datasets -> UUID -> edit

.. http:post:: /datasets/(uuid:dataset)

   Imports a manifest for dataset with given *uuid*.

   **Related permissions**

      datasets -> UUID -> create

.. http:delete:: /datasets/(uuid:dataset)

   Deletes dataset with given *uuid* if not in use.

   **Related permissions**

      datasets -> UUID -> delete

   **Example request**:

      .. sourcecode:: http
  
       DELETE /datasets/b7c658e0-2ddb-46dd-8973-4a59ffc9957e HTTP/1.1
       host: cloud.project-fifo.net

   **Example response**:

      .. sourcecode:: http
  
       HTTP/1.1 204 No Content

   :reqheader x-snarl-token: the snarl token for this session
   :resheader x-snarl-token: the snarl token for this session

   :status 204: the dataset was successfully deleted
   :status 404: the dataset was not found
   :status 503: one or more subsystems could not be reached


.. http:get:: /datasets/(uuid:dataset)/dataset.gz

   Exports *zvol* for dataset with given *uuid*.

   **Related permissions**

      datasets -> UUID -> export

.. http:put:: /datasets/(uuid:dataset)/dataset.gz

   Imports *zvol* for dataset with given *uuid*.

   **Related permissions**

      datasets -> UUID -> create

.. http:put:: /datasets/(uuid:dataset)/metadata[/...]

   Sets a metadata key for dataset with given *uuid*.

   **Related permissions**

      datasets -> UUID -> edit


.. http:delete:: /datasets/(uuid:dataset)/metadata/...

   Removes a metadata key for dataset with given *uuid*.

   **Related permissions**

      datasets -> UUID -> edit

   **Example request**:

      .. sourcecode:: http
  
       DELETE /datasets/b7c658e0-2ddb-46dd-8973-4a59ffc9957e/metadata/(path:metadata) HTTP/1.1
       host: cloud.project-fifo.net

   **Example response**:

      .. sourcecode:: http
  
       HTTP/1.1 204 No Content

   :reqheader x-snarl-token: the snarl token for this session
   :resheader x-snarl-token: the snarl token for this session

   :status 204: the metadata key was successfully deleted from the dataset
   :status 404: the metadata key was not found
   :status 503: one or more subsystems could not be reached