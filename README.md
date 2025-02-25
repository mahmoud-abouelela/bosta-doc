# Bosta API
# User
User creates account manually , creates a business after verification and get API_KEY   
## Pickup locations
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
              "isDefault": false
          }

  - #### DELETE: Deletes a pickup location (make sure it is not linked with an upcoming pickup)
      Payload: NO PAYLOAD

      Response:

            "success": true,
            "message": "pickup location deleted successfully.",
            "data": null
### Url: [http://app.bosta.co/api/v2/pickup-locations/{id}/default](http://app.bosta.co/api/v2/pickup-locations/{id}/default)
Description :   Sets a pickup location to be default
  - #### PUT: Retrieves details of a single pickup location
    Payload: NO PAYLOAD

### Url: 
