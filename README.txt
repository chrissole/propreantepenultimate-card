True Propreantepenultimate Card Specification
---------------------------------------------

§1              Game State:
§1.1.1              - the current active player
§1.1.2                (initially one to the left of the dealer)
§1.2.1              - int AV (attack value)
§1.2.2                (initially 0)
§1.3.1              - int MV (move value)
§1.3.2                (0)
§1.4.1              - bool CW (clockwise)
§1.4.2                (true)
§1.5.1              - bool FC (first card this turn)
§1.5.2                (true)
§1.6.1              - booleans RM, RM2 (require suit / rank matches)
§1.6.2                (true)
§1.7.1              - bool B (bridging 3s and 7s)
§1.7.2                (false)
§1.8.1              - PW (prevent wins)
§1.8.2                (false)

§2              Dealing:
§2.1              Now the top card from the pile is placed on the table.
§2.1              If that card has rank 2 or 5, set AV to that card’s rank.
§2.2              If the rank is 10, set MV to 1.
§2.3              If the rank is Jack, set MV to 1 & CW to false.
§2.4              If the rank is Ace, set RM to false.
§2.5              Go to step 1.

§4              Card Matches:
§4.1              A card can be played as a type 1 match if:
§4.1.1.1            - if the two topmost cards both have rank 6:
§4.1.1.2                this card's doesn’t have rank 6
§4.1.2.1            - and, if RM is true:
§4.1.2.2              - the rank or suit of this card must match, or
§4.1.2.3              - if this card is a Queen of Hearts,
§4.1.2.4                  the top card must be a King,
§4.1.2.5              - or if it is a King of Hearts,
§4.1.2.6                  the top card must be a Queen.
§4.2              A card can be played as a type 2 match if:
§4.2.1.1            1.  It has the same rank as the
§4.2.1.2                  topmost or the penultimate card, or
§4.2.2.1            2.  Its rank is ±1 of the top or penultimate card’s rank,
§4.2.2.2                  wrapping at Ace, or
§4.2.3.1            3.  It has rank 3 or 7,
§4.2.3.2                  and the topmost or penultimate card
§4.2.3.3                  has rank 7 or 3 respectively,
§4.2.3.4                  and B is true, or
§4.2.4.1            4.  At least two cards have been played so far,
§4.2.4.2.1              the top two cards and the card to be played
§4.2.4.2.2                have a rank between 2 and 10 (inclusive),
§4.2.4.3                and either the
§4.2.4.3.1                - sum
§4.2.4.3.2                - difference
§4.2.4.3.3                - product
§4.2.4.3.4                - or quotient
§4.2.4.4.1              of the ranks of two of the three cards
§4.2.4.4.2.1              (top two cards from the pile
§4.2.4.4.2.2                and the card to be played)
§4.2.4.5                in any order
§4.2.4.6                is an integer equal to the remaining card’s rank, or
§4.2.5.1            5.  It is an Ace of Spades
§4.2.5.2                being played on a top or penultimate card
§4.2.5.3                with a non-numeric rank, or
§4.2.6.1            6.  The card's rank is equal to
§4.2.6.2                the number of topmost consecutive cards
§4.2.6.3                on the pile
§4.2.6.4                with identical ranks.

§4              Card Options:
§4.1.1            1.  Don't play a card.
§4.1.2                If FC is true:
§4.1.2.1                Draw Max(1, AV) cards
§4.1.2.2                Set AV to 0
§4.1.2.3                Set PW to false.
§4.1.3                Go to step 1.
§4.2.1.1          2.  FC must be true
§4.2.1.2                and AV must be 0.
§4.2.2                Play your hand without restrictions or effects.
§4.2.3                Draw as many cards as you had before.
§4.2.4                Go to step 1.
§4.3.1.1          3.  The card’s rank must be 2 or 5,
§4.3.1.2                and it can’t be the player’s last card.
§4.3.2                Increase AV by the card’s rank.
§4.4.1.1          4.  The card’s rank must be 3 or 7,
§4.4.1.2.1              and either it’s not playable as the player’s last card
§4.4.1.2.2                or AV mustn’t be 0.
§4.4.2                Decrease AV by this card’s rank.
§4.4.3.1.1            If AV is 0 or less:
§4.4.3.1.2              Set AV to 0
§4.4.3.2.1            otherwise:
§4.4.3.2.2              Set B to true
§4.4.4.1.1            If the preceding card’s rank is
§4.4.4.1.2                different from this card’s rank,
§4.4.4.2                it is 3 or 7,
§4.4.4.3                and FC is false:
§4.4.4.4                The active player can choose to set AV to 0.
§4.4.5.1              If the active player now has no cards and AV is not 0:
§4.4.5.2                Set PW to true and MV to 0
§4.5.1.1          5.  The card’s rank must be 10,
§4.5.1.2                it mustn’t be the player’s last card,
§4.5.1.3                and it must be a type 1 match.
§4.5.2.1              The active player chooses to either
§4.5.2.2.1              - increase
§4.5.2.2.2              - or decrease
§4.5.2.3              MV by 1.
§4.6.1.1          6.  The card must be a Jack
§4.6.1.2                and not the player’s last card.
§4.6.2                Set CW to its inverse.
§4.7.1.1          7.  The card must be an Ace,
§4.7.1.2                not the player’s last card,
§4.7.1.3                and AV must be 0.
§4.7.2.1              The player selects a suit
§4.7.2.2                to which this card’s suit changes.
§4.8.1.1          8.  AV must be 0,
§4.8.1.2                and it must be a type 1 match.
§4.8.2.1              If a card with rank between 2 and 10 (inclusive)
§4.8.2.2                is played horizontally:
§4.8.2.3                Set its rank to 11 minus the card's original rank.

§3              Step 1:
§3.1.1            If PW is false and any player has an empty hand:
§3.1.2              That player wins the game.
§3.2.1            The player Max(0, MV) steps of the current active player
§3.2.2              becomes the new active player,
§3.2.3              clockwise if CW is true or otherwise counterclockwise.
§3.3.1            If MV is positive, set it to 0.
§3.3.2            Increment MV.
§3.4              Set FC to true and B to false.

§5              Step 2:
§5.1              Choose any card option.
§5.2              Set RM2 to RM.
§5.3.1            If FC is false:
§5.3.2              If one of the options in §4.1.3-8 was selected:
§5.3.3                The card to be played must be valid as a type 2 match.
§5.3.4                Unless §4.2.2 was selected, set RM2 to false.
§5.4.1            If the requirements in the first sentence 
§5.4.2              of the selected option’s text can’t be fulfilled:
§5.4.3                Set RM to RM2.
§5.4.4                Go to step 2.
§5.5.1            Unless FC is false and option 1 was selected:
§5.5.2              RM, B and PW are reset to their initial values.
§5.6              Follow any remaining instructions of the selected option.
§5.7              Set FC to false and go to step 2.

§6              Final turns:
§6.1.1            Any player that says “Last Card” must draw a card
§6.1.2                unless this is desired by the player.
§6.2.1            A player can only play their last card
§6.2.2              if they said the second word of this game's name
§6.2.3              before the active player last changed.
§6.3.1            Any player who mispronounces "Propreantepenultimate Card"
§6.3.2              (including shortening it) must draw a card
§6.3.3                unless this is desired by the player.
