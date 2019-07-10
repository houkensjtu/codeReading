Profiling
=========

The following block of code is profiled by :py:mod:`cProfile`:

.. literalinclude:: ../tool/profQCLayers.py
   :language: python



where *16um.json* is the following file:

.. literalinclude:: ../example/16um.json
   :language: json


Before optimizing code performamce, there are 814603 function calls taking 10.835
seconds in total. The output of :py:mod:`cProfile` sorted by cumulative time is
listed in the following table.


=========  =======  =======  =======  ======= ===============================================================
   ncalls  tottime  percall  cumtime  percall filename:lineno(function)
=========  =======  =======  =======  ======= ===============================================================
        1    0.000    0.000   10.803   10.803 QCLayers.py:425(calc_FoM)
       35    9.742    0.278   10.803    0.309 QCLayers.py:383(loTransition)
        2    0.000    0.000   10.449    5.224 QCLayers.py:419(loLifeTime)
        2    0.000    0.000   10.449    5.224 QCLayers.py:422(<listcomp>)
   135301    0.132    0.000    0.797    0.000 fromnumeric.py:1821(sum)
   135303    0.155    0.000    0.640    0.000 fromnumeric.py:64(_wrapreduction)
   135331    0.467    0.000    0.467    0.000 {method 'reduce' of 'numpy.ufunc' objects}
   135180    0.262    0.000    0.262    0.000 {built-in method builtins.abs}
        1    0.000    0.000    0.037    0.037 QCLayers.py:260(solve_whole)
        1    0.036    0.036    0.036    0.036 OneDSchrodinger.py:61(cSimpleSolve1D)
   135313    0.025    0.000    0.025    0.000 {built-in method builtins.isinstance}
   135303    0.019    0.000    0.019    0.000 {method 'items' of 'dict' objects}
        1    0.001    0.001    0.002    0.002 QCLayers.py:178(populate_x)
       65    0.000    0.000    0.001    0.000 QCLayers.py:169(avghwLO)
        1    0.001    0.001    0.001    0.001 OneDSchrodinger.py:74(cSimpleFillPsi)
      227    0.000    0.000    0.001    0.000 {built-in method builtins.sum}
       28    0.001    0.000    0.001    0.000 QCLayers.py:227(<listcomp>)
     1885    0.001    0.000    0.001    0.000 QCLayers.py:173(<genexpr>)
=========  =======  =======  =======  ======= ===============================================================

.. currentmodule:: QCLayers



After optimizing code performance by replace most time consuming function call 
(:py:meth:`QCLayers.loLifeTime`), by C code and add openMP support, 
there are 3613 function calls taking 1.255 seconds in total. 
The output of :py:mod:`cProfile` sorted by cumulative time is listed in the
following table.

=========  =======  =======  =======  ======= ===============================================================
   ncalls  tottime  percall  cumtime  percall filename:lineno(function)
=========  =======  =======  =======  ======= ===============================================================
        1    0.000    0.000    1.205    1.205 QCLayers.py:427(calc_FoM)
       35    0.003    0.000    1.205    0.034 QCLayers.py:383(loTransition)
       30    1.199    0.040    1.199    0.040 OneDSchrodinger.py:113(cLOphononScatter)
        2    0.000    0.000    1.166    0.583 QCLayers.py:421(loLifeTime)
        2    0.000    0.000    1.165    0.583 QCLayers.py:424(<listcomp>)
        1    0.000    0.000    0.048    0.048 QCLayers.py:260(solve_whole)
        1    0.046    0.046    0.046    0.046 OneDSchrodinger.py:65(cSimpleSolve1D)
        1    0.001    0.001    0.002    0.002 QCLayers.py:178(populate_x)
       91    0.000    0.000    0.001    0.000 fromnumeric.py:1821(sum)
       65    0.000    0.000    0.001    0.000 QCLayers.py:169(avghwLO)
      227    0.000    0.000    0.001    0.000 {built-in method builtins.sum}
        1    0.001    0.001    0.001    0.001 OneDSchrodinger.py:78(cSimpleFillPsi)
       93    0.000    0.000    0.001    0.000 fromnumeric.py:64(_wrapreduction)
      121    0.001    0.000    0.001    0.000 {method 'reduce' of 'numpy.ufunc' objects}
     1885    0.001    0.000    0.001    0.000 QCLayers.py:173(<genexpr>)
       68    0.000    0.000    0.001    0.000 ctypeslib.py:196(from_param)
       28    0.000    0.000    0.000    0.000 QCLayers.py:227(<listcomp>)
       65    0.000    0.000    0.000    0.000 {built-in method numpy.core.multiarray.array}
=========  =======  =======  =======  ======= ===============================================================
