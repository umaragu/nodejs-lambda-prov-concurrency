## AWS Lambda NodeJS Provisioned concurrency

This sample provides a nodejs custom runtime. Nodejs functions in global scope which make calls to external systems using callback or promise will not get completed during the init time. Because of that, using provisioned concurrency will not help having all the global variables initiailized with the warm env.

This sample project exposes a lifecycle hook which will be called during the init method and wait for it to complete.

## Build layer

Build a layer for custom runtime. The default initialization hook is <b>initGlobals</b>. 
To change to a different name, modify the argument in the bootstrap file.

```bash

zip -r nodjs-custom-runtime-hook . --exclude '.git/*'

aws lambda publish-layer-version \
 --layer-name "nodejs-lifecycle-hook-extension" \
 --region <use your region> \
 --zip-file  "fileb://nodjs-custom-runtime-hook.zip"

```

## Testing


## Alternate Nodejs Version

If you need to use alternate nodejs version, follow the instruction below

```bash
cd layer
curl https://nodejs.org/dist/v${version}/node-v${version}-linux-x64.tar.xz --output node-v${version}-linux-x64.tar.xz
tar -xf node-v${version}-linux-x64.tar.xz
rm node-v${version}-linux-x64.tar.xz

```

## Security

See [CONTRIBUTING](CONTRIBUTING.md#security-issue-notifications) for more information.

## License

This library is licensed under the MIT-0 License. See the LICENSE file.

