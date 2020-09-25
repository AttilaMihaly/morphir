# [Visualization](index.html)

Visualization in technical terms is the mapping of the `Morphir IR` to `HTML`. Conveniently our main modeling language 
(`Elm`) was designed for that purpose and it's extremely good at it. So let's formalize this in `Elm` code:

```elm
visualization : ir -> Html msg
```

Different elements in the `IR` will map to different structures in `HTML`. On the highest level we can differentiate 
data and logic elements in the `IR` so lets start by differentiating those:

 
## Visualizing Data

In case of data the driver will be the data type. The type of the data will define the general shape of the 
visualization. Let's break down the various types of data we might have in the `IR`:

### Literals

Few examples of literals: 

```elm
1 -- number

True -- Bool

"foo" -- String
```

Literals allow you to insert a few well-known data types (like `Bool`, `Int`, `Float`, `String` or `Char`) directly into 
the `IR`. As you can see these all have trivial mappings to `HTML` so they don't need further explanation:

- 1
- true
- "foo"
   
See [Literal.elm](https://github.com/finos/morphir-elm/blob/master/src/Morphir/IR/Literal.elm) for a full list of
supported literals.

### Data Constructors

Data constructors are defined as part of a custom type definition:

```elm
type Single 
    = Single Int

type Sum 
    = One Int
    | Two Bool
```

Here `Single`, `One` and `Two` are data constructors. They allow you to construct new data types by combining existing 
ones. Without any extra information they can be visualized almost the same as they appear in the source code which will 
result in a nice readable output with some highlighting:

- <span style="font-weight: bold; color: gray;">Single</span> 42 

### Records

Records types will map to labeled fields with values for each record field.


- Lists will either map to `HTML` lists or tables depending on the item type.
- And the list goes on ...

Looking more specifically in the `IR` 

## Visualizing Logic
- The specific data or logic element. This is represented by `Morphir.IR.Value.Value`.
  - In case of data elements we will populate the shape we came up with based on the type directly from the data 
  structure
  - In case of logic we need to 

in -> toFloat -> out

in -> filter [f: explain predicate] -> out