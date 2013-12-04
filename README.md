Mongoose Cheatsheet
====================

## Schema:

```coffeescript
modelSchema = {title:"String",content:"String"}
Model = new mongoose.Schema modelSchema,options
```

### Schema Options

```
Model = new mongoose.Schema schema,
	strict:false 
```

## CRUD
ModelDefine: `Model = new mongoose.Schema(modelSchema,options)`
Initialize: ` model = new Model(key:"value") `
Create: `model.save (err,data)-> # Do Something`
Read: `model.find {### Arguments ###},(err,data)-> # Do Something`
Get ObjectId: `id = mongoose.Types.ObjectId(idString)`
Update: `Model.findByIdAndUpdate id,object,(err,data)-> # Do Something `
Delete: `Model.findByIdAndRemove id,(err,data)-> # Do Something `