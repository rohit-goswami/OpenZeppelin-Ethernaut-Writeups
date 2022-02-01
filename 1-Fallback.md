# Fallback


Read the contract code carefully

> Challenge : Claim the ownership of the contract and reduce its balance to 0.

  
Explore and understand 
>1. How to send ether when interacting with an ABI
>2. How to send ether outside of the ABI
>3. Converting to and from wei/ether units (see help() command)
>4. Fallback methods

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.6.0;

import '@openzeppelin/contracts/math/SafeMath.sol';

contract Fallback {

  using SafeMath for uint256;
  mapping(address => uint) public contributions;
  address payable public owner;

  constructor() public {
    owner = msg.sender;
    contributions[msg.sender] = 1000 * (1 ether);
  }

  modifier onlyOwner {
        require(
            msg.sender == owner,
            "caller is not the owner"
        );
        _;
    }

  function contribute() public payable {
    require(msg.value < 0.001 ether);
    contributions[msg.sender] += msg.value;
    if(contributions[msg.sender] > contributions[owner]) {
      owner = msg.sender;
    }
  }

  function getContribution() public view returns (uint) {
    return contributions[msg.sender];
  }

  function withdraw() public onlyOwner {
    owner.transfer(address(this).balance);
  }

  receive() external payable {
    require(msg.value > 0 && contributions[msg.sender] > 0);
    owner = msg.sender;
  }
}
```

Read the following resources before attempting the Hack: 
1. Truth About **Fallback funtion** : https://tinyurl.com/yckyejw2
2. Ether which is native currrency of Ethreum has several units
    * wei is smallest unit.
    * 1 ether = 1000000000000000000 wei.
    * “wei” are the smallest ether unit, and you should always make calculations in wei and convert only for display reasons.
    * Read more: https://tinyurl.com/4mfpzsrz

## Lets Hack it! 
To get ownership of the contract note these  
1. `contribute()` function
2. `receive()` – a payable fallback function

First of all request a level instance.

Lets looks at first method 

```solidity
function contribute() public payable {
    require(msg.value < 0.001 ether);
    contributions[msg.sender] += msg.value;
    if(contributions[msg.sender] > contributions[owner]) {
      owner = msg.sender;
    }
  }
```

In this function we can only get ownership if our contribution to the contract is more than the owner. constructor already sets contract owner contribution to 1000 Eth. So we must contribute more than that to get the ownership. But we got one more problem here, we can only contribute less than 0.001 eth per transaction due to `require(msg.value < 0.001 ether);` check. 
To beat the present owner’s contribution we need to send many times to flip 1000 Eth but we don’t have that much time so we will look for other method.

2.  calling fallback funtion 

```solidity
receive() external payable {
    require(msg.value > 0 && contributions[msg.sender] > 0);
    owner = msg.sender;
  }
```

We should bypass `require(msg.value > 0 && contributions[msg.sender] > 0);` check first.

Let's contribute some amount by typing in console and then wait for few seconds.
	`contract.contribute({value: toWei("0.0001")}) // using toWei() here.`
   
now we will send some amount to trigger fallback function.

`contract.sendTransaction({value: toWei("0.001")}) //fallback function is payable so it will be triggered.`

Bypass Successful. 
Bravo! We got the ownership of the contract.

check the ownership : `contract.owner() == player`

wait! The hack is not done yet. We have to withdraw all the funds of the contract and to do so we should call `withdraw()` function. 
Note withdraw function can only be called by the owner as it has onlyOwner modifier. We are owner now :P

call `contract.withdraw()`

submit the instance. 


 
