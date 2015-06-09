# True Propreantepenultimate Card Specification

__Game State:__  
1. the current active player (initially one to the left of the dealer)  
2. int AV (attack value) (initially 0)  
3. int MV (move value) (0)  
4. bool CW (clockwise) (true)  
5. bool FC (first card this turn) (true)  
6. booleans RM, RM2 (require suit / rank matches) (true)  
7. bool B (bridging 3s and 7s) (false)  
8. PW (prevent wins) (false)  

__Dealing:__  
1. Now the top card from the pile is placed on the table.  
2. If that card has rank 2 or 5, set AV to that card’s rank.  
3. If the rank is 10, set MV to 1.  
4. If the rank is Jack, set MV to 1 & CW to false.  
5. If the rank is Ace, set RM to false.  
Go to step 1.

__Card Matches:__  
A card can be played as a type 1 match if:  
1. if the two topmost cards both have rank 6: this card's doesn’t have rank 6  
2. and, if RM is true: the rank or suit of this card must match, or if this card is a Queen of Hearts, the top card must be a King, or if it is a King of Hearts, the top card must be a Queen.  

A card can be played as a type 2 match if:  
1. It has the same rank as the topmost or the penultimate card, or  
2. Its rank is ±1 of the top or penultimate card’s rank, wrapping at Ace, or  
3. It has rank 3 or 7, and the topmost or penultimate card has rank 7 or 3 respectively, and B is true, or  
4. At least two cards have been played so far, the top two cards and the card to be played have a rank between 2 and 10 (inclusive), and either the sum, difference, product or quotient of the ranks of two of the three cards (top two cards from the pile and the card to be played) in any order is an integer equal to the remaining card’s rank, or  
5. It is an Ace of Spades being played on a top or penultimate card with a non-numeric rank, or  
6. The card's rank is equal to the number of topmost consecutive cards on the pile with identical ranks.  

__Card Options:__  
1. Don't play a card. If FC is true, draw Max(1, AV) cards, set AV to 0, set PW to false and go to step 1.  
2. FC must be true and AV must be 0. Play your hand without restrictions or effects. Draw as many cards as you had before. Go to step 1.  
3. The card’s rank must be 2 or 5, and it can’t be the player’s last card. Increase AV by the card’s rank.  
4. The card’s rank must be 3 or 7, and either it’s not playable as the player’s last card or AV mustn’t be 0. Decrease AV by this card’s rank. If AV is 0 or less, set AV to 0, otherwise: Set B to true. If the preceding card’s rank is different from this card’s rank, it is 3 or 7, and FC is false: The active player can choose to set AV to 0. If the active player now has no cards and AV is not 0: Set PW to true and MV to 0  
5. The card’s rank must be 10, it mustn’t be the player’s last card,and it must be a type 1 match. The active player chooses to either increase or decrease MV by 1.  
6. The card must be a Jack and not the player’s last card. Set CW to its inverse.  
7. The card must be an Ace, not the player’s last card, and AV must be 0. The player selects a suit to which this card’s suit changes.  
8. AV must be 0, and it must be a type 1 match. If a card with rank between 2 and 10 (inclusive) is played horizontally: Set its rank to 11 minus the card's original rank.  

__Step 1:__  
1. If PW is false and any player has an empty hand: That player wins the game.  
2. The player Max(0, MV) steps of the current active player becomes the new active player, clockwise if CW is true or otherwise counterclockwise.  
3. If MV is positive, set it to 0.  
4. Increment MV.  
5. Set FC to true and B to false.

__Step 2:__  
1. Choose any card option.  
2. Set RM2 to RM.  
3. If FC is false: If one of the card options one to three was selected, the card to be played must be valid as a type 2 match. Unless card option two was selected, set RM2 to false.  
4. If the requirements in the first sentence of the selected option’s text can’t be fulfilled, set RM to RM2. Go to step 2.  
5. Unless FC is false and option 1 was selected, RM, B and PW are reset to their initial values.  
6. Follow any remaining instructions of the selected option.  
7. Set FC to false and go to step 2.  

__Miscellaneous:__  
1. Any player that says “Last Card” must draw a card.  
2. A player can only play their last card if they said the second word of this game's name before the active player last changed.  
3. Any player who mispronounces "Propreantepenultimate Card" (including shortening it) must draw a card.