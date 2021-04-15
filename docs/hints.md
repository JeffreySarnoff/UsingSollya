To incorporate other sollya source files use `execute("filepathname.sollya")`
To run an external command use `bashexecute("<command>")
   if command produces an output in a file, this result can be imported in Sollya
   with help of commands like execute, readfile and parse.
   
   
prec sets bits of precision
diam sets width of interval used with refinement
   diam is relative to the width of the input interval of the command. 
   For instance, suppose that diam=1e-5: if infnorm is called on interval [0;1], 
   the maximal width of an interval will be 1e-5. 
   But if it is called on interval [0;1e-3], the maximal width will be 1e-8.
   
