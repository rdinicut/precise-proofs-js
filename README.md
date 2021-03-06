Precise Proofs Js
==============

Read the [introduction on Precise-Proofs](https://github.com/centrifuge/precise-proofs)

Precise Proofs Js is a library for validating fields/leafs from  Merkle proofs created with [precise-proofs](https://github.com/centrifuge/precise-proofs/blob/master/README.md). 
The library supports 2   hashing functions(SHA2_256SHA3_256) and hex or base base64 encoding for the hashes. Out of the box it uses hex encoding and SHA2_256.

In case you generate your proofs with SHA3_256 and have them base64 encoded. You can switch using the following code:

```javascript
import {PreciseProofs, SHA3_256} from "precise-proofs-js";

const preciseProofs = new PreciseProofs('base64',SHA3_256);
```



## Supported Proof format

```js,
  
// Sorted Hashes
{
    "property": "valueA",
    "value": "Example",
    "salt": "d555901541825e5d40612d220142c7428c385c48e0245fd3a40b8e3b64679be1",
    "sortedHashes": [
        "60c3dfcdd85fcef1d4826d4695fb5064aa8434d014f2c1547f9398bdf72bdb75",
        "8951fa82c3f5563d88769a9ecb8f6e03b389c06ff64a1b26dc5898cefe95a42f",
        "46d0a998333fc2c8b4cfff1d5e122f7c32ff46f0a4410f63821f45cc02fd3723"
    ]
}


// Hex with our without the 0x prefix
{
    "property": "valueA",
    "value": "Example",
    "salt": "d555901541825e5d40612d220142c7428c385c48e0245fd3a40b8e3b64679be1",
    "hashes":[  
        { "right": "60c3dfcdd85fcef1d4826d4695fb5064aa8434d014f2c1547f9398bdf72bdb75=" },
        { "left": "8951fa82c3f5563d88769a9ecb8f6e03b389c06ff64a1b26dc5898cefe95a42f" },
        { "right": "46d0a998333fc2c8b4cfff1d5e122f7c32ff46f0a4410f63821f45cc02fd3723" }
    ]
}
    
    
// Base64 Ecoded
{  
    "property":"ValueA",
    "value":"Example",
    "salt":"1VWQFUGCXl1AYS0iAULHQow4XEjgJF/TpAuOO2Rnm+E=",
    "hashes":[  
        { "right": "kYXAGhDdPiFMq1ZQMOZiKmSf1S1eHNgJ6BIPSIExOj8=" },
        { "left":" GDgT7Km6NK6k4N/Id4CZXErL3p6clNX7sVnlNyegdG0=" },
        { "right": "qOZzS+YM8t1OfC87zEKgkKz6q0f3wwk5+ed+PR/2cDA=" }
    ]
}


    
```



## Usage:


```javascript,
import {PreciseProofs} from "precise-proofs-js";

const rootHash = "29dbffa68e5cd48bb4cb2504190f10883fb187793b2f70eab81fb5440c6809b6";
let proof = {
    "property": "valueA",
    "value": "Example",
    "salt": "d555901541825e5d40612d220142c7428c385c48e0245fd3a40b8e3b64679be1",
    "hashes": [
        "60c3dfcdd85fcef1d4826d4695fb5064aa8434d014f2c1547f9398bdf72bdb75",
        "8951fa82c3f5563d88769a9ecb8f6e03b389c06ff64a1b26dc5898cefe95a42f",
        "46d0a998333fc2c8b4cfff1d5e122f7c32ff46f0a4410f63821f45cc02fd3723"
    
    ]
}

const preciseProofs = new PreciseProofs();
const valid = preciseProofs.isValidField(proof, rootHash)
// valid  === true


// With base64 encoding
const base64RootHash = "Qpvx6jMpfee4eXYeDm+DO+Z8iArdnYdm3J3BH0AUxHU=";
const base64Proof = {
    "property": "value1",
    "value": "1",
    "salt": "Bs89XQyxE05c57R5KVb8aFk7rqf+A5XUgxlH3t1hRoY=",
    "hashes": [
    {
      "left": "bklbhC4cmgYc+w3k5an7PWICQHNZtozeqD16b7GE5ZI="
    },
    {
      "right": "5hFb4MZvIgE9RQnQDlOGGjahlgDIJwX7Id98oxFECbo="
    },
    {
      "right": "CT59ksUtUWOq+HagFoJgJziPOiHkHlvsvytA6TnTLq8="
    }
    ]
}

const base64PreciseProofs = new PreciseProofs('base64');
    
const base64Valid = base64PreciseProofs.isValidField(base64Proof, base64RootHash)
// base64Valid  === true 
```

### Missing features
The following features are being worked on:
* construct tree and generate proof