# Solid Local Pod

A nodejs library which can be used for running a solid pod over localhost.

## Install

```sh
npm install solid-local-pod
```

## Usage Example

This setup will serve the contents from the `/home/user/test` folder at https://localhost:3000. (Due to the automatic ssl certificate generation, you will likely need to accept the security risks in your browser, before being able to use it)

```javascript
const httpsLocalhost = require("https-localhost")()
const LocalPod = require('solid-local-pod')
const solidFileFetch = require('solid-local-pod/src/solidFileFetch')

async function main() {
    // Note: If no certs are provided, it will run on http://localhost:${port}, else https://localhost${port}
    const certs = await httpsLocalhost.getCerts()

    const pod = new LocalPod({
        port: 3000,
        basePath: '/home/user/test',
        certs,
        fetch: solidFileFetch
    })

    pod.startListening()
}
main()
```

You can also take a look at [solid-local-pod-manager](https://github.com/Otto-AA/solid-local-pod-manager) which uses this library.

## Configuration

| Param        | Type           | Description  |
| ------------- |:-------------:|:-----|
| fetch        | (url, options) => Response | Similar to window.fetch. (e.g. solid-auth-cli or solid-local-pod/src/solidFileFetch) |
| port         | number      |   A free port |
| basePath | string      | This will be the root of the solid pod |
| prefix | [string]      | (Optional) Will be prepend to the request path |
| certs | [?] | (Optional) Certificates used for https

## Methods

| Name        |  Description  |
|:------------- |:-----|
| startListening        | Starts the localhost server |
| stopListening         | Stops the localhost server |
| isListening           | Returns true if server is active |
