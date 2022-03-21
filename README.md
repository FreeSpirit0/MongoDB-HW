# MongoDB-HW
Script for creating and doing some queries.


```
use HW8
```
![image](https://user-images.githubusercontent.com/67256736/159283871-04664aac-9391-4d7e-a539-28c78fa77196.png)

Create collection in MongoDB Compass  
![image](https://user-images.githubusercontent.com/67256736/159284047-2ef5f92e-9f7e-495d-b99c-66bcc86472e9.png)
  
Insert data  
```SQL
db.Student.insertMany([
  {"name":"Ramesh","subject":"maths","marks":87},
  {"name":"Ramesh","subject":"english","marks":59},
  {"name":"Ramesh","subject":"science","marks":77},
  {"name":"Rav","subject":"maths","marks":62},
  {"name":"Rav","subject":"english","marks":83},
  {"name":"Rav","subject":"science","marks":71},
  {"name":"Alison","subject":"maths","marks":84},
  {"name":"Alison","subject":"english","marks":82},
  {"name":"Alison","subject":"science","marks":86},
  {"name":"Steve","subject":"maths","marks":81},
  {"name":"Steve","subject":"english","marks":89},
  {"name":"Steve","subject":"science","marks":77},
  {"name":"Jan","subject":"english","marks":0,"reason":"absent"}
])
```  
![image](https://user-images.githubusercontent.com/67256736/159284495-fa10f079-c69c-4773-ab9b-127af876516a.png)  


Find the total marks for each student across all subjects.
```SQL
db.Student.aggregate([{$group:{_id:"$name",totalMarks:{$sum:"$marks"}}}])
```
![image](https://user-images.githubusercontent.com/67256736/159285900-96c8fa7f-66b3-4533-9fe8-9c8138f3e015.png)  

Find the maximum marks scored in each subject.
```SQL
db.Student.aggregate([{$group:{_id:"$subject",maxMarks:{$max:"$marks"}}}])
```
![image](https://user-images.githubusercontent.com/67256736/159286264-15c1acfa-432f-4311-b23b-a3aadb969fe2.png)  

Find the minimum marks scored by each student.
```SQL
db.Student.aggregate([{$group:{_id:"$name",minMarks:{$min:"$marks"}}}])
```
![image](https://user-images.githubusercontent.com/67256736/159286551-3ab3c776-d401-47e8-8e84-7b5b7eadeec5.png)  

Find the top two subjects based on average marks.
```SQL
db.Student.aggregate([{$group:{_id:"$subject", averageMarks:{$avg:"$marks"}}}, {$sort: {averageMarks: -1}}, {$limit: 2}])
```
![image](https://user-images.githubusercontent.com/67256736/159288740-7da15e4a-29ed-4cd1-b4fc-3f6f6ae6ccea.png)

