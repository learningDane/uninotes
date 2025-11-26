#self-taught 
Forsyth–Edwards Notation (FEN) is a standard notation for describing a particular board position of a chess game. The purpose of FEN is to provide all the necessary information to restart a game from a particular position.

FEN is based on a system developed by Scottish newspaper journalist David Forsyth. His system became popular in the 19th century, then Steven J. Edwards extended it to support its use by computers. FEN is defined in the "Portable Game Notation Specification and Implementation Guide". In the Portable Game Notation for chess games, FEN is used to define initial positions other than the standard one.

>FEN does not provide sufficient information to decide whether a draw by threefold repetition may be legally claimed or a draw offer may be accepted; for that, a different format such as Extended Position Description is needed
# Definition
A FEN record defines a particular game position, all in one text line and using only the ASCII character set. A text file with only FEN data records should use the filename extension `.fen`.

A FEN record contains six fields, each separated by a space. The fields are as follows:
1. **Piece placement data**: Each rank is described, starting with rank 8 and ending with rank 1, with a "/" between each one; within each rank, the contents of the squares are described in order from the a-file to the h-file. Each piece is identified by a single letter taken from the standard English names in algebraic notation (pawn = "P", knight = "N", bishop = "B", rook = "R", queen = "Q" and king = "K"). White pieces are designated using uppercase letters ("PNBRQK"), while black pieces use lowercase letters ("pnbrqk"). A set of one or more consecutive empty squares within a rank is denoted by a digit from "1" to "8", corresponding to the number of squares.
2. **Active color**: "w" means that White is to move; "b" means that Black is to move.
3. **Castling availability**: If neither side has the ability to castle, this field uses the character "-". Otherwise, this field contains one or more letters: "K" if White can castle kingside, "Q" if White can castle queenside, "k" if Black can castle kingside, and "q" if Black can castle queenside. A situation that temporarily prevents castling does not prevent the use of this notation.
4. **En passant target square**: This is a square over which a pawn has just passed while moving two squares; it is given in algebraic notation. If there is no en passant target square, this field uses the character "-". This is recorded regardless of whether there is a pawn in position to capture en passant. An updated version of the spec has since made it so the target square is recorded only if a legal en passant capture is possible, but the old version of the standard is the one most commonly used.
5. **Halfmove clock**: The number of halfmoves since the last capture or pawn advance, used for the fifty-move rule.
6. **Fullmove number**: The number of the full moves. It starts at 1 and is incremented after Black's move.
