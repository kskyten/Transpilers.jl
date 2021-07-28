# Transpilers

Transpilers is a common interface for transpiling code into Julia. It is mainly
intended for translating numerical code and wrapping packages and adding
multiple dispatch to packages called via PyCall and RCall. However, it aims to
be flexible and extensible enough to be used more generally.

## Usage

Transpilers exports a single `transpile` method, which takes the desired format
as the first argument and the code to be transpiled as the second argument.
Additional options can be given as keyword arguments.

``` julia
using Transpilers

transpile(Expr, py"1 + 1")

transpile(String, py"lambda x, y: x * y")

open("output.jl", "w") do f
    transpile(f,
    py"""
    import numpy as np

    def foo(x, y):
        x + y * np.dot(x, y)
    """)
end
```

# Backends
https://github.com/kskyten/FromPython.jl
https://github.com/kskyten/FromR.jl
