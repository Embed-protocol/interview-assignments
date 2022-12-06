## Context

You are tackling a bounty for a protocol: You will be implementing the smart contract for its upcoming airdrop of EMB ERC20 token.

Another Protocol member has already written some boilerplate contract and testing code for you to use, but the bulk of the work, the protocol's minting functionality, is up to you to design, implement, and test.

One primary focus for the airdrop is of course security, so pay special attention to that in your submission.

Instead of minting and distributing all the tokens in a single transaction (which might not be possible if the number of minters is large), the Protocol wants you to authenticate minters using ECDSA signatures.

You can assume there already exists some secure software for distributing these signatures to the correct minters.

Using ECDSA signatures to validate mints is the Protocol's preferred mechanism, because it means the airdrop can be extended to additional minter addresses (by creating new signatures) without making any changes to the `Protocol.sol` contract (see below).

The data being signed (using EIP-712) is of the shape:

`(address _minter, uint256 _amount)`

Your `Protocol.signatureMint` function must verify a passed-in signature and distribute the appropriate amount of EMB.

## Constraints

You **cannot** import any additional third party contracts, other than those already provided in the given Solidity and Typescript code. 


## Provided Contract and Testing Code
`EMB.sol`
`Protocol.sol`

### Important note

_The function signatures for minting (`Protocol.signatureMint`) given in the `Protocol.sol` contract below may not be complete. Also the EMB.sol may not be complete. You may need to add additional arguments in order to write a correct implementation that insures security and low gas expense.



`protocol.spec.ts`

```javascript
import { SignerWithAddress } from "@nomiclabs/hardhat-ethers/signers";
import { expect } from "chai";
import { ethers } from "hardhat";
import { Protocol, ERC20, EMBToken } from "../typechain-types"

const provider = ethers.provider
let account1: SignerWithAddress
let account2: SignerWithAddress
let rest: SignerWithAddress[]

let EMBToken: EMBToken
let protocol: Protocol
let merkleRoot: string

describe("Protocol", function () {
  before(async () => {
    ;[account1, account2, ...rest] = await ethers.getSigners()

    EMBToken = (await (await ethers.getContractFactory("EMBToken")).deploy("EMB Token", "EMB")) as EMBToken
    await EMBToken.deployed()
  })

  beforeEach(async () => {
    protocol = await (await ethers.getContractFactory("Protocol")).deploy(account1.address, EMBToken.address)
    await protocol.deployed()
  })

  describe("setup", () => {

    it("should deploy correctly", async () => {
      // if the beforeEach succeeded, then this succeeds
    })

  describe("Signature minting", () => {
    it ("TODO", async () => {
      throw new Error("TODO: add more tests here!")
    })
  })
})
```

## Deliverables

Use the provided contract and testing code to submit your Hardhat/Foundry/etc Solidity project. 

Your submission is expected to be bug-free, simple, and well-documented.

In particular, your deliverables are:

  - `Protocol.sol` must implement a `signatureMint` function which verifies a caller-provided signature that has been signed by an address provided in `Protocol.sol`'s constructor. Once verified, the contract should send the minter their correct amount of EMB.
  
  - `EMB.sol` must be modified to insure security and avoidance of any vulnerability or error while minting by users.

  - `protocol.spec.ts` must be working, tested and can be run easily without errors.

  - **You must submit a full test suite with high test coverage and video of how the project was made from scratch**

## How to submit

Please share your completed private Github repo with us

Thank you, and good luck!