# Arrays Toolkit
- This doc contains some tips and tricks that I learned while solving array related question and based on different scenarios
# Start
- use `unordered_set` if you want to tackle duplicates in an array like [cont dup](./contains-duplicate.md), it can also be used for when we have to do continous lookup's like here [long cons seq.](./longest-consecutive-sequence.md)
- `unordered_map` 
  - can be useful for problems with repetitive calculation of something over and over, 
  - or storing results for likely similar results in future like [group angrm](./group-anagrams.md) or [top k freq.](./top-k-frequent-elements.md)
  - it can also used to save lookup time like in [2-sum](./two-sum.md) where we store values and there index in a umap;
- `prefix sum` is very helpful to build something on the go like in [prod excp self](./product-of-array-except-self.md) or we can also produce that prefix on the go without storing
- use `bucket sort` in a different way for [tok k freq.](./top-k-frequent-elements.md)
- many times dealing with strings we may use some different techniques
  - using a `vector<int> v(26, 0)` to determine anagrams
  - sorting strings, sorting makes many problems easy to solve but as always not a good idea to use them always
- sometimes you can't avoid the abvious extra space or time complaxity needed