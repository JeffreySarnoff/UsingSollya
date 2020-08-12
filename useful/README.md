## setup.sollya

This is my Sollya environment initialization file; setting global variables that control numerical computation and display.

### numerical computatation settings 

- `prec`
  > The precision in significand bits of the float format used in numerical computations.
  Commands try to adapt their working precision to have approximately `prec` correct bits.
  If, in assignment to `diam`, the value assigned is followed by an exclamation mark, no message indicating the new state is displayed. 

- `diam`
  > Parameter used in safe algorithms to control the maximal length of involved intervals.
  More precisely, `diam` is relative to the width of the input interval of the command.
  [`infnorm`, `checkinfnorm`, `accurateinfnorm`, `integral`, `findzeros`, `supnorm`].
  If, in assignment to `diam`, the value assigned is followed by an exclamation mark, no message indicating the new state is displayed. 
  `supnorm` falls back to bisecting the working interval until safe supremum norm bounds can be computed with the required accuracy or until the width of the subintervals becomes less than `diam` times the original interval I, in which case supnorm fails.

- `points`
  > Its value represents the number of points used in numerical algorithms.
  [`dirtyinfnorm`, `dirtyintegral`, `dirtyfindzeros`, `plot`]

 ### recursive refinement settings

 - `taylorrecursions` 
   > The number of recursive steps used when applying Taylor's rule.
  This rule is applied by the interval evaluator (used in `infnorm`, `evaluate`).
  If, in assignment to `diam`, the value assigned is followed by an exclamation mark, no message indicating the new state is displayed. 
  
- `hopitalrecursions`
  > The number of recursive steps used when applying L'Hopital's rule.
  This rule is applied by the interval evaluator (used in `infnorm`, `findzeros`, `evaluate`).
  If, in assignment to `diam`, the value assigned is followed by an exclamation mark, no message indicating the new state is displayed. 
  
 ### system behavior settings
  
 - `dieonerrormode`
   > Controls if Sollya is exited on an error or not.

 - `rationalmode`
   > Controls whether or not rational arithmetic is used.
   
       - When its value is off, which is the default, Sollya will not use rational arithmetic to simplify expressions. All computations, including the evaluation of constant expressions given on the Sollya prompt, will be performed using floating-point and interval arithmetic. Constant expressions will be approximated by floating-point numbers, which are in most cases faithful roundings of the expressions, when shown at the prompt.
       - When the value of the global variable rationalmode is on, Sollya will use rational arithmetic when simplifying expressions. Constant expressions, given at the Sollya prompt, will be simplified to rational numbers and displayed as such when they are in the set of the rational numbers. Otherwise, flaoting-point and interval arithmetic will be used to compute a floating-point approximation, which is in most cases a faithful rounding of the constant expression.

- `display`
  > sets or inspects the global variable specifying number notation
  one of decimal|binary|dyadic|powers|hexadecimal
  
      - If the global notation variable display is decimal, all numbers will be output in scientific decimal notation. If the global notation variable display is dyadic, all numbers will be output as dyadic numbers with Gappa notation. If the global notation variable display is powers, all numbers will be output as dyadic numbers with a notation compatible with Maple and PARI/GP. If the global notation variable display is binary, all numbers will be output in binary notation. If the global notation variable display is hexadecimal, all numbers will be output in C99/ IEEE754-2008 notation. All output notations can be parsed back by Sollya, inducing no error if the input and output precisions are the same (see prec).

- `midpointmode`
  > Controls the way intervals are displayed.
  
      - When its value is off, intervals are displayed as usual (in the form [a;b]). When its value is on, and if a and b have the same first significant digits, the interval in displayed in a way that lets one immediately see the common digits of the two bounds.
      - This mode is supported only with display set to decimal. In other modes of display, midpointmode value is simply ignored.

-  `fullparentheses`
   > An assignment fullparentheses = activation value, where activation value is one of on or off, activates respectively deactivates the output of expressions with full parenthesising. In full parenthesising mode, Sollya commands like print, write and the implicit command when an expression is given at the prompt will output expressions with parenthesising at all places where it is necessary for expressions containing infix operators to be parsed back with the same result. Otherwise parentheses around associative operators are omitted.

- `autosimplify`
   > An assignment autosimplify = activation value, where activation value is one of on or off, activates respectively deactivates the automatic safe simplification of expressions of functions generated by the evaluation of commands or in argument of other commands.
   
      - Sollya commands like remez, taylor or rationalapprox sometimes produce expressions that can be simplified. Constant subexpressions can be evaluated to dyadic floating-point numbers, monomials with coefficients 0 can be eliminated. Further, expressions indicated by the user perform better in many commands when simplified before being passed in argument to a command. When the automatic simplification of expressions is activated, Sollya automatically performs a safe (not value changing) simplification process on such expressions.
       - The automatic generation of subexpressions can be annoying, in particular if it takes too much time for not enough benefit. Further the user might want to inspect the structure of the expression tree returned by a command. In this case, the automatic simplification should be deactivated.

- `verbosity`
  > Controls the amount of information displayed by commands.
  
      - At level 0, commands do not display anything on standard output. Note that very critical information may however be displayed on standard error.
      - Default level is 1. It displays important information such as warnings when roundings happen. For higher levels more information is displayed depending on the command.

- `roundingwarnings`
  > Controls whether or not a warning is displayed when roundings occur.

- `timing`
  > Controls whether or not timing is measured.
  
      - When its value is on, the time spent in each command is measured and displayed (for verbosity levels higher than 1).
