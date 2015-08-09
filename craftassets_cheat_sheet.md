## craft.assets


```
{# craft.assets tag #}
{% set assets = craft.assets.first() %}
{% set assets = craft.assets.last() %}
{% set assets = craft.assets.find() %}
{% set assets = craft.assets.ids() %}
{% set assets = craft.assets.total() %}
{% set assets = craft.assets.find({
  id:         id,
  fixedOrder: true OR false,
  filename:   'fileName.jpg',
  folderId:   id,
  height:     200,
  offset:     number,
  size:       1000,
  sourceId:   id,
  width:      200,
  kind:       AssetFileModel, EntryModel, UserModel, 
              CategoryModel, TagModel,
              elementId,
              [ arrayOfModels, arrayOfModels, arrayOfModels ],
              [ 1, 2, 3 ]
              craft.assets, craft.categories, craft.entries,
              craft.tags, craft.users
  relatedTo:  AssetFileModel, EntryModel, UserModel, 
              CategoryModel, TagModel,
              elementId,
              [ arrayOfModels, arrayOfModels, arrayOfModels ],
              [ 1, 2, 3 ]
              craft.assets, craft.categories, craft.entries,
              craft.tags, craft.users
  order:      'title,id,sourceId,folderId,filename,kind,width,height,size desc',
  limit:      'number',
  indexBy:    'id,title',
  search:     'salty dog'           containing both "salty" and "dog"
              '"salty dog"'         containing the exact phrase "salty dog"
              'salty OR dog'        containing either "salty" or "dog" (or both)
              'salty -dog'          containing "salty" but not "dog"
              'body:salty'          containing "salty" in the "body" field
              'body:salty'          body:dog containing both "salty" and "dog" 
                                    in the "body" field
              'body:*'              containing anything within the "body" field
              'salty locale:en_us'  containing "salty" in the locale "en_us"
              'salt*'               containing a word that begins with "salt"
              '*ty'                 containing a word that ends with "ty"
              '*alt*'               containing a word that contains "alt",
}) %}
{% for asset in assets %}
  {# AssetFileModel #}
  {# Properties #}
  {{ asset.dateCreated }}
  {{ asset.dateUpdated }}
  {{ asset.filename }}
  {{ asset.folderId }}
  {{ asset.height }}
  {{ asset.id }}  
  {{ asset.kind }}
  {{ asset.size }}
  {{ asset.sourceId }}
  {{ asset.url }}
  {{ asset.width }}
  {# Methods #}
  {{ asset.getChildren( fields ) }}
  {{ asset.getParents( fields ) }}
  {{ asset.getHeight( fields ) }}
  {{ asset.getWidth( fields ) }}
  {{ asset.getUrl( fields ) }}
  {% set prev = asset.getPrev( params ) %}
  {% set next = asset.getNext( params ) %}
  {% if prev %} <a href="/link-to-prev-asset">{{ prev.title }}</a> {% endif %}
  {% if next %} <a href="/link-to-next-asset">{{ next.title }}</a> {% endif %}
{% endfor %}}
```