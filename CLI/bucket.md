# Managing Permissions in OCI Bucket with IAM Policies

## Allow a group to manage buckets & objects in Tenancy

<pre><code>Allow Group [GroupName] to Manage buckets in Tenancy 
Allow Group [GroupName] to Manage objects in Tenancy</code></pre>

## Allow a group of users read or write to a particular bucket in a compartment

<pre><code>Allow Group [GroupName] to Read buckets in Compartment [CompartmentName]

Allow Group [GroupName] to Manage objects in Compartment [CompartmentName] Where All {target.bucket.name= '[BucketName]', Any {request.permission= 'OBJECT_CREATE', request.permission='OBJECT_INSPECT'}}</code></pre>

## Allow a group to download from particular bucket

<pre><code>Allow Group [GroupName] to Read buckets in Compartment [CompartmentName]

Allow Group [GroupName] to Read objects in Compartment [CompartmentName] Where target.bucket.name= '[BucketName]'</code></pre>

## Limit write access by bucket tag

<pre><code>Allow Group [GroupName] to Read buckets in Compartment [CompartmentName]

Allow Group [GroupName] to Manage objects in Compartment [CompartmentName] Where All {target.bucket.tag.MyTagNamespace.TagKey= '[TagValue]' , Any {request.permission= 'OBJECT_CREATE' , request.permission= 'OBJECT_INSPECT' }}</code></pre>

## Limit read access by bucket tag

<pre><code>Allow Group [GroupName] to Read buckets in Compartment [CompartmentName]

Allow Group [GroupName] to Read objects in Compartment [CompartmentName] Where target.bucket.tag.MyTagNamespace.TagKey= '[TagValue]'</code></pre>

## Restrict group access to specific buckets by name or pattern

<pre><code>Allow Group [GroupName] to Use buckets in Tenancy Where target.bucket.name= '[BucketName]'

Allow Group [GroupName] to Use buckets in Tenancy Where target.bucket.name=[/BucketPattern\_\*/]</code></pre>

## Restrict group access to Read or write objects in specific buckets

<pre><code>Allow Group [GroupName] to Read buckets in Tenancy

Allow Group [GroupName] to Manage objects in Tenancy Where All {target.bucket.name= '[BucketName]' , Any {request.permission= 'OBJECT_INSPECT' , request.permission= 'OBJECT_READ' }}

Allow Group [GroupName] to Read buckets in Tenancy

Allow Group [GroupName] to Manage objects in Tenancy Where All {target.bucket.name= '[BucketName]' , Any {request.permission= 'OBJECT_INSPECT' , request.permission= 'OBJECT_CREATE' }}</code></pre>

## Restrict group access to Read or write objects in specific buckets based on tags

<pre><code>Allow Group [GroupName] to Read buckets in Tenancy

Allow Group [GroupName] to Manage objects in Tenancy Where All {target.bucket.tag.MyTagNamespace.TagKey= '[TagValue]' , Any {request.permission= 'OBJECT_INSPECT' , request.permission= 'OBJECT_READ' }}

Allow Group [GroupName] to Read buckets in Tenancy

Allow Group [GroupName] to Manage objects in Tenancy Where All {request.principal.group.tag.MyTagNamespace.TagKey=target.bucket.tag.MyTagNamespace.TagKey, Any {request.permission= 'OBJECT_INSPECT' , request.permission= 'OBJECT_CREATE' }}</code></pre>

## Restrict access to Read or write objects or groups of objects by prefix or pattern

<pre><code>Allow Group [GroupName] to Manage objects in Tenancy Where Any {target.object.name = '[ObjectPattern]-\*' , request.operation = 'GetObject' } </code></pre>

## Restrict access to objects by prefix

<pre><code>Allow Group [GroupName] to Manage objects in Tenancy Where All {target.bucket.name = '[BucketName]' , target.object.name = '[ObjectPattern]/\*' }</code></pre>

## Restrict access to a group to Read only forobjects

<pre><code>Allow Group [GroupName] to Manage objects in Tenancy Where All {target.bucket.name = '[BucketName]' , target.object.name = '[ObjectPattern]/\*' , Any{request.permission= 'OBJECT_INSPECT' , request.permission= 'OBJECT_READ' }}</code></pre>

## Restrict access to a particular user to a group of objects by pattern

<pre><code>Allow Any-user to Manage objects in Tenancy Where All {target.bucket.name = '[BucketName]' , target.object.name = '\*.pdf' , request.user.id= '[UserOCID]' }</code></pre>

## Restrict resource access to a particular user

<pre><code>Allow Any-user to Read object-family in Compartment [CompartmentName] Where request.user.id = '[UserOCID]'</code></pre>

## Restrict access to Read or write objects or groups of objects by prefix or pattern

<pre><code>Allow Group [GroupName] to Manage objects in Tenancy Where Any {target.object.name = '[ObjectPattern]-\*' , request.operation = 'GetObject' }</code></pre>

## Restrict access to objects by prefix

<pre><code>Allow Group [GroupName] to Manage objects in Tenancy Where All {target.bucket.name = '[BucketName]' , target.object.name = 'prod/\*' }</code></pre>

## Restrict access to a group to Read only forobjects

<pre><code>Allow Group [GroupName] to Manage objects in Tenancy Where All {target.bucket.name = '[BucketName]' , target.object.name = 'prod/\*' , Any{request.permission= 'OBJECT_INSPECT' , request.permission= 'OBJECT_READ' }}</code></pre>

## Restrict access to a particular user to a group of objects by pattern

<pre><code>Allow Any-user to Manage objects in Tenancy Where All {target.bucket.name = '[BucketName]' , target.object.name = '\*.pdf' , request.user.id= '[UserOCID]' }</code></pre>

## Restrict resource access to a particular user

<pre><code>Allow Any-user to Read object-family in Compartment [CompartmentName] Where request.user.id = '[UserOCID]'</code></pre>

## Restrict access from Allowed IP address (by creating a Network source)

<pre><code>Allow Group [GroupName] to Manage object-family in Tenancy Where request.networkSource.name= '[NetworkSourceName]'</code></pre>

## Prevent delete of buckets & objects

<pre><code>Allow Group [GroupName] to Manage objects in Tenancy Where request.permission != 'OBJECT_DELETE'

Allow Group [GroupName] to Manage buckets in Tenancy Where request.permission != 'BUCKET_DELETE'</code></pre>

## Prevent delete of buckets & objects for specific bucket

<pre><code>Allow Group [GroupName] to Manage objects in Tenancy Where Any {target.bucket.name != '[BucketName]' , All {target.bucket.name= '[BucketName]' , request.permission!= 'OBJECT_DELETE' }}</code></pre>

## Service permission for OLM

<pre><code>Allow Service objectstorage-[RegionIdentifier] to Manage object-family in Compartment [CompartmentName]</code></pre>

## More restrictive permissions

<pre><code>Allow Service objectstorage-[RegionIdentifier] to Manage object-family in Compartment [CompartmentName] Where Any {request.permission='BUCKET_INSPECT', request.permission= 'BUCKET_READ' , request.permission= 'OBJECT_INSPECT' , request.permission= 'OBJECT_UPDATE_TIER' , request.permission= 'OBJECT_DELETE' , request.permission= 'OBJECT_VERSION_DELETE' }</code></pre>

## Source Tenancy Policy statements

<pre><code>Define tenancy DestinationTenancy as [TenancyOCID]

Endorse Group [GroupName] to Manage object-family in Tenancy DestinationTenancy</code></pre>

## Destination Tenancy Policy statements

<pre><code>Define tenancy SourceTenancy as [TenancyOCID]

Define Group [GroupName] as [GroupOCID]

Admit Group [GroupName] of tenancy SourceTenancy to Manage object-family in Tenancy</code></pre>

## More restrictive policy for compartment within Tenancy

<pre><code>Define tenancy SourceTenancy as [TenancyOCID]

Define Group [GroupName] as [GroupOCID]

Admit Group [GroupName] of tenancy SourceTenancy to Manage object-family in Compartment [CompartmentName]</code></pre>

## Allow object storage service to act on behalf of user

<pre><code>Allow Service objectstorage-[RegionIdentifier] to Manage object-family in Compartment [CompartmentName]</code></pre>

## Allow object storage service to use customer keys in encrypted buckets

<pre><code>Allow Service objectstorage-[RegionIdentifier] to Use keys in Tenancy</code></pre>

## Allow object storage service in multiple regions to Use keys

<pre><code>Allow Service objectstorage-[RegionIdentifier1], objectstorage-[RegionIdentifier2] to Use keys in Compartment [CompartmentName]</code></pre>

## Let object storage service in a region use keys

<pre><code>Allow Service objectstorage-[RegionIdentifier] to Use keys in Compartment [CompartmentName] Where target.key.id = '[KeyOCID]'</code></pre>

## Let users access customer data in object storage encrypted with customer managed key in Any region

<pre><code>Allow Group [GroupName] to Manage vaults in Compartment [KeyCompartment]

Allow Group [GroupName] to Manage keys in Compartment [KeyCompartment]

Allow Group [GroupName] to Manage key-delegate in Compartment [KeyCompartment]

Allow Group [GroupName] to Use object-family in Compartment [KeyCompartment]

Allow Any-user to Use keys in Compartment [KeyCompartment] Where All {request.principal.type = 'service' , request.service.name = /objectstorage-\*/}</code></pre>
