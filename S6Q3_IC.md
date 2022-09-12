# Tutorial S6 In-Class Q3
```
Solution
function perm(lst) {
    return is_null(lst)
        ? list(null)
        : accumulate(append, null,
            map(x => map(p => pair(x, p),
                            perm(remove(x, lst))),
                lst));
}
```

Note that the result of perm is a list of lists, so individual elements are lists

```
map(p => pair(x, p),
        perm(remove(x, lst)))
```
By _wishful thinking_,
`perm(remove(x, lst))` returns all the permutation of `lst`\\`x` (`lst` excluding `x`).

`map(p => pair(x, p), perm(remove(x, lst)))` thus appends `x` to the head of all the permutations of `lst`\\`x`. For the rest of the write up, we will refer to these permutations as  P<sub>X</sub> (Permutations starting with x).

Notice that  P<sub>X</sub> contains _all_ the permutations starting with `x` since we fully permutated `lst`\\`x`. Thus to generate all the permutations, we simply need to generate P<sub>X</sub> for each x in the original `lst`

```
map(x => map(p => pair(x, p),
                perm(remove(x, lst))),
    lst));
```
Simplifying `map(p => pair(x, p), perm(remove(x, lst)))`, we have <code>map(x => P<sub>X</sub> , lst)</code>.
Thus, by generating P<sub>X</sub> for each `x` in `lst` we have all the permutations required. However, it will just be a list of P<sub>X</sub>, which will be a list of list of permutations. ie. [P<sub>X1</sub>, P<sub>X2</sub>, P<sub>X3</sub>, ... P<sub>Xn</sub>] where xi is the ith element in the `lst`




```
accumulate(append, null,
            map(x => map(p => pair(x, p),
                            perm(remove(x, lst))),
                lst));
```
Simplifying this statement, we have `accumulate(append, null, [P<sub>X1</sub>, P<sub>X2</sub>, P<sub>X3</sub>, ... P<sub>Xn</sub>])` which is simply appending all the P<sub>Xi</sub> together starting from P<sub>Xn</sub>.



