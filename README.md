<b>Released under a Dual Licensing / JPL</b>
Climate Model Analysis APIs Version 1.0	
=================
JPL has provided a repository of web services for multi-aspect physics-based and phenomenon-oriented phenomenon-oriented climate model performance evaluation and diagnosis through the comprehensive and synergistic use of multiple observational data, reanalysis data, and model outputs. This Climate Model Analysis Project will help you learn the available web services, how to use them, and help you design your climate analytics workflows.

Controllers expect all non-id fields found in the entities (found in /models)
Unless otherwise noted, POST = Create, PUT = Update, DELETE = Delete 

Service URL:
------------
[http://einstein.sv.cmu.edu:9007/climate][1]


Overview:
---------
Currently we are providing APIs in 5 categores:

**Category 1: Manage User**<br/>
   - [Get user by Id](#1)<br/>
   - [Add a user](#2)<br/>
   - [Update a user](#3)<br/>
   - [Delete a user](#4)<br/>

**Category 2: Manage Climate Services**<br/>
   - [Get a climate service by service name](#5)<br/>
   - [Get all climate services](#6)<br/>
   - [Add a climate service](#7)<br/>
   - [Update a climate service by service Id](#8)<br/>
   - [Update a climate service by service name](#9)<br/>
   - [Delete a climate service by service Id](#10)<br/>
   
**Category 3: Manage Service Configuration**<br/>
   - [Get a service configuration by service Id](#11)<br/>
   - [Get all service configurations created by a user](#12)<br/>
   - [Add a service configuration](#13)<br/>
   - [Update a service configuration by service Id](#14)<br/>
   - [Delete a service configuration](#15)<br/>
    
**Category 4: Manage Climate Service Parameters**<br/>
   - [Get all service parameters](#16)<br/>
   - [Get a single pamameter by name](#17)<br/>
   - [Get a single pamameter by Id](#18)<br/>
   - [Add a service parameter](#19)</br>
   - [Update a service parameter by Id](#20)</br>
   - [Update a service parameter by name](#21)</br>
   - [Delete a service parameter](#22)</br>

**Category 5: Manage Service Configuration Item**<br/>
   - [Get a service configuration item by Id](#23)<br/>
   - [Get a service configuration item by a service configuration](#24)<br/>
   - [Get a service configuration item by parameter name](#25)<br/>
   - [Add a service configuration item](#26)<br/>
   - [Update a service configuration item by Id](#27)<br/>
   - [Delete a service configuration item](#28)<br/>
   
Detailed Usages:
----------------
Note: all TimeStamps are in Unix epoch time format to millisecond. Conversion from readable timestamp format to Unix epoch timestamp can be found in http://www.epochconverter.com

####Manage User
1. <a name="1"></a>**GET USER BY ID**
    - **Purpose**: Query a specific user using user's Id.
    - **Method**: GET
    - **URL**: /users/:id
    - **Semantics**: 
        - **id**: Existing user's id.
    - **Sample Usages**:
      - **Sample request**: /users/10
          
      - **Sample result**: {"id":1,"firstName":"John","lastName":"Watson"}
      
      - **Result**: HTTP 200 if successful, HTTP 404 if failed.
      
2. <a name="2"></a>**ADD A USER**
    - **Purpose**: Add a new user to the system.
    - **Method**: POST
    - **URL**: /users/add
    - **Semantics**:  As a POST method, the API cannot be directly executed through a web browser. Instead, it may be executed through Rails, JQuery, Python, BASH, etc.
      - **firstName** (string, not null): First name
      - **lastName** (string, not null): Last name
    - **Sample Usages**:
      - **Sample request**: {"firstName":"John","lastName":"Watson"}
          
      - **Sample result**: 1
               
      - **Result**: HTTP 201 if the new user has been successfully added to the database, with the ID of the newly created object in the response body, HTTP 400 if failed.
      
3. <a name="3"></a>**UPDATE A USER**
    - **Purpose**: Update a user's profile in the system.
    - **Method**: PUT
    - **URL**: /users/update/:id
    - **Semantics**:As a PUT method, the API cannot be directly executed through a web browser.  Instead, it may be executed through Rails, JQuery, Python, BASH, etc.  
      - **id**: A existing user's id.
    - **Sample Usages**:
      - **Sample request**: PUT /users/update/3   {"firstName":"Mary"}
          
      - **Sample result**: Return message "User updated"
      
      - **Result**: HTTP 201 if the user has been successfully updated, HTTP 400 if the id is wrong
           
4. <a name="4"></a>**DELETE A USER**
    - **Purpose**: Delete a user from the system.
    - **Method**: DELETE
    - **URL**: /users/delete/:id
    - **Semantics**: 
        - **id**: Existing user id.
    - **Sample Usages**: 
      - **Sample request**: /users/delete/1
      - **Sample result**: "User is deleted"
      - **Result**: HTTP 201 if the user has been successfully deleted.
  
####Manage Climate Services                
5. <a name="5"></a>**QUERY CLIMATE	SERVICE BY SERVICE NAME**
    - **Purpose**: Query for climate service using service name. If there are multiple services with the same name, all will be returned. 
    - **Method**: GET
    - **URL**: /climate/getClimateService/:name/json
    - **Semantics**:
        - **name**: Existing service name.
    - **Sample Usages**:
      - **Sample json request**: /climate/getClimateService/NightVale/json
      - **Sample json result**: 
			
      - **Result**: HTTP 200 if returned successfully, HTTP 404 if not found.
      
6. <a name="5"></a>**GET A CLIMATE	SERVICE BY ID**
    - **Purpose**: Query for climate service using service ID. Result will be unique.
    - **Method**: GET
    - **URL**: /climate/getClimateService/id/:id
    - **Semantics**:
        - **id**: Id of an existing service.
    - **Sample Usages**:
      - **Sample json request**: /climate/getClimateService/id/30
      - **Sample json result**: 
			 {"id":30,"rootServiceId":1,"user":{"id":31,"firstName":"John","lastName":"Watson"},"name":"testName","purpose":"For testing","url":"http://einstein.sv.cmu.edu:9008/forTesting","scenario":"Used only for testing","createTime":"Feb 26, 2015 4:14:44 PM","versionNo":"1"}
      - **Result**: HTTP 200 if returned successfully, HTTP 404 if not found.
      
6. <a name="6"></a>**GET ALL CLIMATE SERVICE**
    - **Purpose**: Query all climate services.
    - **Method**: GET
    - **URL**: /climate/getAllClimateServices/json
    - **Semantics**:
    
    - **Sample Usages**: 
      - **Sample json request**: /climate/getAllClimateServices/json
      - **Sample json result**: [{"id":33,"rootServiceId":0,"user":{"id":33,"firstName":"John","lastName":"Watson"},"name":"NightVale","purpose":"","url":"","scenario":"","createTime":"Feb 26, 2015 4:20:31 PM","versionNo":""},{"id":34,"rootServiceId":1,"user":{"id":33,"firstName":"John","lastName":"Watson"},"name":"testName","purpose":"For testing","url":"http://einstein.sv.cmu.edu:9008/forTesting","scenario":"Used only for testing","createTime":"Feb 26, 2015 4:20:31 PM","versionNo":"1"}]
[{"climateServiceName":"testName","purpose":"For testing","url":"http://einstein.sv.cmu.edu:9008/forTesting","scenario":"Used only for testing","creatorId":"admin","createTime":"2014/12/18 19:37","versionNo":"1","rootServiceId":"1"}]
      - **Result**: HTTP 200 if successful, HTTP 404 if failed.
      
7. <a name="7"></a>**ADD A CLIMATE SERVICE**
    - **Purpose**: Add a new climate service to the system.
    - **Method**: POST
    - **URL**: /climate/addClimateService
    - **Semantics**: As a POST method, the API cannot be directly executed through a web browser. Instead, it may be executed through Rails, JQuery, Python, BASH, etc.
        - **name** (string, not null): Non existing unique name of the climate service
        - **creatorId** (string, not null): ID of the creator
        - **purpose** (string, optional): Purpose of the climate service
        - **url** (string, optional): Url linked to the configuration page of a certian climate service
        - **scenario** (string, optional): Scenario in which the climate service could be used
      
        - **createTime** (string, default to current time): Time the climate service is created, defaults to current time
        - **versionNo** (double, optional): Version number of the service
        - **rootServiceId** (int, optional): Root service id of the service        
    - **Sample Usages**:
      - **Command Line Example**: 
          1. Prepare input sensor type metadata in a json string:
              - {"creatorId":"24","name":"testName","purpose":"For testing","url":"http://einstein.sv.cmu.edu:9008/forTesting","scenario":"Used only for testing","versionNo":"1","rootServiceId":"1"}
          2. curl -H "Content-Type: application/json" -d @climateService.json "http://einstein.sv.cmu.edu:9008/addClimateService"
      - **Result**: HTTP 201 if the climate service metadata has been successfully added to the database, with the content body returning the ID of the new service as Gson formatted string. HTTP 400 if failed.

8. <a name="8"></a>**UPDATE A CLIMATE SERVICE BY SERVICE ID**
    - **Purpose**: Update a climate service using service id.
    - **Method**: PUT
    - **URL**: /climate/updateClimateService/id/:id
    - **Semantics**: 
        - **id**: Existing service id.
         - **name** (string, not null): Non existing unique name of the climate service
        - **creatorId** (string, not null): ID of the creator
        - **purpose** (string, optional): Purpose of the climate service
        - **url** (string, optional): Url linked to the configuration page of a certian climate service
        - **scenario** (string, optional): Scenario in which the climate service could be used
      
        - **createTime** (string, default to current time): Time the climate service is created, defaults to current time
        - **versionNo** (double, optional): Version number of the service
        - **rootServiceId** (int, optional): Root service id of the service  
    - **Sample Usages**:
      - /climate/updateClimateService/id/20
      - **Result**: HTTP 200 if the climate service has been successfully updated to the database.
      
9. <a name="9"></a>**UPDATE A CLIMATE SERVICE BY SERVICE NAME**
    - **Purpose**: Update a climate service using service name. If there are multiple, only the first climate service is changed. (The above interface is recommended)
    - **Method**: PUT
    - **URL**: /climate/updateClimateService/name/:oldName
    - **Semantics**: 
      - **oldname**: Existing service name.
        - **name** (string, not null): New name of the climate service
        - **creatorId** (string, not null): ID of the creator
        - **purpose** (string, optional): Purpose of the climate service
        - **url** (string, optional): Url linked to the configuration page of a certian climate service
        - **scenario** (string, optional): Scenario in which the climate service could be used
      
        - **createTime** (string, default to current time): Time the climate service is created, defaults to current time
        - **versionNo** (double, optional): Version number of the service
        - **rootServiceId** (int, optional): Root service id of the service 
    - **Sample Usages**:
      - http://einstein.sv.cmu.edu:9008/updateClimateService/name/testName
      - **Result**: HTTP 200 if the climate service has been successfully updated to the database.
      
10. <a name="10"></a>**DELETE A CLIMATE SERVICE BY SERVICE ID**
    - **Purpose**: Delete a service from the system.
    - **Method**: DELETE
    - **URL**: /climate/deleteClimateService/:id
    - **Semantics**:
        - **id**: Existing service id.
    - **Sample Usages**: 
      - /climate/deleteClimateService/20
      - **Result**: HTTP 200 if returned successfully, HTTP 404 if not found.

####Manage Service Configuration
11. <a name="11"></a>**GET A SERVICE CONFIGURATION BY SERVICE ID**
    - **Purpose**: Query a specific climate service configuration using service id. 
    - **Method**: GET
    - **URL**: /climate/getServiceConfiguration/:id/json
    - **Semantics**:
        - **id**: Existing service id.
    - **Sample Usages**: 
      - **Sample json request**:       
      - **Sample json result**: <br/>
          [{"timestamp":1368568993000,"value":517,"sensorName":"sensor1"},
          ... <br/>
          {"timestamp":1368568896000,"value": 520,"sensorName":"sensor1"}]
      - **Result**: HTTP 200 if successful, HTTP 404 if failed.

12. <a name="12"></a>**GET ALL SERVICE CONFIGURATIONS CREATED BY A USER**
    - **Purpose**: Query all service configurations created by a certain user using the user's id. 
    - **Method**: GET
    - **URL**: /climate/getAllServiceConfigurationsByUserId/:userId/json
    - **Semantics**:
        - **userId**: Existing user's id.
    - **Sample Usages**: 
      - **Sample json request**:       
      - **Sample json result**: <br/>
          [{"timestamp":1368568993000,"value":517,"sensorName":"sensor1"},
          ... <br/>
          {"timestamp":1368568896000,"value": 520,"sensorName":"sensor1"}]
      - **Result**: HTTP 200 if successful, HTTP 404 if failed.
 
13. <a name="13"></a>**ADD A SERVICE CONFIGURATION**
    - **Purpose**: Add a new service configuration to the system. 
    - **Method**: POST
    - **URL**: /climate/addServiceConfiguration
    - **Semantics**: As a POST method, the API cannot be directly executed through a web browser. Instead, it may be executed through Rails, JQuery, Python, BASH, etc.
        - **serviceId**: 
        - **userId**
    - **Sample Usages**: 
      - **Sample json request**:       
      - **Sample json result**: <br/>
          [{"timestamp":1368568993000,"value":517,"sensorName":"sensor1"},
          ... <br/>
          {"timestamp":1368568896000,"value": 520,"sensorName":"sensor1"}]
      - **Result**: HTTP 201 if the service configuration has been successfully added to the database, HTTP 400 if failed.
      
14. <a name="14"></a>**UPDATE A SERVICE CONFIGURATION BY SERVICE ID**
    - **Purpose**: Update a service configuration using specific service id in the system. 
    - **Method**: PUT
    - **URL**: /climate/updateServiceConfiguration/id/:id
    - **Semantics**:
        - **id**: Existing service id.
    - **Sample Usages**: 
      - **Sample json request**:       
      - **Sample json result**: <br/>
          [{"timestamp":1368568993000,"value":517,"sensorName":"sensor1"},
          ... <br/>
          {"timestamp":1368568896000,"value": 520,"sensorName":"sensor1"}]
      - **Result**: HTTP 201 if the service configuration has been successfully added to the database, HTTP 400 if failed.

15. <a name="15"></a>**DELETE A SERVICE CONFIGURATION**
    - **Purpose**: Delete a service configuration from the system. 
    - **Method**: DELETE
    - **URL**: /climate/deleteServiceConfiguration/:id
    - **Semantics**:
        - **id**: Existing service id.
    - **Sample Usages**: 
      - **Sample json request**:       
      - **Sample json result**: <br/>
          [{"timestamp":1368568993000,"value":517,"sensorName":"sensor1"},
          ... <br/>
          {"timestamp":1368568896000,"value": 520,"sensorName":"sensor1"}]
      - **Result**: HTTP 200 if returned successfully, HTTP 404 if not found. 
 
###Manage Climate Service Parameters     
16. <a name="16"></a>**GET ALL SERVICE PARAMETERS**
    - **Purpose**: Query all service parameters.
    - **Method**: GET
    - **URL**: /parameter/getAllParameters/json
    - **Semantics**:
    - **Sample Usages**:  
      - **Sample json request**: http://einstein.sv.cmu.edu:9000/getAllServiceParameter/json
      - **Sample json result**: [{"serviceId":"2","parameterDataType":"testType","parameterRange":"testrange","parameterEnumeration":"number","parameterRule":"rule","parameterPurpose":"purpose"}]
      - **Result**: HTTP 200 if successful, HTTP 404 if failed.

17. <a name="17"></a>**GET A SINGLE PARAMETER BY NAME**
    - **Purpose**: Query a specific service parameter using name.
    - **Method**: GET
    - **URL**: /parameter/getParameter/name/:name/json
    - **Semantics**:
      - **name**: Existing parameter name.
    - **Sample Usages**:  
      - **Sample json request**: http://einstein.sv.cmu.edu:9000/getAllServiceParameter/json
      - **Sample json result**: [{"serviceId":"2","parameterDataType":"testType","parameterRange":"testrange","parameterEnumeration":"number","parameterRule":"rule","parameterPurpose":"purpose"}]
      - **Result**: HTTP 200 if successful, HTTP 404 if failed.

18. <a name="18"></a>**GET A SINGLE PARAMETER BY ID**
    - **Purpose**: Query a specific service parameter using id.
    - **Method**: GET
    - **URL**: /parameter/getParameter/id/:id/json
    - **Semantics**:
      - **id**: Existing parameter id.
    - **Sample Usages**:  
      - **Sample json request**: http://einstein.sv.cmu.edu:9000/getAllServiceParameter/json
      - **Sample json result**: [{"serviceId":"2","parameterDataType":"testType","parameterRange":"testrange","parameterEnumeration":"number","parameterRule":"rule","parameterPurpose":"purpose"}]
      - **Result**: HTTP 200 if successful, HTTP 404 if failed.
            
19. <a name="19"></a>**ADD SERVICE PARAMETER**
    - **Purpose**: Add a service parameter to the system.
    - **Method**: POST
    - **URL**: /parameter/addParameter
    - **Semantics**: As a POST method, the API cannot be directly executed through a web browser. Instead, it may be executed through Rails, JQuery, Python, BASH, etc.
        - **serviceId** (int, not null): Unique id of service
        - **parameterDataType** (string, optional): Data Type of the parameter
        - **parameterRange** (string, optional): Range of the parameter
        - **parameterEnumeration** (string, optional): Parameter enumeration 
        - **parameterRule** (string, optional): Parameter rule
        - **parameterPurpose** (string, optional): Parameter purpose
    - **Sample Usages**:
      - **Command Line Example**: 
          1. Prepare input sensor type metadata in a json file:
              - "serviceParameter.json" file contains: {"serviceId":"2","parameterDataType":"testType","parameterRange":"testrange","parameterEnumeration":"number","parameterRule":"rule","parameterPurpose":"purpose"}
          2. curl -H "Content-Type: application/json" -d @executionLog.json "http://einstein.sv.cmu.edu:9008/addServiceParameter"
      - **Result**: HTTP 201 if the climate service metadata has been successfully added to the database, HTTP 400 if failed.

20. <a name="20"></a>**UPDATE A SERVICE PARAMETER BY ID**
    - **Purpose**: Update a service parameter using id to the system.
    - **Method**: PUT
    - **URL**: /parameter/updateParameter/id/:id
    - **Semantics**: 
        - **id**: Existing parameter id.
    - **Sample Usages**:
      - **Command Line Example**: 
          1. Prepare input sensor type metadata in a json file:
              - "climateService.json" file contains: {"climateServiceName": "testName", "purpose": "Test only"}
          2. curl -H "Content-Type: application/json" -d @climateService.json "http://einstein.sv.cmu.edu:9008/updateClimateService"
      - **Result**: HTTP 200 if the parameter has been successfully updated to the database.
      
21. <a name="21"></a>**UPDATE A SERVICE PARAMETER BY NAME**
    - **Purpose**: Update a service parameter using name to the system.
    - **Method**: PUT
    - **URL**: /parameter/updateParameter/name/:oldName
    - **Semantics**: 
        - **oldName**: Existing parameter name.
    - **Sample Usages**:
      - **Command Line Example**: 
          1. Prepare input sensor type metadata in a json file:
              - "climateService.json" file contains: {"climateServiceName": "testName", "purpose": "Test only"}
          2. curl -H "Content-Type: application/json" -d @climateService.json "http://einstein.sv.cmu.edu:9008/updateClimateService"
      - **Result**: HTTP 200 if the parameter has been successfully updated to the database.

22. <a name="22"></a>**DELETE A SERVICE PARAMTER**
    - **Purpose**: Delete a service parameter using the name from the system. 
    - **Method**: DELETE
    - **URL**: /parameter/deleteParameter/name/:name
    - **Semantics**:
        - **name**: Existing parameter id.
    - **Sample Usages**: 
      - **Sample json request**:       
      - **Sample json result**: <br/>
          [{"timestamp":1368568993000,"value":517,"sensorName":"sensor1"},
          ... <br/>
          {"timestamp":1368568896000,"value": 520,"sensorName":"sensor1"}]
      - **Result**: HTTP 200 if returned successfully, HTTP 404 if not found.

###Manage Service Configuration Item
23. <a name="23"></a>**GET A SERVICE CONFIGURATION ITEM BY ID**
    - **Purpose**: Query a specific service configuration item using id.
    - **Method**: GET
    - **URL**: /climate/serviceConfigItemById/:id
    - **Semantics**: 
        - **id**: Existing service configuration item id.
    - **Sample Usages**:
      - **Sample request**: 
          
      - **Sample result**: 
      
      - **Result**: HTTP 200 if successful, HTTP 404 if failed.

24. <a name="24"></a>**GET A SERVICE CONFIGURATION ITEM BY A SERVICE CONFIGURATION**
    - **Purpose**: Query a specific service configuration item using one service configuration id.
    - **Method**: GET
    - **URL**: /climate/serviceConfigItemByServiceConfig/:serviceConfigId
    - **Semantics**: 
        - **serviceConfigId**: Existing service configuration id.
    - **Sample Usages**:
      - **Sample request**: 
          
      - **Sample result**: 
      
      - **Result**: HTTP 200 if successful, HTTP 404 if failed.
      
25. <a name="25"></a>**GET A SERVICE CONFIGURATION ITEM BY PARAMETER NAME**
    - **Purpose**: Query a specific service configuration item using parameter name.
    - **Method**: GET
    - **URL**: /climate/serviceConfigItemByParamName/:param
    - **Semantics**: 
        - **param**: Existing parameter name.
    - **Sample Usages**:
      - **Sample request**: 
          
      - **Sample result**: 
      
      - **Result**: HTTP 200 if successful, HTTP 404 if failed.
      
26. <a name="26"></a>**ADD A SERVICE CONFIGURATION ITEM**
    - **Purpose**: Add a new service configuration item to the system.
    - **Method**: POST
    - **URL**: /climate/addServiceConfigItem
    - **Semantics**:  As a POST method, the API cannot be directly executed through a web browser. Instead, it may be executed through Rails, JQuery, Python, BASH, etc.
      - **userId**:
      - **serviceId**:    
    - **Sample Usages**:
      - **Sample request**: 
          
      - **Sample result**: 
               
      - **Result**: HTTP 201 if the new service configuration item has been successfully added to the database, HTTP 400 if failed.
      
27. <a name="27"></a>**UPDATE A SERVICE CONFIGURATION ITEM BY ID**
    - **Purpose**: Update a service configuration item in the system.
    - **Method**: PUT
    - **URL**: /climate/updateServiceConfigItem/id/:id
    - **Semantics**:As a PUT method, the API cannot be directly executed through a web browser.  Instead, it may be executed through Rails, JQuery, Python, BASH, etc.  
      - **id**: Existing service configuration item id.
    - **Sample Usages**:
      - **Sample request**: 
          
      - **Sample result**:
      
      - **Result**: HTTP 201 if the service configuration item has been successfully updated, HTTP 400 if the id is wrong
           
28. <a name="28"></a>**DELETE A SERVICE CONFIGURATION ITEM**
    - **Purpose**: Delete a service configuration item from the system.
    - **Method**: DELETE
    - **URL**: /climate/deleteServiceConfigItem/:id
    - **Semantics**: 
        - **id**: Existing service configuration item id.
    - **Sample Usages**: 
      - **Sample request**: http://einstein.sv.cmu.edu:9000/getSensorReading/androidAccelerometer/1395247329000/json
      - **Sample result**: {"timestamp":1368568896000,"sensorName":"sensor1","value":518}
      - **Result**: HTTP 201 if the service configuration item has been successfully deleted.
      
[1]: http://einstein.sv.cmu.edu:9007/climate "The Application Server running in the Smart Spaces Lab, CMUSV"

Examples:
----------------
1. Consume Rest API in Python
    - GET
    <pre>
      <code>
         import json, requests
         response = requests.get("http://einstein.sv.cmu.edu:9000/get_devices/json")
         print(response.json())
      </code>
    </pre>
    - POST
    <pre>
      <code>
         import requests
         requests.post("http://einstein.sv.cmu.edu:9000/sensors", data={}, headers={}, files={}, cookies=None, auth=None)
      </code>
    </pre>
    
2. Consume Rest API in Java
    - GET
   <pre>
      <code>
      import java.net.HttpURLConnection;
      import java.net.URL;
      public static String httpGet(String urlStr) throws IOException {
              URL url = new URL(urlStr);
      		HttpURLConnection conn = (HttpURLConnection) url.openConnection();
      
      		if (conn.getResponseCode() != 200) {
      			throw new IOException(conn.getResponseMessage());
      		}
      
      		// Buffer the result into a string
      		BufferedReader rd = new BufferedReader(new InputStreamReader(conn.getInputStream()));
      		StringBuilder sb = new StringBuilder();
      		String line;
      		while ((line = rd.readLine()) != null) {
      			sb.append(line);
      		}
      		rd.close();
      
      		conn.disconnect();
      		return sb.toString();
   	}
      </code>
   </pre>
    - POST (Please download Gson Jar first http://code.google.com/p/google-gson/downloads/list)
   <pre>
      <code>
      import java.io.BufferedReader;
      import java.io.IOException;
      import java.io.InputStreamReader;
      import java.io.OutputStream;
      import java.io.OutputStreamWriter;
      import java.io.Writer;
      import java.net.HttpURLConnection;
      import java.net.URL;
      import com.google.gson.JsonObject;
      
      public class SensorReadingPostExample {
         	public static void main(String args[]) throws Exception {
         		String URLStr = "http://einstein.sv.cmu.edu:9000/sensors";
         		java.util.Date date = new java.util.Date();
         		
         		JsonObject jo = new JsonObject();
         		//Sample data
         		jo.addProperty("timestamp", date.getTime()); //Long type
         		jo.addProperty("id", "my_test_device_id");   //String type
         		jo.addProperty("temp", 888);                 //Double type
         		   
         		httpPostSensorReading(URLStr, jo.toString());
         	}
         
         	public static String httpPostSensorReading(String urlStr, String jsonString) throws Exception {
         		URL url = new URL(urlStr);
         		HttpURLConnection conn = (HttpURLConnection) url.openConnection();
         		conn.setRequestMethod("POST");
         		conn.setRequestProperty("Content-Type", "application/json");
         		conn.setRequestProperty("Accept", "application/json");
         		conn.setDoOutput(true);
         
         		// Create the form content
         		OutputStream out = conn.getOutputStream();
         		Writer writer = new OutputStreamWriter(out, "UTF-8");
         
         		writer.write(jsonString);
         
         		writer.close();
         		out.close();
         
         		if (conn.getResponseCode() != 200) {
         			throw new IOException(conn.getResponseMessage());
         		}
         
         		// Buffer the result into a string
         		BufferedReader rd = new BufferedReader(new InputStreamReader(
         				conn.getInputStream()));
         		StringBuilder sb = new StringBuilder();
         		String line;
         		while ((line = rd.readLine()) != null) {
         			sb.append(line);
         		}
         		rd.close();
         
         		conn.disconnect();
         		return sb.toString();
         	}
      
      }
      </code>
   </pre>
