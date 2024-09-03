# Chess Engine To-do

The purpose of this page is to provide a sequential list of steps that should lead you in the direction of writing a Chess bot from scratch. Many of these steps can be swapped, or entire chapters can be completed out of order, and all of those are valid choices. Each step is given a number in a sequence to provide a possible order of completion for simplicity. While it is the intention of this page to be language-agnostic, there are situations in which the approaches listed can not be applied by all or even the majority of programming languages. Coding is a creative experience, so feel free to deviate and take your own approach.

## Chapter 1: Board Representation

[There are many different ways to represent a chess board in code](https://www.chessprogramming.org/Board_Representation), but this guide will focus specifically on an approach utilizing [bitboards](https://www.chessprogramming.org/Bitboards).

1. **Implement bitboards**

Depending on your language and personal choice, a bitboard can be implemented in a couple different ways. You can simply treat all unsigned 64 bit integers as a bitboard, and all method arguments can be treated as such; [you could create an alias for an unsigned 64 bit integer](https://www.geeksforgeeks.org/typedef-in-c/); [you could create a struct with one field](https://doc.rust-lang.org/book/ch19-04-advanced-types.html#using-the-newtype-pattern-for-type-safety-and-abstraction); or some other strategy. Choose one of these based off of what is available in your language and personal preference.

2. **Write bitboard helper functions**

There are many different functions that can make working with bitboards a lot easier. While they are not all strictly necessary to working with bitboards, all of the following methods are worth reading into:

   - `is_empty()` (returns true if there are no set bits in the bitboard)
   - `is_one()` (returns true if there is only one bit set in the bitboard - this is effectively a [`is_power_of_two()`](https://www.geeksforgeeks.org/program-to-find-whether-a-given-number-is-power-of-2/) algorithm)
   - `pop_count()` (returns the total number of set bits in the bitboard - see [Chess Programming Wiki on the topic](https://www.chessprogramming.org/Population_Count))
   - `lsb1b()` (returns a bitboard [with only the least significant bit set](https://www.chessprogramming.org/General_Setwise_Operations#Least_Significant_One))
   - `nort(), east(), sout(), west()` ([directional shifting operations](https://www.chessprogramming.org/General_Setwise_Operations#Shifting_Bitboards))
   - `print()` (some way to visually print or transcribe the 2d bitboard for debugging purposes)

It is worth noting that this is under the assumption that your language and bitboard representation means you can already perform [bitwise operations](https://en.wikipedia.org/wiki/Bitwise_operation) on it. If for some reason this is not possible, it is worth either overloading the bitwise operators or creating functions mimicking them.

It is also suggested that bitboard constants are made to represent all files, ranks, long diagonals, starting pieces, and possibly more as needed.

3. **Move generation functions**

After implementing your bitboards and its functions, it is time to create move generation algorithms for each piece in the game. The basic concept is: for each piece you are given an origin square, and you will return all possible squares that piece can move to. For bitboards, we usually relinquish the responsibility of determining whether a move is truly legal for the sake of pins and checks, and we only generate the [pseudo-legal destination squares](https://www.chessprogramming.org/Move_Generation#Pseudo-legal).

For [knights](https://www.chessprogramming.org/Knight_Pattern) and [kings](https://www.chessprogramming.org/King_Pattern) this means the solution is relaively trivial, and can be easily implemented with either bit-shifting operations, or a look-up table.

For pawns, there are many things that must be taken into account, such as direction, double-pushes, and en passant. Implementing this simply means that the `pawn_moves()` method signature must be overly-abundant in its arguments. It is recommended for this step to look at other engines.

For bishops, rooks, and queens, there are many possible approaches to implement. It is recommended to first go with your intution and experiment on how to generate the possible pseudo-legal attacking squares, as there are [many, many different, efficient ways to implement sliding piece move generation algorithms](https://www.chessprogramming.org/Sliding_Piece_Attacks), and they can be quite difficult to comprehend and implement.

It is recommended to, if possible, first write unit tests for all of these move generation functions, and then implement the simplest solution for all pieces. Once you have something working, you can come back and optimize once you begin writing board traversal and `perft()` functions later.

4. **Initial board representation**

5. **`from_fen()` function**

6. **`make_move()` and `unmake_move()`**

7. **Legal move validation and `perft()` functions**
