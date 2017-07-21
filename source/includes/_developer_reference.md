# Developer Reference

Here's a collection of things that are not well documented, and
workaround we'll have to adopt in our current system for the time being.

## Using the right serializer & adapter

Active Model Serializers have 3 available adapter. Attributes (default),
json, and json api. Since we're adhering to the json api spec, we want
to use the :json_api adapter.

Unfortunately, there's no way to configure this in a non-global way, so
we'll have to pass it in as an option everywhere we want to use it.

```ruby
render json: @investments, each_serializer: ::V2::InvestmentsSerializer, adapter: :json_api
```

For the time being, we'll need to explicity pass in the v2 serializers.

## Limiting what fields are sent back

```ruby
render json: @investments, each_serializer: ::V2::InvestmentsSerializer, adapter: :json_api, fields: { investments: [:titled, :created_at]}
```

There's only one important condition here.

The fields method requires an argument of:

  * `{ obect_type: [:fields, :here] }`

The plural_resource_name needs to correspond with the 'type' of the response. This is so AMS can figure out which json objects in your response you want to limit.

The type is usually the lowercase plural of the model.

  * ex: Investment -> investments.

This can be either a string or a symbol.

## Including other relationships

```ruby
render json: @investments, each_serializer: ::V2::InvestmentsSerializer, include: [:address]
```

Include accepts a straight array of what relationships to include.

  * ex: `include: [:address, :user, :other_relationship`

## Rendering Errors

[Documentation Here](https://github.com/bf4/active_model_serializers/blob/d03db81070d6e18c7191f4986bc0cc60b9dfc8a3/docs/jsonapi/errors.md)

```ruby
resource = Profile.new(name: 'Name 1',
                       description: 'Description 1',
                       comments: 'Comments 1')
resource.errors.add(:name, 'cannot be nil')
resource.errors.add(:name, 'must be longer')
resource.errors.add(:id, 'must be a uuid')

render json: resource, status: 422, adapter: :json_api, serializer: ActiveModel::Serializer::ErrorSerializer
# #=>
#  { :errors =>
#    [
#      { :source => { :pointer => '/data/attributes/name' }, :detail => 'cannot be nil' },
#      { :source => { :pointer => '/data/attributes/name' }, :detail => 'must be longer' },
#      { :source => { :pointer => '/data/attributes/id' }, :detail => 'must be a uuid' }
#    ]
#  }.to_json
```

Direct error document generation

```ruby
options = nil
resource = ModelWithErrors.new
resource.errors.add(:name, 'must be awesome')

serializable_resource = ActiveModel::SerializableResource.new(
  resource, {
    serializer: ActiveModel::Serializer::ErrorSerializer,
    adapter: :json_api
  })
serializable_resource.as_json(options)
# #=>
# {
#   :errors =>
#     [
#       { :source => { :pointer => '/data/attributes/name' }, :detail => 'must be awesome' }
#     ]
# }
```
