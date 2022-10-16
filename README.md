# Genesis Character Event Contract

### Contract Basics

* Contract should sort queue array by highest amount of SOL contribution as priority and ascending based on submission time.
* Upon deployment set `owner` to contract deployer.

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

### Write functions:

Can be called by `owner` only.

```
addWinner
```
Takes the top user submission and moves it to the winner array. SOL amount for that user/row is transfered to deployer/owner of contract. If there is a conflict between more than one, take the one which is timestamped earlier. 
```
end
```
Stops taking in new submissions and returns outstanding SOL to wallets.
