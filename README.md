Mongoose Cheatsheet
====================

## Initialize

```coffeescript
mongoose = require("mongoose")
mongoose.connect("localhost/test")
```

## Schema: 
```coffeescript
# Setup schema

schemaObject = 
	name:"String"
schemaOptions =
	strict:false
	# collection: mongodbCollectionName
	
schema = mongoose.Schema(schemaObject,schemaOptions)

# Static Methods
schema.statics "methodName",(callback)->
	this.find({name: name}, callback)

# Instance Methods
schema.methods.findSimilarTypes = (callback)->
	this.model('Animal').find({ type: this.type }, callback)


```

## Model

```
# Setup model
Model = mongoose.model("CollectionName",schema)

# Initialize a model:
model = new Model(key:"value") 
```

## CRUD

```coffeescript
# Create: 
model.save (err,data)-> 
	# Do Something

# Read: 
model.find {### Arguments ###},(err,data)-> 
	# Do Something

# Get ObjectId: 
id = mongoose.Types.ObjectId(idString)

# Update: 
Model.findByIdAndUpdate id,object,(err,data)-> 
	# Do Something 

# Delete: 
Model.findByIdAndRemove id,(err,data)-> 
	# Do Something 
```

## Express Restful Example
```coffeescript
base ?= "/restapi"
app.delete "#{base}/:id",(req,res)->
	Model.findByIdAndRemove req.params?.id,(err,data)->
		res.json(data)
app.post "#{base}/:id",(req,res)->
	Model.findByIdAndUpdate req.params?.id, req?.body, (err,data)->
		res.json(data)
app.post "#{base}",(req,res)->
	model = new Model(req.body)
	model.save (err,data)->
		unless err then res.json data
app.get "#{base}",(req,res)->
	Model.select("-password").find({}).sort("-id").exec(err,data)->
		res.json data
```
