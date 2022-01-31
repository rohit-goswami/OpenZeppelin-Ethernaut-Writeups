# Hello Ethernaut
> This level walks you through the very basics of how to play the game.

This is very basic challenge of ethernaut CTF, you just need to read and follow the instructions carefully.

Challenge: 
> To add metamask into your browser, adding test ETH to it and authencticate into the contract by finding the password.

Steps to follow: 

1.  First create **level instance** to interact with the contract. Then write commands in console window.
2.  Type ```contract.info()```: Expand the result to find next step to do ie  "You will find what you need in info1()."
3.  ```contract.info1()```: "Try info2(), but with \"hello\" as a parameter"
4. ```contract.info2("hello")```: "The property infoNum holds the number of the next info method to call."
5. ```contract.infoNum()```: expand the result and you'll see mentioned  number is 42, so we need to call info42 next.
6. ```contract.info42()```: "theMethodName is the name of the next method." - next method name revealed.
7. ```contract.theMethodName()```: "The method name is method7123949." - method to call next.
8. ```contract.method7123949()```: "If you know the password, submit it to authenticate()." - do we really know the password
? Don't worry we can find it. Remember we can check the contract interface by calling abi. 
9. ```contract.abi```: look we have password method, so let's try calling it next. also note that we have authenticate method too.
10. ```contract.password```: Yippi! we got the password in result mentioned as "ethernaut0". Try authenticating the contract next.
11. ```contract.authenticate("ethernaut0")```: confirm the metamask transaction and wait for few seconds.
12. Now submit the instance, confirm the transaction and wait for completion.

> Further learning: 
 https://ethereum.stackexchange.com/questions/234/what-is-an-abi-and-why-is-it-needed-to-interact-with-contracts/235
 https://medium.com/@houzier.saurav/calling-functions-of-other-contracts-on-solidity-9c80eed05e0f
 https://medium.com/mycrypto/the-ethereum-virtual-machine-how-does-it-work-9abac2b7c9e




Congrats! we did it. Lets move on to the real challenges.  
![image](https://user-images.githubusercontent.com/15854015/151848427-94229470-8436-49d9-8c3b-2617f0e43409.png)
