
# NeoLink

This is a Chrome extension wallet for the Neo Smart Economy.

Currently the project is undergoing heavy development and is hardcoded to only operate on TestNet.

![alt](https://github.com/phetter/NeoLink/blob/master/neolink_alpha_ss.png)


## Current Features

* Open a wallet using an encyrpted WIF
* Get a list of transactions for any known address - does not require login
* Get the balance of any known address - does not require login
* Send Neo or Gas to an address
* Test invoke smart contracts, with parameters, to determine gas cost and test
* Send invoke smart contracts with parameters and arguments
* Authorize both types of smart contract invocations as requested by third-party dApp
* SemVer 2.0 compliant http://semver.org/


## Future Features

* Easy selection of MainNet, TestNet, or custom private net
* Contact book that remembers addresses used 
* Configurable watch wallet for any saved addresses to display balances all in one view
* Create wallet
* Import Wallet
* Export Wallet
* Ledger hardware support
* Any ideas from the community!


## Setup

yarn install

yarn run start &#35; (for development with live reload)

yarn run build &#35; (production)


Your unpacked extension will be in the ./build/ folder.

See https://developer.chrome.com/extensions/getstarted#unpacked for instructions on manually loading an unpacked Chrome extension in developer mode.

## Use NeoLink with your dApp

Add the following code to your dApp:


```
<input type='text' id='contractScriptHash' />
<input type='text' id='operationName' />
<input type='text' id='runInvokeArgument1' />
<input type='text' id='runInvokeArgument2' />
<input type='text' id='assetType' />
<input type='text' id='assetAmount' />

<button id="runInvokeButton">Invoke</button>
<script>
document.getElementById("runInvokeButton).addEventListener("click",
    function() {
      var scriptHash = document.getElementById("contractScriptHash").value
      var operation = document.getElementById("operationName").value
      var invokeArg1 = document.getElementById("runInvokeArgument1").value
      var invokeArg2 = document.getElementById("runInvokeArgument2").value
      var type = document.getElementById("assetType").value
      var amount = document.getElementById("assetAmount").value

      var invocationObject = {
        'scriptHash': scriptHash,
        'operation': operation,
        'arg1': invokeArg1,
        'arg2': invokeArg2,
        'assetType': type,
        'assetAmount': amount
      }
      window.postMessage({ type: "FROM_PAGE", text: invocationObject }, "*");
}, false);
</script>
```


Please note that currently the code is limited to a maximum of three arguments to the smart contract.

TODO: add arbritrary number of arguments


## Triggering an IoT Smart Contract Payment

### Python

Python command line: (must be synced to TestNet)
```
testinvoke b3a14d99a3fb6646c78bf2f4e2f25a7964d2956a putvalue ['test','0000ff'] --attach-gas=0.000025

```

### NeoLink

- Install NeoLink
    - Clone github.com/cityofzion/neolink/
    - Follow the instructions there to install and build
    - Login with encrypted WIF (wallet needs a balance of TestNet gas)
- Login to iot.splyse.tech
    - user: neo@splyse.tech
    - pass: neo
- Locate contract with name 'test' in the list of Devices
- Enter a color code hex value in the form of '00ff00' (without quotes) into the input field
- Click pay
- If you are logged into your NeoLink wallet you will see a message in the web page asking you to open NeoLink and authorize the transaction.
- Open NeoLink and click the 'yes' button to authorize the transaction.

