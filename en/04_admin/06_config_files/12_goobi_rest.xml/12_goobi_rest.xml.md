# goobi_rest.xml

In the `goobi_rest.xml` configuration file, the REST API endpoints used by Goobi Workflow are shared based on the respective path (as part of the URL). For each endpoint, the allowed HTTP methods and various access restrictions can be defined.

The file is usually located here:

```bash
/opt/digiverso/goobi/config/goobi_rest.xml
```

A sample configuration could look like this:

```xml
<?xml version='1.0' encoding='UTF-8'?>
<config>
    <endpoint path="/seterrorstep.*">
        <method name="post">
            <allow netmask="0:0:0:0:0:0:0:1/128" token="CHANGEME"/>
            <allow netmask="127.0.0.0/8" token="CHANGEME"/>
        </method>
    </endpoint>
    <endpoint path="/addtoprocesslog.*">
        <method name="post">
            <allow netmask="0:0:0:0:0:0:0:1/128" token="CHANGEME"/>
            <allow netmask="127.0.0.0/8" token="CHANGEME"/>
        </method>
    </endpoint>
    <endpoint path="/closestep.*">
        <method name="post">
            <allow netmask="0:0:0:0:0:0:0:1/128" token="CHANGEME"/>
            <allow netmask="127.0.0.0/8" token="CHANGEME"/>
        </method>
    </endpoint>
    <endpoint path="/process/check.*">
        <method name="get">
            <allow netmask="127.0.0.0/8" token="CHANGEME"/>
        </method>
    </endpoint>
    <endpoint path="/processes/search">
        <method name="get">
            <allow netmask="127.0.0.0/8" token="CHANGEME"/>
        </method>
        <method name="post">
            <allow netmask="127.0.0.0/8" token="CHANGEME"/>
        </method>
    </endpoint>
    <endpoint path="/vocabulary/.*">
        <cors>
            <method>GET</method>
            <origin>https://intranda.com</origin>               
        </cors>
        <method name="get">
            <allow />
        </method>
        <method name="post">
            <allow />
        </method>
    </endpoint>
    <endpoint path="/mails/disable/.*">
        <method name="get">
            <allow />
        </method>
    </endpoint>

    <!-- allow all commands just locally with the token 'test'
    <endpoint path=".*">
      <method name="post">
        <allow netmask="0:0:0:0:0:0:0:1/128" token="test"/>
        <allow netmask="127.0.0.0/8" token="test"/>
      </method>
      <method name="get">
        <allow netmask="0:0:0:0:0:0:0:1/128" token="test"/>
        <allow netmask="127.0.0.0/8" token="test"/>
      </method>
      <method name="put">
        <allow netmask="0:0:0:0:0:0:0:1/128" token="test"/>
        <allow netmask="127.0.0.0/8" token="test"/>
      </method>
    </endpoint>
    -->
</config>
```

## General structure

A configuration consists of several rules for endpoints. These are the `<endpoint>` elements. Each endpoint element requires a `path` attribute. This specifies the path to the corresponding endpoint and may contain regular expressions. The sub-elements of `<endpoint>` are `<method>` or `<cors>` elements.

## JWT authentication (JSON Web Token).

An endpoint element may additionally contain the `jwtAuth` attribute and require authentication using JSON Web Token. The default value is `false`.

```xml
<endpoint path="." jwtAuth="true">
    ...
</endpoint>
```

If JWT authentication is enabled and the token is invalid, Goobi responds with HTTP status code 401 (Unauthorized).

## Endpoints enabled by default

By default, the following paths are enabled without access restrictions:

```bash
/view/object/
/view/media/
/process/image/
/messages/
/processes/\\d+?/images.*
/openapi.json
```

<!---
In the expression for the operation ID there must be exactly one backslash in the GUI. This escapes the 'd'.
-->

The expression `\\d+?` describes a process id.

When Goobi Workflow is in development mode, the endpoint `/developer/` is enabled by default. As long as Goobi Workflow is developed without port shares on the router in a local network, this endpoint is not publicly accessible.

## Allow access to API methods

One or more allowed HTTP request methods can be specified for each API endpoint. For this purpose, a `method` sub-element is entered in the corresponding `endpoint` for each HTTP method used. A `method` element has exactly one `name` attribute. The most commonly used HTTP methods are:

```text
get
head
post
put
delete
options
```

Within the `method` element, the `allow` element is used to configure the access shares and restrictions for the particular endpoint/method combination. For this, one or more shares are added as follows:

```xml
<method name="get">
    <allow netmask="0:0:0:0:0:0:0:1/128" token="CHANGEME"/>
    <allow netmask="127.0.0.0/8" token="CHANGEME"/>
    <!--
    or for public endpoints:
    -->
    <allow />
</method>
```

An IPv4 or IPv6 netmask is specified with the `netmask` attribute and the associated token with the `token` attribute. If the `token` or the `netmask` attribute is omitted, access is allowed without a token or with any IP address. If both are omitted, the endpoint can be accessed from any IP address without a token. This can be useful if an endpoint is to be completely public or authenticated by other methods (for example JSON web tokens). The `test` token can be used to allow access to endpoints from localhost only.

When checking a request, Goobi proceeds by document order and checks the first `<enpoint>`/`<method>` pair that matches the request. If no `<allow>` rule matching the request is found, Goobi returns status code `401` and refuses to process the request. This also implies that the order of rules in this configuration file should be respected. If Goobi returns a message with 401, it may be because an endpoint higher up was formulated too generally and Goobi does not advance to a rule lower down because processing is already denied due to the rule higher up in the document.

## HTTP header fields

In addition to the shares, the `header` element can be used to specify one or more HTTP header fields which will be automatically written by Goobi to the header fields of the response protocol when requests are made with the corresponding request method at the respective endpoint. This can be handy if the client or browser should get certain meta information about the endpoint's behavior. To do this, the `name` attribute is used to specify the HTTP header field. The `header` element may contain one or more `value` sub-elements and in practice may look like the following:

```xml
<method>
    <allow />
    <header name="Content-Language">
    	<value>de-DE</value>
    	<value>en-US</value>
    </header>
</method>
```

In the HTTP header, following field is added:

```text
HTTP/2 200 OK
...
Content-Language: de-DE, en-US
```

## CORS (Cross Origin Requests)

The configuration also allows cross-origin requests to be enabled. For this purpose, a `<cors>` element can be created inside an endpoint, where the allowed methods are configured with `<method>` elements and the allowed origins with `<origin>` elements. If a `<cors>` element is configured for an endpoint, Goobi will automatically handle any preflight requests sent by the browser. For example, the configuration may look like the following:

```xml
<endpoint path="/vocabulary/.*">
    <cors>
        <method>GET</method>
        <origin>https://intranda.com</origin>               
    </cors>
    <method name="get">
        <allow />
    </method>
    <method name="post">
        <allow />
    </method>
</endpoint>
```

The cross-origin methods can be queried using the HTTP request method `OPTIONS` and the endpoint specified in the configuration. For example, if an HTTP request is sent with the following header, Goobi lists the possible cross-origin methods in the HTTP response header fields. For an `OPTIONS` request, the response has no content and the status code is 204 (No Content).

Request:
```text
OPTIONS /vocabulary/.* HTTP/2
...
```

Answer:
```text
HTTP/2 204 No Content
...
Access-Control-Allow-Methods: GET
Access-Control-Allow-Origin: https://intranda.com
Access-Control-Allow-Headers: origin,content-type,accept,token
...
```