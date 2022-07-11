With this new trend of writing smart contracts and all the developers that are jumping into the web3 space, it is important to make sure we not only develop smart contracts but we develop gas efficient, well written and secure smart contracts. Since these ones hold sometimes thousands if not millions of dollars, it becomes very important to develop well-written smart contracts.
In this article, we’re going to discuss some of the guidelines to develop secure and gas efficient smart contracts. 
This article will have 2 big parts which are going to be: security and gas optimization.
let’s dive in.


 ## Security

Since smart contracts hold millions if not billions of dollars, it becomes trivial to develop highly secure and well-written smart contracts. This includes well tested and audited smart contracts. To achieve this with smart contracts, we first have to change our mindset towards smart contract development. While in web2, the priority is to go to production as soon as possible with the ability to catch and fix bugs in production, it is very difficult and costly to change/fix smart contracts that are already deployed. 
In this first part, we’ll talk about a few key aspects to consider while writing smart contracts. 

- Lock contracts to specific compiler versions
As you write smart contracts, you always start by writing something similar to `pragma solidity ^0.8.0;`. This line of code specifies the version of the compiler that can compile your code. For best practice, always make sure you specify that version so that your smart contract does not get compiled by higher compiler versions which can introduce bugs. This helps to avoid/prevent unexpected bugs in our code. 

- Checks
Checks are conditions that are added to our smart contracts to make sure some standards are always followed to avoid unexpected behaviors. Imagine you’re writing a function called buyFood and this function is responsible for paying for a plate of food at a restaurant. Since no one is there on the blockchain to confirm that you paid for the food, your program should do the job for you. In this case you’d add a check to your function to make sure the user has paid for the plate he is eating. This is just an  example that shows how important checks are in our code. In solidity we have different types of checks such as require, modifier,etc. The best use of checks can help you avoid attacks or prevent the attacker from accessing some parts of your code. Simple checks can avoid your code to fall for popular attacks like reentrancy gard. 

- Oracles 
While building applications, we need external data. But in the blockchain ecosystem, smart contracts don’t have access to external information. To make sure, we don’t introduce bugs in our codes, we use oracles to access outside data and bring it to our smart contracts in a decentralized manner. In order to avoid bugs while reading external data, we need to use oracles. Imagine, we are building an app that needs to have access to temperature data in London at exactly 3pm. The problem here is that userA can have 24degrees, userB has 28degrees, etc. Now, while computing this on the blockchain, there will be no consensus. To  avoid all those bugs or vulnerabilities, we need to use oracles. 

- Randomness 
It is very hard to generate random numbers in a decentralized architecture. It is even harder to do that using different mechanisms(blockHeight + timestamp, etc.). To avoid creating random bugs in our code, it is better to use services that provide randomness in a decentralized manner. To achieve this, a protocol like Chainlink will be highly recommended. 

- Code flow 
While writing code for decentralized apps, we should be very careful on which step we’re going through before the other. Here a recommended behavior would be to put checks before any on-chain manipulation or update states before doing any transfer. Bad code flow has been at the root of so many different attacks that led to millions of dollars lost. So, it is very important to think about code flow and code operations while writing smart contracts. The less risky operations should come first. Do not only think about your contract the way you want your frontend to interact with it. But do the security part while having in mind that your contract can be called from anywhere not only in your frontend. 

- Utilize audited code 
As developers, before coding any solution, we should first look if there are no solutions that exist to our problem. And the good thing with web3 is that so many projects and protocols are leaving their work open-source for everyone to look into or contribute to. Openzeppelin is one of the favorite repositories out there that has tested and audited code that you can use safely instead of redoing the same process yourself and sometimes introduce new bugs into your code. It is a smart choice to make use of these boilerplates tested by experts. 
Disclaimer: Make sure you double-check the code by yourself before using it and understand what it does.

- Minimize complexity
Many developers agree that complexity introduces more ambiguity in the code. The goal of writing code should be to write simple code that can be understood and modified anytime. Once you write very complex code, there are chances that you might be missing something or introducing something that might be very hard to understand for another developer working on your code. A good advice would be to write simple and easy to understand code so that you don’t introduce ambiguity, bugs and vulnerabilities in your project. 

- Prepare code for attacks
Since no one writes perfect, bug-free code, it is important to write code that can survive hard times. While building our smart contracts, we need to write code that can be ready to handle bugs and attacks. This pattern is a little bit challenging because of immutability on the blockchain. Once code is deployed on the blockchain, it becomes non-changeable. Because of that, we can add options of emergency-stop to our contract or we can make upgradable contracts or restrict certain access to certain addresses,etc. There are quite a number of good practices and techniques to apply to our contract to make it a little bit ready for attacks. 


## Gas optimization 


At this point, we already know that to deploy and write to the blockchain, we need to pay a certain amount of crypto(tokens) called gas fees. Sometimes these gas fees go up to thousands of dollars on the ethereum blockchain. 
Paying that much money to interact with a protocol is a little bit wrong(bad experience) and especially if we want to onboard many people to web3. So, we need to reduce that cost as much as we can. That should be in our mind while building these apps or writing these smart contracts. 
Let’s see some good practices about reducing gas fees in our smart contracts. 

- Variables
Solidity is a statically-typed language. This means every variable is assigned a type before usage. This type allocates memory or storage for that variable. For global variables in solidity, it is better to store on-chain what you’ll only use and assign the right storage to it. Since writing to the blockchain is costly, we need to minimize that cost. If you have  a variable `uint256 myNumber` and maybe you will not need a uint256, a better practice is to shrink that down to what you’ll need for your dapp. 
Another point that might save you a little bit of gas is the fact that you don’t always need to initiate your variable with an initial value. Let’s say you have something like `uint256 myNumber = 0`. Instead of writing it like that, you could have just written:`uint256 myNumber` and that would start at Zero.  It is worth mentioning that while using a Struct, you always need to use the right variable type to save a little bit of storage.

- Loops 
As we have been mentioning through this whole article, writing to the blockchain is costly, so to avoid or reduce on that cost we always have to make sure we can reduce the number of writing actions we perform. A good example would be to use a repetitive action like a loop to write to the blockchain. Imagine we have a loop that increments the number of elements in a global array. If we access that array directly and add all iterations, that would cost a tremendous amount of money. What we could do to reduce that cost would be to copy our global array into a new variable in memory, then iterate through our loop. At the end of the loop, we take our new array and update it in the global array variable. That way, instead of writing to the blockchain so many times, we’ll just need to do it once while updating our global variable with the result of the iteration. 

- Function visibility 
So many discussions have proven that while writing functions in solidity, we can save an amount of gas by making the function visibility “external” instead of “public”.

Short messages in require()
Again, having in mind that storage is expensive on the blockchain, we need to minimize what we store. A general structure of a require function is:`require(condition, “message”)`. We need to minimize the length of our message so that it does not take up much space. 

- Don’t store it on the blockchain 
The amount of things we store on-chain should be very very limited. It doesn’t make sense to store a whole movie on-chain yet we have services that can handle that perfectly. Everything stored on-chain should have a specific reason for choosing on-chain storage over off-chain storage. 

- Clean code 
To avoid unnecessary high costs in gas, we need to keep our code clean. Unused code should be deleted so that it doesn’t take much space. Variables declared but not used should also be removed from our code. Also the part of our code that doesn’t require to be executed on-chain should be reconsidered and preferably put and executed off-chain. 

This was  a long article ! 

We have covered some of the solidity/smart contracts best practices to help you write not only secure code but also gas efficient code as well. These practices are one of the fundamentals and the ones to look at first while writing smart contracts. It is worth mentioning that we also have other best practices that are not mentioned in this article or might be discovered later after this article is published. 
If you get any other best practice, drop that in the comments so that we can all learn them together. 

Until next time, keep #BUIDLING. 

