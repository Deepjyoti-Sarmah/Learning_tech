
## A simple blockchain build using Go
Does not have Prove of Work yet

#### How it is Designed ?

#### 4 structs
Book  <-- BookCheckot  <-- Block <-- Blockchain

Book {
	id , title, author, publishdate, isbn
}

BookCheckout {
	bookid, user, checkoutdate , isgenesis
}

Block {
	Prevhash, Position, data, timestamp, hash
}

Blockchain {
	collection of Blocks
}

Create new Book 

new Blockchain -> write block -> Add Block -> create Block  -> validate block -> generate hash -> validhash                                                    
create Block -> is Genesis





