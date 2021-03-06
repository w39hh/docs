.. Project-FiFo documentation master file, created by
   Heinz N. Gies on Fri Aug 15 03:25:49 2014.

*******************
API - Organizations
*******************

.. http:get:: /orgs

   Lists all organizations.

   **Related permissions**

      cloud -> orgs -> list

   **Example request**:

   .. sourcecode:: http
  
     GET /orgs HTTP/1.1
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
   :reqheader x-full-fields: fields to include in the full list - please see: :http:get:`/orgs/(uuid:org)`
   :resheader content-type: the returned datatype, usually ``application/json``
   :resheader x-snarl-token: the snarl token for this session
   
   :status 200: the orgs list is returned
   :status 403: user is not authoriyed
   :status 503: one or more subsystems could not be reached

____


.. http:post:: /orgs

   Creates a new organization.

   **Related permissions**

      cloud -> orgs -> create

.. todo::
    
  Example Requests & Responses still missing.

____


.. http:get:: /orgs/(uuid:org)

   Returns organization with given *uuid*.

   **Related permissions**

      orgs -> UUID -> get

   **Example request**:

   .. sourcecode:: http
  
     GET /orgs/b7c658e0-2ddb-46dd-8973-4a59ffc9957e HTTP/1.1
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
     "name": "Project-FiFo",
     "uuid": "b7c658e0-2ddb-46dd-8973-4a59ffc9957e",
     "triggers": {},
     "metadata": {}
     }

   :reqheader accept: the accepted encoding, valid is ``application/json``
   :reqheader x-snarl-token: the snarl token for this session
   :resheader content-type: the returned datatype, usually ``application/json``
   :resheader x-snarl-token: the snarl token for this session

   :status 200: the organization's information is returned
   :status 403: user is not authoriyed
   :status 404: the organization was not found
   :status 503: one or more subsystems could not be reached

   :>json string name: name of the organization
   :>json string uuid: UUID of the organization
   :>json object triggers: list of the organization's triggers
   :>json object metadata: metadata associated with the organization

____


.. http:delete:: /orgs/(uuid:orgs)

   Deletes organization with given *uuid*.

   **Related permissions**

      orgs -> UUID -> delete

   **Example request**:

   .. sourcecode:: http
  
     DELETE /orgs/b7c658e0-2ddb-46dd-8973-4a59ffc9957e HTTP/1.1
     host: cloud.project-fifo.net

   **Example response**:

   .. sourcecode:: http
  
     HTTP/1.1 204 No Content

   :reqheader x-snarl-token: the snarl token for this session
   :resheader x-snarl-token: the snarl token for this session

   :status 204: the organization was successfully deleted
   :status 404: the organization was not found
   :status 503: one or more subsystems could not be reached

____


.. http:get:: /orgs/(uuid:org)/triggers

   Lists the organization's triggers.

   **Related permissions**

      orgs -> ID -> get

   **Example request**:

   .. sourcecode:: http

     GET /orgs/b7c658e0-2ddb-46dd-8973-4a59ffc9957e/triggers HTTP/1.1
     host: cloud.project-fifo.net
     accept: applicaiton/json
     x-snarl-token: 1b2230af-03bb-4bf7-ab49-86fab503bf16

   **Example response**:

   .. sourcecode:: http

     HTTP/1.1 200 OK
     vary: Accept
     content-type: application/json
     x-snarl-token: 1b2230af-03bb-4bf7-ab49-86fab503bf16
     
      {}

   :reqheader accept: the accepted encoding, valid is ``application/json``
   :reqheader x-snarl-token: the snarl token for this session
   :resheader content-type: the returned datatype, usually ``application/json``
   :resheader x-snarl-token: the snarl token for this session

   :status 200: the organization's triggers are returned
   :status 404: the triggers were not found
   :status 403: user is not authorized
   :status 503: one or more subsystems could not be reached

   :>json array permissions: list of triggers for the organization

____


.. http:put:: /orgs/(uuid:org)/triggers/(uuid:role)/<permission.../...>

   Adds a new trigger to org with given *uuid*.

   **Related permissions**

      * orgs -> UUID -> edit
      * roles -> ROLE -> grant

.. todo::
    
  Example Requests & Responses still missing.

____


.. http:delete:: /orgs/(uuid:org)/triggers/(uuid:trigger)

   Deletes a trigger from organization with given *uuid*.

   **Related permissions**

      orgs -> UUID -> edit

   **Example request**:

   .. sourcecode:: http
  
     DELETE /orgs/b7c658e0-2ddb-46dd-8973-4a59ffc9957e/triggers/b7c658e0-2ddb-46dd-8973-4a59ffc9957e HTTP/1.1
     host: cloud.project-fifo.net

   **Example response**:

   .. sourcecode:: http
  
     HTTP/1.1 204 No Content

   :reqheader x-snarl-token: the snarl token for this session
   :resheader x-snarl-token: the snarl token for this session

   :status 204: the trigger was successfully deleted from the organization
   :status 404: the trigger was not found for that organization
   :status 503: one or more subsystems could not be reached

____


.. http:put:: /orgs/(uuid:org)/metadata[/...]

   Sets a metadata key for organization with given *uuid*.

   **Related permissions**

      orgs -> UUID -> edit

   **Example request**:

   .. sourcecode:: http

     PUT /api/0.1.0/vms/2ca285a3-05a8-4ca6-befd-78fa994929ab/metadata/jingles HTTP/1.1
     Accept: application/json
     x-snarl-token: d2d685b7-714d-4d28-bb7c-6f80b29da4dd
     Content-Type: application/json

     {"notes":  [{"text":"yap","created_at":"2014-09-13T01:34:03.379Z"}]}

   **Example response**:

   .. sourcecode:: http

     HTTP/1.1 204 No Content
     x-snarl-token: d2d685b7-714d-4d28-bb7c-6f80b29da4dd
     vary: accept

   :reqheader accept: the accepted encoding, alis is ``application/json``
   :reqheader x-snarl-token: the snarl token for this session
   :reqheader content-type: the provided datatype, usually ``application/json``
   :resheader x-snarl-token: the snarl token for this session

   :status 204: no content
   :status 404: the VM could not be found
   :status 403: user is not authorized
   :status 503: one or more subsystems could not be reached

   :>json string <key>: values to store under this key





____


.. http:delete:: /orgs/(uuid:org)/metadata/...

   Removes a key from the metadata for organization with given *uuid*.

   **Related permissions**

     orgs -> UUID -> edit

   **Example request**:

   .. sourcecode:: http
  
     DELETE /orgs/b7c658e0-2ddb-46dd-8973-4a59ffc9957e/metadata/... HTTP/1.1
     host: cloud.project-fifo.net

   **Example response**:

   .. sourcecode:: http
  
     HTTP/1.1 204 No Content

   :reqheader x-snarl-token: the snarl token for this session
   :resheader x-snarl-token: the snarl token for this session

   :status 204: the metadata key was successfully deleted from the organization
   :status 404: the metadata key was was not found for that organization
   :status 503: one or more subsystems could not be reached

