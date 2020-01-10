from pymongo import MongoClient
import dronekit

#quadcopter object
telemetry_serial = 'COM6'
baud_rate = 57600
quad = None
lat1 = 0
lon1 = 0
try:
    quad = dronekit.connect(ip='COM6', baud=57600)
except:
    pass
 
#connect to the MongoDB.

conn = MongoClient('mongodb+srv://root:root@cluster0-tbodi.mongodb.net/test?retryWrites=true&w=majority',27017)

#Access the testdb database and the emp collection.
db = conn.test.drogos
 
#create a dictionary to hold emp details.




 
#create dictionary. 11.0102 76.9504
emp_rec = {}
 
#set flag variable.
flag = True

#loop for data input.
while (flag):
   #ask for input.
##   emp_name,emp_addr,emp_id = input("Enter emp name, address and id: ").split(',')
   #place values in dictionary.
##   emp_rec = {'name':emp_name,'latitude1':emp_addr,'longitude1':emp_id}
   #insert the record

            
    if quad != None:
        cf = False 
        cg = False
       
        if lat1 != quad.location.global_relative_frame.lat:
            lat1 = quad.location.global_relative_frame.lat
            cf = True
            print(quad.location.global_relative_frame.lat)
        if lon1 != quad.location.global_relative_frame.lon:
            lon1 = quad.location.global_relative_frame.lon
            cg = True
        if (cf,cg== True, True):
            ret = db.update_one(
    {"name": "1"},
    {
        "$set": {
            "latitude1": lat1, "longitude1":lon1
        },

    }
)
            print (lat1,lon1)
   # else:
    #    print(lat1,lon1)
     ##   print('Transmission not established')
   #Ask from user if he wants to continue to insert more documents?
##   flag = input('Enter another record? ')
##   if (flag[0].upper() == 'N'):
##      flag = False
 
#find all documents.
##ret = db.find()
## 
##print()
##print('+-+-+-+-+-+-+-+-+-+-+-+-+-+-')
## 
###display documents from collection.
##for record in ret:
###print out the document.
##    print(record['name'] + ',',record['latitude1'] + ',',record['longitude1'])
## 
##print()
 
#close the conn to MongoDB


