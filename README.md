# Bosta API
# User
User creates account manually , creates a business after verification and get API_KEY   
# Pickup locations
### Url:  [http://app.bosta.co/api/v2/pickup-locations](http://app.bosta.co/api/v2/pickup-locations)

Description :

 - #### GET:  Retrieves all business locations by using API KEY
	  Payload: NO PAYLOAD

   RESPONSE: Returns a list of pickup locations for this business   
  - #### POST: Adds pickup location to your business based on district id   fetched from Bosta
    - **Steps**:
        To create a pickup location you need to first get the district id which is nearest to you (make sure that  **pickupAvailability: true** in response)
      
        - **First Method:**
      
             1- By getting all cities, find the city id [GET: http://app.bosta.co/api/v2/cities](http://app.bosta.co/api/v2/cities)
      
             2- Get districts info by passing city it in url, which returns list of districts in this city
    
             [GET: http://app.bosta.co/api/v2/cities/{cityId}/districts](http://app.bosta.co/api/v2/cities/{cityId}/districts)
          
        - **Second Method:**
      
             1- Get your location's latitude and longitude
          
             2- Pass it as query params which will return city info, zone info, district info based on your location (it is not accurate for your exact location try making the scope bigger)
    
             [GET: http://app.bosta.co/api/v2/cities/pinLocation?lat=30.071004&lng=31.346511](http://app.bosta.co/api/v2/cities/pinLocation?lat=30.071004&lng=31.346511)
          
    		**BOSTA Address Format**

				 city: "City name from the cities list (Required)",
				 zoneId: "you can get the zone ids from the zones API listed above (Optional)",
				 districtId: "you can get the district ids from the districts API listed above (Required)",
				 firstLine: "Address Line 1 (Required) and MUST be at least 5 characters.",
				 secondLine:" Nearby Landmark (Optional)",
				 buildingNumber: "(Optional)",
				 floor: "(Optional)",
				 apartment: "Apartment number (Optional)",
				 geoLocation: [lat, long] (Optional), // Preferred,
				 isWorkAddress: "boolean value (true or false) (Optional)",
				 locationName:" Only needed when specifying you business location",
	 - **Payload**:
		
          ![image](https://github.com/user-attachments/assets/2e6beea6-6215-4293-9e38-d2f027769440)
      
### Url: [http://app.bosta.co/api/v2/pickup-locations/{pickup_location_id}](http://app.bosta.co/api/v2/pickup-locations/{pickup_location_id})

Description :
  - #### GET: Retrieves details of a single pickup location
      Payload: NO PAYLOAD


      Response:


       ![{BCC72E5D-05D6-493C-B856-5E4040286966}](https://github.com/user-attachments/assets/3999cba8-2800-4f8a-8e79-d7ab8e94bf9d)

 - #### PUT: Edits details of pickup location
      Payload:

    
      ![{8876490E-DBF7-45AE-9234-D3C6A07BF46D}](https://github.com/user-attachments/assets/62774604-8098-493e-bf44-f5a1675e4425)

     Response:
    
          "success": true,
          "message": "pickup location updated successfully.",
          "data": {
              "isDefault": false}

  - #### DELETE: Deletes a pickup location (make sure it is not linked with an upcoming pickup)
      Payload: NO PAYLOAD

      Response:

            "success": true,
            "message": "pickup location deleted successfully.",
            "data": null
### Url: [http://app.bosta.co/api/v2/pickup-locations/{id}/default](http://app.bosta.co/api/v2/pickup-locations/{id}/default)
Description :   
  - #### PUT: Sets a pickup location to be default
    Payload: NO PAYLOAD

# Pickup Requests
### Url: [http://app.bosta.co/api/v2/pickups/available-dates?days=5](http://app.bosta.co/api/v2/pickups/available-dates?days=5)
Description :   
  - #### GET: Retrives list of avalible pickup dates returning dates = the number specified in the url
    Payload: NO PAYLOAD

	Response:

	   ![{FFD2C487-EE94-4A61-9A9A-3D574E77C6BA}](https://github.com/user-attachments/assets/c1ac8bab-d668-4399-8f1c-74165105c6e5)


### Url: [http://app.bosta.co/api/v2/pickups](http://app.bosta.co/api/v2/pickups)
Description :   
  - #### GET: Retrives all pickups for a business (must provide page number '?page=1')
    Payload: NO PAYLOAD

	Response:

	![{42296B9C-87CF-4C7C-88BF-383BC7D71C27}](https://github.com/user-attachments/assets/8a0a6a88-089a-4daf-a183-df54ba410970)
 - #### POST: Creates a new pickup ( contact person is set to location contact info if not specified, repetedDate is by default set to ONE TIME if not sent)
   try to assign dates which is avalible for pickup

   
    Payload:

	![image](https://github.com/user-attachments/assets/e578e5fe-2e6c-4e67-a85e-96556394647c)

### Url: [http://app.bosta.co/api/v2/pickups/{id}](http://app.bosta.co/api/v2/pickups/{id})
Description :   
  - #### GET: 
    Payload: NO PAYLOAD


    Response:

      ![image](https://github.com/user-attachments/assets/fa994970-e7d9-42cc-94a7-46a1f3935751)

- #### PUT: Updates pickup certain feilds
   Payload:

     ![image](https://github.com/user-attachments/assets/54f60f89-8ed1-4107-bd35-a46de7e52c3b)

  Response:

    ![image](https://github.com/user-attachments/assets/e5830a61-bc25-4c58-8860-a98c2a492f0f)

  
- #### Delete: Deletes pickup request with its id
   Payload: NO PAYLOAD

# Order Requests
  Description:
  
### Types of orders 
     
   Type |  Code|  Timeline Status |
   -----|-------| ---------------|
  Deliver	| 10 | **new:** 10, **pickedup:** 21, **transit:** 30, **out_for_delivery:** 41, **delivered:** 45| 
  Cash Collection | 15 |  **ready_for_collection:** 11,**out_for_collection:** 40, **collected:** 45|
  Exchange | 30 | **new:** 10, **pickedup:** 21, **transit:** 30, **out_for_return:** 41, **returned:** 46|
  Customer Return Pickup | 25 |  **new:** 10, **pickedup:** 23, **transit:** 30, **out_for_exchange:** 41, **out_for_return:** 41, **exchange_returned:** 46|
  Sign & Return | 35 | **new:** 10, **pickedup:** 21, **transit:** 30, **out_for_signature:** 22, **out_for_return:** 41, **signed_and_returned:** 46|

### Shipping Fees
  Shipping fees varaies based on pickup location, drop-off, package size additional funds is added if you enable that customer can open the package
	
  [https://business.bosta.co/settings/pricing-plan](https://business.bosta.co/settings/pricing-plan)
  
### 

### Url: [https://app.bosta.co/api/v2/deliveries](https://app.bosta.co/api/v2/deliveries) 

 - #### POST: 

   #### DELIVERY:
      Payload:

     ![image](https://github.com/user-attachments/assets/379f4526-13a3-42f9-8eb1-1725b88e820a)


     Response:

     ![image](https://github.com/user-attachments/assets/c9f3cdb5-828c-4982-a4fe-7f222174f47a)
  
   #### Exchange:
      Payload:

      ![image](https://github.com/user-attachments/assets/ab4a5858-cf49-433e-b80f-a142caa98bc9)


     Response:

     ![image](https://github.com/user-attachments/assets/c9f3cdb5-828c-4982-a4fe-7f222174f47a) 

   #### Return:
	
      Payload:

      ![image](https://github.com/user-attachments/assets/ec45a6a6-77e5-4569-b739-99f3c421c9c0)


     Response:
   
      It is expected to be picked up from your customer within 4 days (as shown on the ui)


      ![image](https://github.com/user-attachments/assets/82fbd87c-fe6b-4812-b00a-65d3d6b2b563)

   #### Cash Collection:
      Payload:


      Based on the amount of cash to be collected and the location bosta fees will change it is the same from 1 - 2000EGP if the amount increased the fees will increase

      ![image](https://github.com/user-attachments/assets/3dfe3ceb-7a34-48a9-b7b1-79edd40512dc)


     Response:

      It is expected to be picked up from your customer within 4 days (as shown on the ui)


      ![image](https://github.com/user-attachments/assets/eaf4b14e-97e6-4eee-895e-ae83ddc16ff0)


   #### Sign & return:
      Payload:

      ![image](https://github.com/user-attachments/assets/89ed86b5-ef8f-433f-8296-fbfc29ee8043)


     Response:
		
     ![image](https://github.com/user-attachments/assets/c9f3cdb5-828c-4982-a4fe-7f222174f47a) 
