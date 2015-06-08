# True Propreantepenultimate Card Specification

§1                Game State consists of:
§1.1                - the current active player (initially one to the left of the dealer)
§1.2                - int AV (attack value) (initially 0)
§1.3                - int MV (move value) (0)
§1.4                - bool CW (clockwise) (true)
§1.5                - bool FC (first card this turn) (true)
§1.6                - bool RM (require suit / rank matches) (true)
§1.7                - bool B (bridging 3s and 7s) (false)
§1.8                - PW (prevent wins) (false)

§2                Now the top card from the pile is placed on the table.
§2.1              If that card has rank 2 or 5, set AV to that card’s rank.
§2.2              If the rank is 10, set MV to 1.
§2.3              If the rank is Jack, set MV to 1 & CW to false.
§2.4              If the rank is Ace, set RM to false.
§2.5              Go to step 1.

§3                Step 1:
§3.1              If PW is false and any player has an empty hand, they win the game.
§3.2.1            The player Max(0, MV) steps of the current active player becomes the new active player,
§3.2.2              clockwise if CW is true or otherwise counterclockwise.
§3.3.1            If MV is positive, set it to 0.
§3.3.2            Increment MV.
§3.4              Set FC to true and B to false.

§4                Step 2:
§4.1              The active player chooses one of the following options to play a card.
§4.2              If FC is false, the active player may only play a card if:
§4.2.1.1            1.  It has the same rank as the topmost or the penultimate card, or
§4.2.1.2            2.  Its rank is ±1 of the top or penultimate card’s rank, wrapping at Ace, or
§4.2.1.3            3.  It has rank 3 or 7, and the topmost or penultimate card has rank 7 or 3 respectively, and B is true, or
§4.2.1.4.1          4.  At least two cards have been played so far,
§4.2.1.4.2              the top two cards and the card to be played have a rank between 2 and 10 (inclusive),
§4.2.1.4.3              and either the
§4.2.1.4.3.1              - sum
§4.2.1.4.3.2              - difference
§4.2.1.4.3.3              - product
§4.2.1.4.3.4              - or quotient
§4.2.1.4.4              of the ranks of two of the three cards (top two cards from the pile and the card to be played)
§4.2.1.4.5              in any order
§4.2.1.4.6              is an integer equal to the remaining card’s rank, or
§4.2.1.5            5.  It is an Ace of Spades being played on a top or penultimate card with a non-numeric rank, or
§4.2.1.6            6.  The card's rank is equal to the number of topmost consecutive cards on the pile with identical ranks.
§4.2.2            Unless option (2) was selected, set RM to false.
§4.3.1.1          After the requirements of first sentence of the option text have been checked:
§4.3.1.2            Unless FC is false and option 1 was selected:
§4.3.1.3              RM, B and PW are reset to their initial values.
§4.3.2            Options:
§4.3.2.1.1          1.  Don't play a card.
§4.3.2.1.2              If FC is true:
§4.3.2.1.2.1              Draw Max(1, AV) cards
§4.3.2.1.2.2              Set AV to 0
§4.3.2.1.2.3              Set PW to false.
§4.3.2.1.3              Go to step 1.
§4.3.2.2.1          2.  FC must be true.
§4.3.2.2.2              Play your hand without restrictions or effects.
§4.3.2.2.3              Draw as many cards as you had before.
§4.3.2.2.4              Go to step 1.
§4.3.2.3.1.1        3.  The card’s rank must be 2 or 5,
§4.3.2.3.1.2              and it can’t be the player’s last card.
§4.3.2.3.2              Increase AV by the card’s rank.
§4.3.2.4.1.1        4.  The card’s rank must be 3 or 7,
§4.3.2.4.1.2.1            and either it’s not playable as the player’s last card
§4.3.2.4.1.2.2              or AV mustn’t be 0.
§4.3.2.4.2              Decrease AV by this card’s rank.
§4.3.2.4.3              If AV is 0 or less, set it to 0; otherwise set B to true.
§4.3.2.4.4.1            If the preceding card’s rank is different from this card’s rank,
§4.3.2.4.4.2              it is 3 or 7,
§4.3.2.4.4.3              and FC is false:
§4.3.2.4.4.4              The active player can choose to set AV to 0.
§4.3.2.4.5.1            If the active player now has no cards and AV is not 0:
§4.3.2.4.5.2              Set PW to true and MV to 0
§4.3.2.5.1.1        5.  The card’s rank must be 10,
§4.3.2.5.1.2              it mustn’t be the player’s last card,
§4.3.2.5.1.3.1            and, if RM is true,
§4.3.2.5.1.3.2              the rank or suit of this card must match.
§4.3.2.5.2              The active player chooses to either increase or decrease MV by 1.
§4.3.2.6.1.1        6.  The card must be a Jack
§4.3.2.6.1.2              and not the player’s last card.
§4.3.2.6.2              Set CW to its inverse.
§4.3.2.7.1.1        7.  The card must be an Ace,
§4.3.2.7.1.2              not the player’s last card,
§4.3.2.7.1.3              and AV must be 0.
§4.3.2.7.2              The player selects a suit to which this card’s suit changes.
§4.3.2.8.1.1        8.  AV must be 0,
§4.3.2.8.1.2.1            if the two topmost cards both have rank 6:
§4.3.2.8.1.2.2              this card's mustn't have rank 6
§4.3.2.8.1.3.1            and, if RM is true:
§4.3.2.8.1.3.2              the rank or suit of this card must match
§4.3.2.8.1.3.3.1            except if this card is a Queen of Hearts,
§4.3.2.8.1.3.3.2              in which case it can be played on any King,
§4.3.2.8.1.3.4.1            or if it is a King of Hearts,
§4.3.2.8.1.3.4.2              in which case it can be played on any Queen.
§4.3.2.8.2.1            If a card with rank between 2 and 10 (inclusive) is played horizontally:
§4.3.2.8.2.2              Set its rank to 11 minus the card's original rank.
§4.3.3            Set FC to false and go to step 2.

§5.1              Any player that says “Last Card” must draw a card.
§5.2.1            A player can only play their last card
§5.2.2              if they said the second word of this game's name
§5.2.3              before the active player last changed.