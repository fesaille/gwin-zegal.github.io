# Aggregation framework

<img src='https://upload.wikimedia.org/wikipedia/commons/9/93/MongoDB_Logo.svg' class='titleLogo' alt='logo'/>


## Selection stage

### **`$match`** - filtering documents 

!!! Code
	```py3
	{ $match: { <query> } }
	```

- a `$match` may contain a `$text` query operator, but it must be the first in the pipeline
- `$match` should come early in the pipeline
- `$where` can not be used with `$match`
- `$match` uses the same syntax as `find()`

### **`$project`** - shaping document

{ $project: { <specification(s)> } }

- specify fields to be retained
- `_id` must be explicitly removed
- let add new fields or reassign values
- can be used as many times as required in an aggregation pipeline

### **`$addFields`**: add transformation fields in the document

### **`$geoNear`**: filtering	 documents

## Cursor-like stages

### **`$limit`**: limit

### **`$skip`**: limit

### **`$count`**: limit

### **`$sort`**: limit

### **`$sample`**: limit

## Group stage

### **`$group`**: limit
