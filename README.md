# Generating Secure Hash
```javascript
var postData = {
    param1: value1,
    param2: value2,
    param3: value3
};
function generateHash(postData) {
	var key = '';

	//sort input param
	var orderedData = {};
	Object.keys(postData).sort().forEach(function(key) {
		orderedData[key] = postData[key];
	});

	//format uri encoding of param Object
	var message = '';
	for (var i in orderedData) {
		message += '&' + i + '=' + orderedData[i];
	}
	message = message.substr(1);

	//generate the secure hash
	var cr = require('crypto');
	var Buffer = require('buffer').Buffer;
	var privateKey = new Buffer(key, 'hex', 'ascii');

	var hash = cr.createHmac('sha256', privateKey).update(message).digest('hex');

	return hash;
}
// this value of secureHash should be with the request
var mySecureHash = generateHash(postData);
```

```php
$postData = new ArrayObject();
$postData.param1=$value1;
$postData.param2=$value2;
$postData.param3=$value3;

function generateHash($postData) {
    $key = "";
    $orderedData = new Object();
    call_method(call_method(call_method($Object, "keys", $postData), "sort"), "forEach", new Func(function($key = null) use (&$orderedData, &$postData) {
        set($orderedData, $key, get($postData, $key));
    }));
    $message = "";
    foreach (keys($orderedData) as $i) {
        $message = _plus($message, _concat("&", $i, "=", get($orderedData, $i)));
    }
    $message = call($encodeURI, call_method($message, "substr", 1.0));
    $cr = call($require, "crypto");
    $Buffer = get(call($require, "buffer"), "Buffer");
    $privateKey = _new($Buffer, $key, "hex", "ascii");
    $hash = call_method(call_method(call_method($cr, "createHmac", "sha256", $privateKey), "update", $message), "digest", "hex");
    return $hash;
});
$secureHash = generateHash($postData);
```


In order to generate toy hash secret
 1. **Order** , order all send parameters from A-Z except <code>AppId</code> and <code>Password</code>
 2. **Concat** , concat parameters as URL query parameters, 
    ex: <code>param1=param1Value&param2=param2Value</code>
 3. **Hash** , hash the concated string using <code>SHA-256 HMAC</code> with your <code>hash secret</code>, you can get it from your merchant account merchant portal [merchant portal](http://business.vapulus.com)


<aside class="notice">
Please be aware that <code class="text-block">appId</code>, <code class="text-block">password</code> and <code class="text-block">hash secret</code> are provided for you in your application details when you create a new application on vapulus. If you didn't already add an application, you can add one by going to (App > add app) from <a href="https://business.vapulus.com/" target="_blank">merchant portal</a> then go to applications, you'll find your applications are listed, click on any of them and it will redirect you to the details of that application where can find all the params and other details you gonna need.
</aside>
<aside class="notice">
If you using node.js you can use our npm generate secret hashing package [Using NPM package to generate secure hash](#Using-NPM-package-to-generate-secure-hash)
</aside>

## Example
If your request parameters as follow:

Param Name   | Example Value              
------------ | ---------------------------
cardNum      | 5123456789012346           
cardExp      | 2105                       
cardCVC      | 123                        
holderName   | John Doe                   
mobileNumber | 20100000000000             

After **order** and **concat** string will be:
<code>cardCVC=123&cardExp=2105&cardNum=5123456789012346&holderName=John Doe&mobileNumber=20100000000000</code>

The Secure Hash value is:
<code>a79f3371b3c4b0d867c9fe1b6be3ec69b79c3c526393f6736b4c5c0917690d9c</code>


## Using NPM package to generate secure hash

If you wish to use our npm package to generate your <code>secure hash</code> string, then follow theses instructions:
1. Install npm package <code>npm install vapulus-hashing-pkg --save</code>
2. The package is now installed in your project, you can now require it and use it as shown on the right dark side. 


```javascript
var vapulusHash = require('vapulus-hashing-pkg');

var myRequestParams = {
    cardNum : '5123456789012346',
    cardExp : 2105,
    cardCVC : 123,
    holderName :'John Doe',
    mobileNumber :'20100000000000'
};

var secureHash = vapulusHash.generateHash(myRequestParams);
```
