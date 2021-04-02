Enable Datapub apps in your CKAN instance.

Find out about Datapub here - https://github.com/datopian/datapub.

## Installation

This extension requires https://github.com/datopian/ckanext-blob-storage to be enabled as it uses `storage_service_url` for uploading files.

Just follow standard procedure for setting up an extension for the CKAN and add `datapub` into list of the plugins. Note that this extension was developed and tested using version 2.8.

Setup JS modules:

```
sh sync.sh
```

It would:

* git clone the datapub repo (can be any custom repo, by default, it is https://github.com/datopian/datapub)
* install dependencies
* build
* update JS modules in fanstatic

**Note:**

- if you are developing a React app, e.g., custom `datapub` app, you can use the following attributes passed from the `/templates/datapub/snippets/upload_module.html`:

```html
<div id="ResourceEditor"
     data-dataset-id="{{ pkg_name }}"
     data-api="{{ base_url }}"
     data-lfs="{{ h.blob_storage_lfs_url() }}"
     data-auth-token="{{ api_key }}"
     data-organization-id="{{ h.blob_storage_organization_name(pkg_name) }}"
     data-resource-id="{{ resource_id }}">
</div>
```
## CKAN >= 2.9 support

CKAN >= 2.9 uses webassets to manage all the bundles and the tag changed from `resource` to `asset`.

In order to build an `upload_module.html` that runs on CKAN >= 2.9 you can pass `webassets` as third parameter.

Example:

```
sh sync.sh https://github.com/datopian/datapub master webassets
```

This will create an `upload_module.html` like the following one:

```html
{% asset "datapub/datapub-js" %}
{% asset "datapub/datapub-css" %}

<div id="ResourceEditor"
     data-dataset-id="{{ pkg_name }}"
     data-api="{{ base_url }}"
     data-lfs="{{ h.blob_storage_lfs_url() }}"
     data-auth-token="{{ api_key }}"
     data-organization-id="{{ h.blob_storage_organization_name(pkg_name) }}"
     data-resource-id="{{ resource_id }}">
</div>
```