[Visualization](index.html)

Visualization in technical terms is the mapping of the `Morphir IR` to `HTML`. Conveniently our main modeling language 
(`Elm`) was designed for that purpose and it's extremely good at it. So let's formalize this in `Elm` code:

```elm
visualization : ir -> Html msg
```

Different elements in the `IR` will map to different structures in `HTML`. The `IR` contains both data and logic and
in both cases the `HTML` we produce will depend on two things:

- The type of the data/logic. This is represented by `Morphir.IR.Type.Type`.
- The specific data/logic element. This is represented by `Morphir.IR.Value.Value`.

