# Genesis Character Event Contract

## Write Functions

```
setOwner
```
<b>Permissions:</b> Can be called by current `owner` only.

Changes the owner of the contract.

```
selectWinner
```
<b>Permissions:</b> Can be called by `owner` only.

#### What it does:
Searches through the Queue Array and searches for the highest SOL contribution wallet, if there is a draw, it should take the one with earlier timestamp in ascending order (older to newer). Moves the selection to a "Selected Array" and withdraws the SOL contribution from the smart contract to the `owner` address.

```
end
```
<b>Permissions:</b> Can be called by `owner` only.

Stops taking in new submissions and returns outstanding SOL in the Queue Qrray back to the wallet addresses it came from.

```
submit
```
<b>Permissions:</b> Can be called by anybody.

Submits a wallet address into the Queue Array.

```
approve
```
<b>Permissions:</b> Can be called by anybody.

Approves spending of SOL for contributions.

```
addSol
```
<b>Permissions:</b> Can be called by anybody but requires approve function to be called first.

Transfers a user specified amount of SOL to the smart contract.

## Read Functions

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
Displays the top `address` based on the amount of SOL contributed.

```
getTop5
```
Displays the top 5 submissions and amount of SOL submitted for each.

```
getWinners
```
Displays the winner addresses.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------

### Contract Basics

* Contract will store a list of submissions signed by public wallets (Phantom Wallet)
* Contract will prioritize submissions with SOL attached then timestamped (ascending)
* Contract should allow modification of submissions 
  * Increase of SOL contribution
  * Updating of image
* Submissions made with referrals get 10 `RefPoints` added to their wallet 


* Have an API that displays the most recent winners

## Data to Store On-Chain

|Address|SOL|
|-------|---|

## Data to Store Off-Chain

|Address|SOL|ImageURL|RefPoints|
|-------|---|--------|---------|

* Contract should sort queue array by highest amount of SOL contribution as priority and ascending based on submission time.
* Upon deployment set `owner` to contract deployer.
* Mirror blockchain arrays to local DB for efficiency.

## Queue Array (On-chain)
|Address|SOL|
|-------|---|

## Winner Array (On-chain)
|Address|SOL|
|-------|---|

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
