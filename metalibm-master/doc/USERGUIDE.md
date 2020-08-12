# Metalibm User Guide

## USAGE

Example of meta-functions can be found in the metalibm_functions directory.
The list of supported functions can be found in the Section "List of metafunctions". 

### Generating a function

Example to generate a faithful (default) approximation of the exponential function for single precision and a x86 AVX2 target:
```python2 metalibm_functions/ml_exp.py --precision binary32 --target x86_avx2 --output x86_avx2_exp2d.c ```

### Generating a function and its functionnal test bench

The following command line will generate code for single precision exponential
 and a functionnal test bench with 1000 random inputs.

```python2 metalibm_functions/ml_exp.py --precision binary32 --auto-test 1000 --target x86 --output x86_exp2f.c ```

### Generating a function and its performance test bench

The following command line will generate code for single precision exponential
 and a performance test bench with 1000 random inputs (wrapped in an outer loop
 for better measurement stability).

```python2 metalibm_functions/ml_exp.py --precision binary32 --bench 1000 --target x86 --output x86_exp2f.c ```

Note: --bench and --auto-test options can be combined.

### Building a function after generation

To check that the generated code compiles correctly, use the **--build** option to trigger compiling after generating

```python2 metalibm_functions/ml_exp.py --precision binary32 --build --target x86 --output x86_exp2f.c ```

### executing a test bench

By adding **--execute** on the command line, metalibm will try to build and execute the generated file.
Beware, pure function code can not be executed (it is not a program simply a function), functionnal or performance testbench can be executed.

```python3 metalibm_functions/ml_exp.py --precision binary32 --auto-test -- execute --target x86 --output x86_exp2f.c ```


### Verbosity

metalibm verbosity can be configured through the command-line option `--verbose`.
This command accepts default options such as **Info**, **Verbose** to enable some defaults verbosity level.
    Verbosity level can be specialized to only allow specific information display, for example **Info:passes** can be used to only display information messages generated by optimization passes.

### Activating optimization passes

Metalibm delivers a small subset of optimization passes (a.k.a pass). A pass is a transformation which manipulates the set of operation nodes to many different purposes: e.g. resolve unknown node formats, improve the graph fitness to a specific backend, optimize the graph or statically profile it.

To list the passes available in your metalibm install execute:
```
python3 metalibm_functions/status.py --pass-info
```
The command line option `--pass-info` is also available with most meta-functions or meta-entities.

To activate an optimization pass you have to chose between two options:
- `--passes <list of slot:pass_tag>` remove every default pass prio to adding command line passes
- `--extra-passes <list of slot:pass_tag>` add command lines passes to the default line of passes

The default list of passes is meta-function specific (most have none).

the list of slot:pass_tag is a comma ',' separated list of `slot:pass` arguments. `slot` indicates at which stage of pass scheduling the associated pass must be registered and `pass` is the pass class name which select which pass must be appended at the chosen slot. `slot` can be chosen among:
- `start` at the beginning of implementation generation (right after initial operation graph generation)
- `typing` after start and after canonical vectorization
- `optimization` after typing
- `beforecodegen` just before the backend code generation takes place
`pass` can be chosen among the tags listed by `--pass-info`.

The passes inserted through command-line arguments are inserted at the indicated slot, after default passes (if using `--extra-passes`) always in left-to-right-order.
For example `--extra-passes typing:basic_legalization,beforecodegen:dump,beforecodegen:quit` will insert a step of basic operation legalization during typing stage after default passes, will dump the state of the operation graph before code generation and will exit (quit) generation after that (before generating any code).


## List of metafunctions (version 1.0):

### Officially supported functions

- Exponential  (exp, exp2)
- Logarithm    (log, log2, log10, log1p)
- Square root
- Division
- Error function (erf)
- Hyperbolic Cosine

### Unstable functions

- Hyperbolic Sine
- Cubic root

## Experimental functions

- Reciprocal square root
- Cosine and Sine