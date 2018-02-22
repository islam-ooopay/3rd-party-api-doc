## Add card

```bash
curl -X POST "https://3rdparty.vapulus.com/app/addCard" \
  -d appId=XXX \
  -d password=XXX \
  -d cardNum=XXX \
  -d cardExp=XXX \
  -d cardCVC=XXX \
  -d holderName=XXX \
  -d mobileNumber=XXX 
```

```javascript
// required params are:
var postData = {
  "cardNum": _CardNum,
  "cardExp": _isoDate,
  "cardCVC": _CardCVC,
  "holderName": _holderName,
  "mobileNumber": _mobileNumber,
};
```

```php
$request_string = 'cardNum=' + $_cardNum 
                  + '&cardExp=' + $_cardExp 
                  + '&cardCVC=' + $_cardCVC 
                  + '&holderName=' + $_holderName
                  + '&mobileNumber=' + $_mobileNumber;
```


> The above request will returns JSON structured like this:

```json
{
  "msg" : "response msg",
  "statusCode": 200,
  "data": {
    "userId": 1,
    "cardId": "asd-asd648as-das546asd-ads564"
  }
}
```
**<code class="text-block">[_baseUrl](#3rd-Party-API-List)</code> + <code class="text-block">app/addCard</code>**

Allow the 3rd party app to card and get back card and user ids' for this card

These are the params you will need:

| Params       | Description                                    | restriction |
| ------------ | ---------------------------------------------- | :---------: |
| cardNum      | the 16 numbers of the card                     | required    |
| cardExp      | the expiry date of the card, <code>YYMM</code> | required    |
| cardCVC      | the cvc number on the card                     | required    |
| holderName   | name of the card owner                         | required    |
| mobileNumber | mobile number of card owner                    | required    |

<aside class="notice">
In additional to these params you have to send <code class="text-block">appId</code>, <code class="text-block">password</code> and <code class="text-block">hashSecret</code>
</aside>
<aside class="notice">
In order for you to generate secure hash look at <a href="#Generating-Secure-Hash">Generating Secure Hash</a>
</aside>
