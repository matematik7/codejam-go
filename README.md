# codejam-go [![Build Status](https://travis-ci.org/matematik7/codejam-go.svg?branch=master)](https://travis-ci.org/matematik7/codejam-go)

Some helper stuff for codejam competition in go. See example.

To enable pprof images install:
```
sudo apt-get install graphviz
```


## input

Reads whitespace separated stuff from input file

- **input.String()** - string input
- **input.Bytes()** - []byte input
- **input.Int()** - int input (64-bit usually)
- **input.Float()** - float64 input
- **input.BigInt()** - \*big.Int input
- **input.Digits()** - split digits without space to []int slice
- **input.SliceInt(n)** - *n* ints to integer.Slice
- **input.SetInt(n)** - *n* ints to integer.Set
- **input.MultiSetInt(n)** - *n* ints to integer.MultiSet
- **input.SliceTupleFromInts(n, m)** - *n* tuples of *m* ints to SliceTuple
- **input.SliceTupleFromFloats(n, m)** - *n* tuples of *m* floats to SliceTuple
- **input.SliceTupleFromStrings(n, m)** - *n* tuples of *m* strings to SliceTuple
- **input.GridInt(y, x)** - *y* rows and *x* cols to integer.Grid, first is row index
- **input.SliceFloat(n)** - *n* floats to []float64
- **input.GridFloat(y, x)** - *y* rows and *x* cols to [][]float64, first is row index
- **input.SliceString(n)** - *n* strings to []string
- **input.SliceBytes(n)** - *n* []byte words to [][]byte


## output

Writes output after **Case #n:**, beginning space and trailing newline are provided if necessary.

Output to solution file:
- **output.Print(...interface{})** - prints all, spaces are added between operands when neither is a string
- **output.Println(...interface{})** - prints all, spaces are always added between operands and a newline is appended
- **output.Printf(format, ...interface{})** - prints with format string

Output to console:
- **output.DebugCase()** - prints case number, input and output
- **output.Debug(...interface{})** - first calls *DebugCase()*, then prints all, spaces are added between operands when neither is a string
- **output.Debugf(format, ...interface{})** - first calls *DebugCase()*, then prints with format string
- **output.Fatal(...interface{})** - same as *Debug()*, but terminates
- **output.Fatalf(format, ...interface{})** - same as *Debugf*, but terminates
- **output.Periodic(...interface{})** - prints all only every second, for fast loops, spaces are added between operands when neither is a string
- **output.Periodicf(...interface{})** - prints with format string only every second, for fast loops
- **output.PeriodicInt(a)** - prints integer *a* only every second, for very fast loops, avoids memory allocation for interface{}
- **ouptut.PeriodicCount()** - increases internal count every call, prints only every second

Output to chart (draws a png chart per testcase):
- **output.Point(x, y)** - chart point with float64 coordinates
- **output.PointInt(x,y)** - chart point with int coordinates

Testing asserts:
(all asserts have optional fatal bool parameter, that can be set to terminate if mistake is encountered)
- **output.AssertByteCount(byte, count, fatal)** - check if output has *count* number of *byte*-s
- **output.AssertCount(count, fatal)** - check if output has *count* bytes


## integer

Useful function for integers

- **integer.MAX** - maximum int can hold
- **integer.MIN** - minimum int can hold
- **integer.Min(...int)** - returns minimal from the given ints
- **integer.Max(...int)** - returns maximal from the given ints
- **integer.Abs(a)** - returns absolute value of a
- **integer.Ceil(a, b)** - divides a by b and rounds the result up
- **integer.Range(max)** - python style range, return slice of ints from *0* to *max-1*
- **integer.Range(min,max)** - python style range, return slice of ints from *min* to *max-1*
- **integer.Range(min,max,step)** - python style range, return slice of ints from *min* to *max-1* with step spacing
- **integer.Gcd(...int)** - return greatest common divider of given ints
- **integer.Lcm(...int)** - return least common multiple of given ints
- **integer.Pow(a,b)** - returns a to the power b
- **integer.Log10(a)** - returns log base 10 of a
- **integer.Log2(a)** - returns log base 2 of a

### integer.Set

Set implementation for integers (using map[int]struct{})

- **ms := integer.NewSet(...int)** - construct Set from given ints
- **ms.Copy()** - returns independent copy of Set
- **ms.Contains(a)** - returns true if a is in Set
- **ms.ContainsAll(...int)** - returns true if all given ints are in Set
- **ms.ContainsAny(...int)** - returns true if any of given ints is in Set
- **ms.Len()** - returns number of elements in Set
- **ms.Insert(...int)** - insert all given ints in Set
- **ms.Remove(...int)** - remove given ints from Set
- **ms.Clear()** - remove all elements from Set

### integer.MultiSet

Multiset implementation for integers (using map[int]int)

- **ms := integer.NewMultiSet(...int)** - construct MultiSet from given ints
- **ms.Copy()** - returns independent copy of MultiSet
- **ms.Contains(a)** - returns true if a is in MultiSet
- **ms.ContainsAll(...int)** - returns true if all given ints are in MultiSet
- **ms.ContainsAny(...int)** - returns true if any of given ints is in MultiSet
- **ms.Len()** - returns number of elements in MultiSet
- **ms.Count(a)** - returns number of a's in MultiSet
- **ms.Insert(...int)** - insert all given ints in MultiSet
- **ms.InsertN(a, n)** - insert n a's in MultiSet
- **ms.RemoveOne(...int)** - remove one of each given int from MultiSet
- **ms.RemoveAll(...int)** - remove all of each given int from MultiSet
- **ms.Clear()** - remove all elements from MultiSet

### integer.Slice

Slice are a few wrapper functions around []int

- **s := integer.NewSlice(n)** - zero slice with n elements
- **s.Fill(...int)** - fill slice with ints
- **s.String()** - for direct output.Print, space separated

### integer.Grid

Grid are a few wrapper functions around [][]int

- **g := integer.NewGrid(y, x)** - grid y rows by x cols
- **g.FillRow(i, ...int)** - fill i-th row with ints
- **g.FillCol(i, ...int)** - fill i-th col with ints
- **g.FillRowTuple(i, tuple)** - fill i-th row with ints from tuple
- **g.FillColTuple(i, tuple)** - fill i-th col with ints from tuple
- **g.GetRow(i)** - get i-th row in new Slice
- **g.GetCol(i)** - get i-th col in new Slice
- **g.Print(sep)** - returns string, *sep* separated cols, rows in lines
- **g.String()** - for direct output.Print, space separated cols, rows in lines
- **g.GoString()** - nice output for Debugf, | separted cols, use with output.Debugf("%#v", g)

## st

### st.Tuple

Tuple is a collection of ints, floats and strings

- **Tuple := st.IntTuple(...int)** - construct tuple from given ints
- **Tuple := st.FloatTuple(...float64)** - construct tuple from given floats
- **Tuple := st.StringTuple(...string)** - construct tuple from given strings
- **Tuple := t.Copy()** - returns independent copy of Tuple

### st.SliceTuple

- **slt := st.NewSliceTuple(...Tuple)** - construct SliceTuple from given tuples
- **slt := st.FromInts(c, ...int)** - construct SliceTuple from given ints, *c* ints per tuple
- **slt := st.FromFloats(c, ...float64)** - construct SliceTuple from given floats, *c* floats per tuple
- **slt := st.FromStrings(c, ...string)** - construct SliceTuple from given strings, *c* strings per tuple
- **slt := slt.Copy()** - returns independent copy of SliceTuple
- **slt := slt.CopySlice()** - returns copy of slice that contains pointers to same elements as original
- **slt.Prepend(...Tuple)** - prepend tuple(s) to slice
- **slt.Append(...Tuple)** - append tuple(s) to slice
- **slt.Insert(i, ...Tuple)** - insert tuple(s) on i-th place
- **slt.Remove(i)** - delete tuple at i
- **slt.RemoveFirst()** - delete first tuple
- **slt.RemoveLast()** - delete last tuple
- **slt.PrefixIntConst(...int)** - prefix all tuples with given ints
- **slt.PrefixFloatConst(...float)** - prefix all tuples with given floats
- **slt.PrefixStringConst(...string)** - prefix all tuples with given strings
- **slt.PrefixIntIndex()** - prefix all tuples with their slice index
- **slt.PostfixIntConst(...int)** - postfix all tuples with given ints
- **slt.PostfixFloatConst(...float)** - postfix all tuples with given floats
- **slt.PostfixStringConst(...string)** - postfix all tuples with given strings
- **slt.PostfixIntIndex()** - postfix all tuples with their slice index
- **slt.Reverse()** - reverse slice
- **slt.Get(i)** - returns i-th tuple
- **slt.First()** - return first tuple
- **slt.Last()** - return last tuple
- **slt.Swap(i, j)** - swap i-th and j-th tuple
- **slt.Len()** - return length of slice
- **slt.SortOrder(...Sorter)** - set sort order with sorters (see st.Sorter section)
- **slt.Sort()** - sort based on sort order
- **slt.HeapInit()** - initialize heap
- **slt.HeapPop()** - remove min and return it from heap
- **slt.HeapPush(Tuple)** - add Tuple to heap
- **slt.HeapFix(i int)** - fix heap after *i* was changed

### st.Sorter

- **s := IntAsc(c)** - sort by *c* int ascending
- **s := IntDesc(c)** - sort by *c* int descending
- **s := FloatAsc(c)** - sort by *c* float ascending
- **s := FloatDesc(c)** - sort by *c* float descending
- **s := StringAsc(c)** - sort by *c* string ascending
- **s := StringDesc(c)** - sort by *c* string descending

## stringmap

A simple library for unique integer to string mapping for using strings in integer.MultiSet and graph stuff

- **sm := stringmap.New()**
- **i = sm.Int(string)** - get index for string
- **str = sm.Get(int)** - get string for index

## twod

2d library, everything to do with 2d vectors and stuff

- **AngleDiff(a1, a2)** - returns difference between angles in radians that is always between 0 and 2PI

### twod.Vector

2d vector represented as []float64, x is 0 and y is 1

- **v := NewVector(x, y)** - construct new vector
- **v.Len()** - vector length |v|
- **v := v.Sub(v1)** - returns vector v-v1
- **v.Dot(v1)** - returns dot product v.v1
- **v.Atan2()** - calculates vector angle using atan2 function
