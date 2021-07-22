**POST /rest/api/v0/gdp/stories/make_stories/**
----
  Creates a new Story in Makestory and returns empty response.
* **URL Params**  
  None
* **Headers**  
  Content-Type: application/json 
  Authorization: TBD
* **Data Params**  
```
  { 
    "url": string, 
    "title": string, 
    "categories": [comma separated string], 
    "publisherName": string, 
    "publisherId": string, 
    "language": string, 
    "summary": string, 
  } 
```
* **Success Response:**  
* **Code:** 200  
  **Content:**  `{ }` 
* **Error Response:**  

  * **Code:** 401  
  **Content:** `{ error : "You are unauthorized to make this request." }`

**POST /rest/api/v0/gdp/stories/publish/**
----
  Creates a new Story and returns empty response.
* **URL Params**  
  None
* **Headers**  
  Content-Type: application/json 
  Authorization: TBD
* **Data Params**  
```
  { 
    "storyId": string 
    "title": string
    "imageUrl": string
    "language": string 
    "category": [comma separated string]
    "regionRequests": [ 
          { 
              "region": string
              "glanceTime": {
                      "duration": {
                          "unit": "DurationUnit",
                          "length": 1
                      },
                      "startTime": epochTime
                  }
          }
     ]
    "publisherName":string,    
    "publisherId": string      
    "cards": [ 
      { 
        "pageId" : string 
        "imageUrl": string 
        "imageAttribution": string 
        "isCoverCard": boolean
        "summary": string, 
        "sequenceNumber": integer 
        "url": string 
        "title": string 
        "cta" : { 
            "text": string, 
            "url": string 
          } 
       }   
    ] 
  } 
```
* **Success Response:**  
* **Code:** 200  
  **Content:**  `{ }` 
* **Error Response:**  

  * **Code:** 401  
  **Content:** `{ error : "You are unauthorized to make this request." }`
  
  
Payload Reference :
```` 
enum DurationUnit {
    HOURS
    DAYS
    MINUTES
    SECONDS
}  
````  
  

**POST /rest/api/v0/gdp/stories/image_selection/**
----
  Selects and Returns Urls of Images based on Input Given by the Publisher.
* **URL Params**  
  None
* **Headers**  
  Content-Type: application/json 
  Authorization: TBD
* **Data Params**  
```
  {
    "articles": {
      "title": string
      "description": string
  }
```
* **Success Response:** 
* **Code:** 200  
  **Content:**  `{ 
    "images": [comma separated string]
  }`  
  OR 
* **Code:** 200  
  **Content:**  `{ 
    "images": []
  }`    
* **Error Response:**  
  * **Code:** 401  
  **Content:** `{ error : "You are unauthorized to make this request." }`
  OR  
  * **Code:** 500  
  **Content:** `{ error : "Internal Server Error." }`
  
**POST /rest/api/v0/gdp/stories/cards_story/**
----
  Allows Publisher to add card(s) to an existing published story.
* **URL Params**  
  None
* **Headers**  
  Content-Type: application/json 
  Authorization: TBD
* **Data Params**  
```
  {
    "storyId": string,
    "cards": [ 
      { 
        "pageId" : string 
        "imageUrl": string 
        "imageAttribution": string 
        "isCoverCard": boolean 
        "summary": string, 
        "sequenceNumber": integer 
        "url": string 
        "title": string 
        "cta" : { 
            "text": string, 
            "url": string 
          } 
       }   
    ] 
  }
```
* **Success Response:**  
* **Code:** 200  
  **Content:**  `{ }` 
* **Error Response:**  

  * **Code:** 401  
  **Content:** `{ error : "You are unauthorized to make this request." }`
  
  
  
 GET /rest/api/v0/gdp/stories/published/?storyId=:storyId&partner=:partnerId&region=:regionId&status=:status
----
  Gets All the Published Stories.
* **URL Params**  
  *Optional:* `
    storyId=[string],
    partnerId=[string],
    regionId=[string],
    status=[string]
    `
* **Data Params**  
  None
* **Headers**  
  Content-Type: application/json  
  Authorization: Bearer `<OAuth Token>`
* **Success Response:**  
* **Code:** 200  
  **Content:** 
  
  ```
   { 
      "data": { 
        "count": integer, 
        "next": null, 
        "previous": null, 
        "results": [ 
          { 
            "id": string, 
            "status": "", 
            "imageUrl": "" 
          } 
        ] 
      } 
  }
  ```
* **Error Response:**  
 
  * **Code:** 401  
  **Content:** `{ error : "You are unauthorized to make this request." }`
  
  

 DELETE /rest/api/v0/gdp/stories/:storyId/remove/?pages=:pageId1,pageId2
----
  Remove pageId(s) from an already published story or delete all pages from a story. All pages including the story are removed if no pageId is specified
* **Path Params**  
  *Required:* `
    storyId=[string],
    `
* **URL Params**  
  *Optional:* `
    pageIds=[list of comma separated pageIds],
    `  
* **Data Params**  
  None
* **Headers**  
  Content-Type: application/json  
  Authorization: Bearer `<OAuth Token>`
* **Success Response:**  
* **Code:** 200  
  **Content:**  `{success: "Deletion Operation is successful for story and pages" }` 
  **Content:**  `{success: "Deletion Operation is successful for given pages" }` 
* **Error Response:**  
  * **Code:** 400  
  **Content:** `{ error : "No Published Story Exist" }`  
  OR  
  * **Code:** 401  
  **Content:** `{ error : "You are unauthorized to make this request." }`
