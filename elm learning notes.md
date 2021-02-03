# Elm learning notes

Written by Mena Zhang.

---

2021/1/2

#### Elm Architecture -> Text Fields

- `div` <- two children
- `<input>` <- three attributes
  - `placeholder` is the text that shows when there is no content
  - `value` is the current content of this `<input>`
  - `onInput` sends messages when the user types in this `<input>` node

#### Elm Architecture -> Forms

- Using helper function to make `view` cleaner

```elm
  view : Model -> Html Msg
  view model =
    div []
      [ viewInput "text" "Name" model.name Name
      , viewInput "password" "Password" model.password Password
      , viewInput "password" "Re-enter Password" model.passwordAgain PasswordAgain
      , viewValidation model
      ]

  viewInput : String -> String -> String -> (String -> msg) -> Html msg
  viewInput t p v toMsg =
    input [ type_ t, placeholder p, value v, onInput toMsg ] [] 
```



---

2021/1/6

#### Types -> Reading Types

- **Type Variable** `a` is saying that we can match any type

```elm
> List.reverse
<function> : List a -> List a

> List.length
<function> : List a -> Int
```

- **Constrained Type Variable**  make operator more flexible
  - `number` permits `Int` and `Float`
  - `appendable` permits `String` and `List a`
  - `comparable` permits `Int`, `Float`, `Char`, `String`, and lists/tuples of `comparable` values
  - `compappend` permits `String` and `List comparable`

<font color=Red>Notes: Normally type variables can get filled in with anything, but `number` can only be filled in by `Int` and `Float` values. It **constrains** the possibilities.</font>

---

2021/1/19

#### Types -> Pattern Matching

- **case** 

  ```elm
  toName user =
    case user of
      Regular name age ->
        name
  
      Visitor name ->
        name
  -- toName (Regular "Thomas" 44) == "Thomas"
  -- toName (Visitor "kate95")    == "kate95"
  ```

- **Wild Cards**  _ represents the unused data