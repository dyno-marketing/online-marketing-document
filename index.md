# SmartPx Integration Document 

## Integration Steps
### Step 1
Insert the script bellow into the `<head>` element of client’s website
```html
<script src="https://smartpx.io/sdk/smartpx.min.js?v=1.2"></script>
<script type="text/javascript">
	Smartpx.init({
		is_check: false, // Redirect to Social Id detection service, default false
		custom_fields: {
			"source": <int: source_id>, // Require
			"f": <string: facebook_id>, // Not require - Default empty
	                "is_newer_f_version": <boolean: is_newer_f_version> // Not require - Default false
			"p": <string: phone>, // Not require - Default empty
			"e": <string: email>, // Not require - Default empty
		}
	});
</script>
```
Every time a customer visits SmartPx integrated website, our system will write a data field called ```session_id``` into his/her browser’s cookie, which will allow us to transparently integrate with each other.

### Step 2
Get SmartPx ```session_id``` via this script:
```html
<script>
var session_id = Smartpx.getSession();
</script>
```

### Step 3 
Call SmartPx api to get demographic information and interest of ```session_id``` which belongs to specific user you want to target

## Api: 
### Base Url: ```https://gateway.dyno.me/online-marketing-api```

### Customer Demographic
Path: /profiles/sessions/:session_id/demographic
* Method: Get
* Sample response: 
```json
{"has_error":false,"data":{"demographic":{"firstName":"Tu","lastName":"Pham","genderType":1,"middleName":"Phuong","locale":"en_US","sessionId":"ycsq99fao1f1501125848939", "age_group":"2"}}}
```
* Notes:
- age_group: 0: 13 -> 17, 1: 18 -> 24, 2: 25 -> 34, 3: 35 -> 44, 4: 45 -> 54, 5: 55 -> 64, 6: 65+


### Customer Interest
Path: /profiles/sessions/:session_id/interest
* Method: Get
* Sample response: 
```json
{"has_error":false,"data":{"top_categories":[{"score":"0","categoryId":"e4f43e90-670c-11e7-bbb9-2477038c8d04"},{"score":"83","categoryId":"a6156d20-670c-11e7-bbb9-2477038c8d04"},{"score":"96","categoryId":"c4f21f40-670c-11e7-bbb9-2477038c8d04"},{"score":"63","categoryId":"a20cdd30-670c-11e7-bbb9-2477038c8d04"},{"score":"0","categoryId":"1cda0c50-670c-11e7-bbb9-2477038c8d04"},{"score":"47","categoryId":"d174f120-670c-11e7-bbb9-2477038c8d04"}]}}
```

### Get all interest categories
Path: /categories
* Method: Get
* Sample response: 
```json
{"has_error":false,"data":{"categories":[{"id":"06d99240-670c-11e7-bbb9-2477038c8d04","name":"Pets","parentId":"f895fd90-670b-11e7-bbb9-2477038c8d04","path":"f895fd90-670b-11e7-bbb9-2477038c8d04","created":1499868701,"updated":0,"deleted":0},{"id":"090c0d30-670d-11e7-bbb9-2477038c8d04","name":"Restaurant","parentId":"ec7d90d0-670c-11e7-bbb9-2477038c8d04","path":"ec7d90d0-670c-11e7-bbb9-2477038c8d04","created":1499869134,"updated":0,"deleted":0},{"id":"0aec5b60-670c-11e7-bbb9-2477038c8d04","name":"Politics & Social Issues","parentId":"f895fd90-670b-11e7-bbb9-2477038c8d04","path":"f895fd90-670b-11e7-bbb9-2477038c8d04","created":1499868707,"updated":0,"deleted":0},{"id":"11989ea0-670d-11e7-bbb9-2477038c8d04","name":"Family & Relationship","parentId":"","path":"","created":1499869148,"updated":0,"deleted":0},{"id":"158b2b00-670c-11e7-bbb9-2477038c8d04","name":"Do it yourself (DIY)","parentId":"f895fd90-670b-11e7-bbb9-2477038c8d04","path":"f895fd90-670b-11e7-bbb9-2477038c8d04","created":1499868725,"updated":0,"deleted":0},{"id":"1cda0c50-670c-11e7-bbb9-2477038c8d04","name":"Travel","parentId":"f895fd90-670b-11e7-bbb9-2477038c8d04","path":"f895fd90-670b-11e7-bbb9-2477038c8d04","created":1499868737,"updated":0,"deleted":0}]}}
```
* Reference: [DYNO Response Data Decode Document](https://docs.google.com/spreadsheets/d/1U84yleaRtQewOsbIqmkkJkB8fES9YdYcWH_Sej_ycYc/edit#gid=1975035837)

# Mobile flow
## Api
### Base Url: ```https://gateway.dyno.me/social-login-api```
### App Login
Path: /api/social
* Method: Post
* Params:
```json
{    
  "d_o": <int: device_os>, // Require
  "d_t": <int: device_type>, // Require
  "d_i": <int: device_id>, // Require
  "a_id": <int: advertising_id>, // Require
  "s_i": <string: social_id>, // Require
  "s_t": <string: social_type>, // Require
  "is_newer_f_version": <boolean: is_newer_f_version>, // Not require - Default false
  "p": <string: phone>, // Not require - Default empty
  "e": <string: email>, // Not require - Default empty
}
```
* Default value
``` 
   DEVICE_OS = (1, 'Android'), (2, 'Ios'), (3, 'Winphone')
   DEVICE_TYPE = (1, 'Phone'), (2, 'Tablet/Ipad'), (99, 'Other')
   SOCIAL_TYPE = (1, 'Facebook'), (2, 'Google Plus'), (3, 'Instagram'), (4, 'Twitter'), (5, 'Zalo')
```

