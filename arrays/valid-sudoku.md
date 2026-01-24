# Valid Sudoku
# Date 23-01-2026
# Problem link
- https://leetcode.com/problems/valid-sudoku/description/
# Description
- A `9x9` sudoku table is given, we have to check if it is valid
- Conditions are :-
  - no duplicate num in a row
  - no duplicate num in a col
  - no duplicate num in a box of `3x3`
- You don't have to account for number that are blank, to check if this sudoku is solvable, just check validity for above conditions
- Example
```bash
board=
[["5","3",".",".","7",".",".",".","."]
,["6",".",".","1","9","5",".",".","."]
,[".","9","8",".",".",".",".","6","."]
,["8",".",".",".","6",".",".",".","3"]
,["4",".",".","8",".","3",".",".","1"]
,["7",".",".",".","2",".",".",".","6"]
,[".","6",".",".",".",".","2","8","."]
,[".",".",".","4","1","9",".",".","5"]
,[".",".",".",".","8",".",".","7","9"]]

Output: true
```
# Approach
- use a `unordered_set` for rows, cols, and boxed, that too separate for each row, col and box
- iterate over the 2d array
- find boxIndex using `(row/3) * 3 + (col/3)`
- if current element found in current set(row, col or box), return false
- and keep adding them in their set
- return true at last if nothing collides
```cpp
class Solution {
  public:
	bool isValidSudoku(vector<vector<char>> &board) {
		unordered_set<char> row[9];
		unordered_set<char> col[9];
		unordered_set<char> block[9];
		for (int i = 0; i < 9; i++) {
			for (int j = 0; j < 9; j++) {
				if (board[i][j] == '.') {
					continue;
				}
				char value = board[i][j];
				int bi = (i / 3) * 3 + (j / 3);
				if (row[i].count(value) || col[j].count(value) ||
					block[bi].count(value)) {
					return false;
				}
				row[i].insert(value);
				col[j].insert(value);
				block[bi].insert(value);
			}
		}
		return true;
	}
};
```
- Time complexity : O(n<sup>2</sup>)
- Space complexity : O(9x9x3) ~ O(1) potentially since sudoku of `9x9`
***