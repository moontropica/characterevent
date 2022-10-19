# Genesis Character Event Contract

### Contract Basics

* Contract should sort queue array by highest amount of SOL contribution as priority and ascending based on submission time.
* Upon deployment set `owner` to contract deployer.
* Mirror blockchain arrays to local DB for efficiency.

## Queue Array
|Address|SOL|ImageURL|
|-------|---|--------|

## Winner Array
|Address|SOL|ImageURL|
|-------|---|--------|

### Read functions:

```
getOwner
```
Prints the owner/deployer of the contract.

```
getTotalUsers
```	
Gets the total amount of submissions in queue array + winner array.

```
getTopUser
```	
Displays the top user and amount of SOL submitted.

```
getTop5
```
Displays the top 5 submissions and amount of SOL submitted for each.

### Write functions (Admin):

Can be called by `owner` only.

```
addWinner
```
Takes the top user submission and moves it to the winner array. SOL amount for that user/row is transfered to deployer/owner of contract. If there is a conflict between more than one, take the one which is timestamped earlier. 
```
end
```
Stops taking in new submissions and returns outstanding SOL in the queue array back to the wallet address it came from.

### Write functions (Regular User):

```
submit
```
Adds the submission to queue.

address (address), sol (uint256), imageURL (string)

Connected Wallet:

* if SOL contribution `> 0` & image is uploaded
  * request approval of funds transfer
  * transfer SOL requested to smart contract
  * upload image file locally
  * add details to queue
    * address
    * sol
    * imageURL
  * add details to local DB
  
* if SOL contribution `= 0` & image is uploaded
  * add details to queue array
  * add details to local DB
  
* if no image is attached and Submit is clicked throw an error modal
  
* if `address` is already in queue, show modal and allow modification to image or add SOL:
````
This wallet has already submitted a character request.

OK
````
OK is selected, use `modify` function to allow adding SOL and updating image.

```
modify
```
Edits the queue array.

sol (uint256), imageURL (string)

* Wallet needs to match an address in the queue array.
* SOL value should only increase.
  * Error Modal: You can only increase your SOL position.
