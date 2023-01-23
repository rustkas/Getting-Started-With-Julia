```
julia> println("Greetings! 你好! 안녕하세요?")
Greetings! 你好! 안녕하세요?

julia> 6*7
42

julia> ans
42

julia> 8*5
40

julia> ans
40

julia> ans+10
50

julia> a=3
3

julia> b
ERROR: UndefVarError: b not defined

julia> b = "Julia"
"Julia"

julia> b
"Julia"

julia> a = 1; b = 2; c = 3
3

julia> if 10 > 0
         println("10 is bigger than 0")
       end
10 is bigger than 0

julia>

```

`CTRL+C` - clear or interrupt a current command
`CTRL+L` - clear the screen

```
julia> printstyled(10;color=:blue)
10
julia> printstyled(10;color=:red)
10
julia> printstyled(10;color=:yellow)
10
julia>
```

```
julia> include("hello.jl")
Hello, Julia World!
```

`julia -e "a = 6 * 7; println(a)"`

```
julia -e "a = 6 * 7; println(a)"
42
```

`julia script.jl arg1 arg2 arg3`

```
julia script.jl arg1 arg2 arg3
arg1
arg2
arg3
```

```
julia main.jl
Hello, Julia World!
```

Launch package Manager
```
>julia ]
(@v1.8) pkg>
```

We can also specify multiple packages at once:

```(v1.1) pkg> add JSON StaticArrays```

To remove packages, use rm:

```(v1.1) pkg> rm JSON StaticArrays```

So far, we have referred only to registered packages. Pkg also supports working with unregistered packages. To add an unregistered package, specify a URL:

```(v1.1) pkg> add https://github.com/JuliaLang/Example.jl```

Use rm to remove this package by name:

```(v1.1) pkg> rm Example```

Use update to update an installed package:

```(v1.1) pkg> update Example```

To update all installed packages, use update without any arguments:

```(v1.1) pkg> update```


Make a graph of 100 random numbers between 0 and 1:
```
julia> using Winston

julia> plot(rand(100))
```

 ![Graph of 100 random numbers between 0 and 1](/plot.png)

 ```
 julia fizzbuzz.jl
1
2
Fizz
4
Buzz
Fizz
7
8
Fizz
Buzz
11
Fizz
13
14
FizzBuzz
16
17
Fizz
19
Buzz
Fizz
22
23
Fizz
Buzz
26
Fizz
28
29
FizzBuzz
31
32
Fizz
34
Buzz
Fizz
37
38
Fizz
Buzz
41
Fizz
43
44
FizzBuzz
46
47
Fizz
49
Buzz
Fizz
52
53
Fizz
Buzz
56
Fizz
58
59
FizzBuzz
61
62
Fizz
64
Buzz
Fizz
67
68
Fizz
Buzz
71
Fizz
73
74
FizzBuzz
76
77
Fizz
79
Buzz
Fizz
82
83
Fizz
Buzz
86
Fizz
88
89
FizzBuzz
91
92
Fizz
94
Buzz
Fizz
97
98
Fizz
Buzz
 ```

 ```
julia> a=5
5

julia> b=2a^2+30a+9
209
```


## How Julia works

```
julia> f(x) = 2x + 5
f (generic function with 1 method)

julia> code_llvm(f, (Int64,))
;  @ REPL[3]:1 within `f`
; Function Attrs: uwtable
define i64 @julia_f_147(i64 signext %0) #0 {
top:
; ┌ @ int.jl:88 within `*`
   %1 = shl i64 %0, 1
; └
; ┌ @ int.jl:87 within `+`
   %2 = add i64 %1, 5
; └
  ret i64 %2
}

julia> code_native(f, (Int64,))
        .text
        .file   "f"
        .globl  julia_f_170                     # -- Begin function julia_f_170
        .p2align        4, 0x90
        .type   julia_f_170,@function
julia_f_170:                            # @julia_f_170
; ┌ @ REPL[3]:1 within `f`
        .cfi_startproc
# %bb.0:                                # %top
        pushq   %rbp
        .cfi_def_cfa_offset 16
        .cfi_offset %rbp, -16
        movq    %rsp, %rbp
        .cfi_def_cfa_register %rbp
; │┌ @ int.jl:87 within `+`
        leaq    (%rcx,%rcx), %rax
        addq    $5, %rax
; │└
        popq    %rbp
        retq
.Lfunc_end0:
        .size   julia_f_170, .Lfunc_end0-julia_f_170
        .cfi_endproc
; └
                                        # -- End function
        .section        ".note.GNU-stack","",@progbits

julia>
```