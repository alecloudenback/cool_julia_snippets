# cool_julia_snippets

PRs welcome.

## Nested Struct Compostion...
via M Protter on Slack 2020-06.

Shared common fields and emulating common object oriented shared field pattern.

"Another approach [you] may like would be to have a common internal data structure that the subtypes of Pet all are assumed to carry. E.g. if all pets have a name, weight, age and list of medications, you might write
```julia
abstract type Pet end
struct CommonPetData
    name::String
    weight_kg::Float64
    age_years::Float64
    medications::Vector{String}
end
data(p::Pet) = p.data
name(p::Pet) = data(p).name
weight_kg(p::Pet) = data(p).weight_kg
age_years(p::Pet) = data(p).age_years
medications(p::Pet) = data(p).medications
```
and then when you make a specific pet instance, say a cat, it would store a `CommonPetData` as well as say, the length of it's tail, so you could write
```
struct Cat <: Pet
    data::CommonPetData
    tail_length_cm::Float64
end
tail_length_cm(c::Cat) = c.tail_length_cm
```

Now we managed to avoid repeating all the boilerplate relating to the name, weight, age and medications.
If you made a `Dog` and for whatever didn't want to call it's `CommonPetData` field data, and instead called it `petadata`, then you'd just write a method `data(d::Dog) = d.petdata`
You may also find it desireable to define custom constructors and show methods for your subtypes of `Pet` so that the user just writes and sees `cat(name, weight, ... tail_length_cm) `
"
