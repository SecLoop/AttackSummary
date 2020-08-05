# Allowed: *Method
```
Lists the set of requests which the requesting user is allowed to issue for this URL. If this header line is omitted, the default allowed methods are "GET HEAD"

Example of use:
		Allow: GET HEAD PUT
```
# Public: *method
```
As "Allow" but lists those requests which anyone may use. If omitted, the default is "GET" only.

Example of use:
		Public: GET HEAD TEXTSEARCH
```

# Access-Control-Allow-Methods
```
The Access-Control-Allow-Methods response header specifies the method or methods allowed when accessing the resource in response to a preflight request.
```
# Timing-Allow-Origin
```
The Timing-Allow-Origin response header specifies origins that are allowed to see values of attributes retrieved via features of the Resource Timing API, which would otherwise be reported as zero due to cross-origin restrictions.
```
