### Sealed Trait 
> A `sealed` trait can be extended only in the same file as its declaration. It works as a alternative to `enum`.It is used whwn the sub types are finite and we know all the sub-types in advance. This will also help to catch the bugs eaarly in the program.

> By sealing the class, Scala will not let any other be created outside the source file. Consequently, Scala can use this fact to check that our match statements are exhaustive.

