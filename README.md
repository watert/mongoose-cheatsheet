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
schema = mongoose.Schema schema,
	strict:false 

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
