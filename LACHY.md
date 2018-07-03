
# foldl, foldr and foldl'

foldl = "evaluate from the left"
foldr = "evaluate from the right"

Same as the wind: northerly = from the north
note that the expansion runds differently from the actual evaluation

## foldr

```haskell
foldr f z [] = z
foldr f z (x:xs) = f x (foldr f z xs)

foldr (+) 0 [1, 2, 3, 4, 5] -->
1 + (foldr (+) 0 [2, 3, 4, 5])
1 + (foldr (+) 0 [2, 3, 4, 5]) -->
1 + (2 + (foldr (+) 0 [3, 4, 5])) -->
1 + (2 + (3 + (foldr (+) 0 [4, 5]))) -->
1 + (2 + (3 + (4 + (foldr (+) 0 [5])))) -->
1 + (2 + (3 + (4 + (5 + (foldr (+) 0 []))))) -->
1 + (2 + (3 + (4 + (5 + (0))))) -->
1 + (2 + (3 + (4 + (5)))) -->
1 + (2 + (3 + (9))) -->
1 + (2 + (12)) -->
1 + (14) -->
15
```

## foldl

```haskell
foldl f z [] = z
foldl f z (x:xs) = foldl f (f z x) xs

foldl (+) 0 [1, 2, 3, 4, 5] ->
foldl (+) (0 + 1) [2, 3, 4, 5] ->
foldl (+) ((0 + 1) + 2) [3, 4, 5] ->
foldl (+) (((0 + 1) + 2) + 3) [4, 5] ->
foldl (+) ((((0 + 1) + 2) + 3) + 4) [5] ->
foldl (+) (((((0 + 1) + 2) + 3) + 4) + 5) [] ->
(((((0 + 1) + 2) + 3) + 4) + 5) ->
((((1 + 2) + 3) + 4) + 5) ->
(((3 + 3) + 4) + 5) ->
((6 + 4) + 5) ->
(10 + 5) ->
15
```

## why does foldl reverse a list?
```haskell
foldl (flip (:.)) Nil (1 :. 2 :. 3 :. Nil) ->
foldl (flip (:.)) (1 :. Nil) (2:. 3:. Nil) ->
foldl (flip (:.)) (2 :. 1 :. Nil) (3 :. Nil) ->
foldl (flip (:.)) (3 :. 2:. 1 :. Nil) Nil ->
(3:. 2:. 1:. Nil)
```


