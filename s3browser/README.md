# s3 browser

The S3 browser proposed, alongside with the following instructions, have the solely purpose of demoing a GUI experience with `s3gw`.  
This S3 browser is a patched version of [Rhosys/aws-s3-explorer](https://github.com/Rhosys/aws-s3-explorer).

## Requirements

- [s3cmd](https://github.com/s3tools/s3cmd)
- npm

## Instructions

These instructions assume you have created a bucked named `test`.

### Set `CORS` permissions on bucket `test`

```shell
$ s3cmd -c s3cmd.cfg setcors cors.xml s3://test
..
DEBUG: response - 200
```

`cors.xml`:

```xml
<CORSConfiguration>
<CORSRule>
    <ID>Allow everything</ID>
    <AllowedOrigin>*</AllowedOrigin>
    <AllowedMethod>GET</AllowedMethod>
    <AllowedMethod>HEAD</AllowedMethod>
    <AllowedMethod>PUT</AllowedMethod>
    <AllowedMethod>POST</AllowedMethod>
    <AllowedMethod>DELETE</AllowedMethod>
    <AllowedHeader>*</AllowedHeader>
    <MaxAgeSeconds>120</MaxAgeSeconds>
</CORSRule>
</CORSConfiguration> 
```

This will make your browser to be authorized from backend for all `CORS` related calls.

### Set up S3 browser application

1. Clone [giubacc/aws-s3-explorer](https://github.com/giubacc/aws-s3-explorer)
2. Checkout `s3gw-demo` branch
3. Identify the following code portion in `src/store.js` and change the values accordingly with your environment

```javascript
endpoint: 'http://s3gw-no-tls.local:30080',
accessKeyId: '0555b35654ad1656d804',
secretAccessKey: 'h7GhxuBLTrlhVUyxSPUKUV8r/2EI4ngqJxD7iBdBYLhwluN30JaT3Q==',
```

After this, you can execute

```shell
npm install
npm start
```

This should spawn up a local web server at:

```text
http://localhost:8080/
```

Accessing with your web browser at that address should show you the S3 browser application up and running.
