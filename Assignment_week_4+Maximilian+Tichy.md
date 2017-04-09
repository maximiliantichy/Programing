
# Assignment for week 4

Use the following table to provide us with

|name | exam number|
|----|----|
|Maxilian Tichy| 200740|
|other group member's name| exam number|

In this assignment, we will play around with functions and use the `fsolve` routine to solve an equation.

First, we need to import some libraries.

Recall that you need to have installed plotly for this to work. Further, you need to register at the plotly website.


```python

```


```python

```


```python
from scipy import optimize

from plotly.offline import download_plotlyjs, init_notebook_mode, plot, iplot
from plotly.graph_objs import Bar, Scatter, Figure, Layout
init_notebook_mode(connected=True)
from numpy import arange


```


<script>requirejs.config({paths: { 'plotly': ['https://cdn.plot.ly/plotly-latest.min']},});if(!window.Plotly) {{require(['plotly'],function(plotly) {window.Plotly=plotly;});}}</script>


Let us define the function $f(x) = x^2+c$ which is a function of $x$ for a given value of $c$.


```python
def my_function(x,c):
    return x**2 + c
```


```python

```

Now we would like to solve $x^2 + c =0$. As this is a simple equation, you can this analytically. This helps us to understand how `fsolve` works.

If you want to know more about `fsolve`, simply google "python fsolve".

For our purposes here, we call `fsolve` as `optimize.fsolve`, then we give a function and an initial value where `fsolve` starts looking for a solution. `fsolve` uses numerical techniques to find the "zero" of a function; it does not solve the equation analytically. Roughly speaking, it looks at a value of $x$ whether it is above or below 0. If it is below 0, it needs to change $x$ in such a way that $f(x)$ increases. It uses the derivative $f'(x)$ to figure out whether it should increase or decrease $x$ to get to $f(x)=0$. So suppose that $f(x) < 0$ and $f'(x) >0$ then it will increase $x$ (move to the right) to a solution to $f(x) =0$.

As `my_function` is actually a function of two variables ($x$ and $c$), we define a new "anonymous" function `lambda` that is only a function of $x$ and we solve for this function to 0. Say, we start looking for a solution at $x=1$, then we type:


```python
optimize.fsolve(lambda x: my_function(x,-2),+1)
```




    array([ 1.41421356])



This only gives one solution? But with a quadratic equation, there are usually two solutions. In the following cell give the python command to give the other solution:


```python
optimize.fsolve(lambda x: my_function(x,-2),+1)

```




    array([ 1.41421356])




```python
optimize.fsolve(lambda x: my_function(x,-2), -5)
```




    array([-1.41421356])



Now try the following cell. Explain below why you get an error message; $x=0$ does not solve this equation?


```python
optimize.fsolve(lambda x: my_function(x,-2),0)
```

    //anaconda/envs/py35/lib/python3.5/site-packages/scipy/optimize/minpack.py:161: RuntimeWarning: The iteration is not making good progress, as measured by the 
      improvement from the last ten iterations.
      warnings.warn(msg, RuntimeWarning)
    




    array([ 0.])



The code couldn't find an x for wich my_function= 0. This is because fsolve does not *solve* the equation but just tries different x until it hits the value zero. If a given number gives f(x)>0 it will try the next number "to the left" eg nearer to Zero. However if the code stats searching for solutions at 0 it will be unable to find a solution for my_function, as to do so it would need to check values "away" from 0 instead of "nearer" to zero. 

**simply said the last number (here zero) describes the number interval in wich the function will search for x such that f(x)=0. However all slutions fall outside of the interval (wich is 0 only) and thus no solution can be found**

Now we let's consider another function, with $c = 2$ (instead of $c = -2$). Explain below why we get an error this time


```python
optimize.fsolve(lambda x: my_function(x,2),-1)
```

    C:\Users\Maximilian\Anaconda3\lib\site-packages\scipy\optimize\minpack.py:161: RuntimeWarning:
    
    The iteration is not making good progress, as measured by the 
      improvement from the last ten iterations.
    
    




    array([-0.00097656])



The function has no point at wich f(x)=0, thus the error of no value being found is displayed here. With c>0, there can be no x that satisfies f(x)=0.

Now define the function $f(x) = \frac{1}{x}$ in python:


```python
def function_plotted(x):
    return x**(-1)
```

and use plotly to plot this function for $x > 0$. Adjust the range for $x$ so that you get a "decent" graph.


```python
range_x = 1
iplot(function_plotted(range_x))

```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-46-7a905a112051> in <module>()
          1 range_x = 1
    ----> 2 iplot(function_plotted(range_x))
    

    C:\Users\Maximilian\Anaconda3\lib\site-packages\plotly\offline\offline.py in iplot(figure_or_data, show_link, link_text, validate, image, filename, image_width, image_height)
        333 
        334     plot_html, plotdivid, width, height = _plot_html(
    --> 335         figure_or_data, config, validate, '100%', 525, True
        336     )
        337 
    

    C:\Users\Maximilian\Anaconda3\lib\site-packages\plotly\offline\offline.py in _plot_html(figure_or_data, config, validate, default_width, default_height, global_requirejs)
        149     # force no validation if frames is in the call
        150     # TODO - add validation for frames in call - #605
    --> 151     if 'frames' in figure_or_data:
        152         figure = tools.return_figure_from_figure_or_data(
        153             figure_or_data, False
    

    TypeError: argument of type 'float' is not iterable



```python
range_x=1
iplot function_x(range_x)
```


      File "<ipython-input-47-9ff21c27b7bd>", line 2
        iplot function_x(range_x)
                       ^
    SyntaxError: invalid syntax
    



```python
range_x=1
iplot.function_plotted(range_x)
```


    ---------------------------------------------------------------------------

    AttributeError                            Traceback (most recent call last)

    <ipython-input-48-72ce8e11cf55> in <module>()
          1 range_x=1
    ----> 2 iplot.function_plotted(range_x)
    

    AttributeError: 'function' object has no attribute 'function_plotted'


*okay at this point I have run out of ideas  how to make markdown plott this and I couldn't find instructions*


```python
range_x= x>0
iplot(function_plotted)
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-50-2c9294933652> in <module>()
          1 range_x= x>0
    ----> 2 iplot(function_plotted)
    

    C:\Users\Maximilian\Anaconda3\lib\site-packages\plotly\offline\offline.py in iplot(figure_or_data, show_link, link_text, validate, image, filename, image_width, image_height)
        333 
        334     plot_html, plotdivid, width, height = _plot_html(
    --> 335         figure_or_data, config, validate, '100%', 525, True
        336     )
        337 
    

    C:\Users\Maximilian\Anaconda3\lib\site-packages\plotly\offline\offline.py in _plot_html(figure_or_data, config, validate, default_width, default_height, global_requirejs)
        149     # force no validation if frames is in the call
        150     # TODO - add validation for frames in call - #605
    --> 151     if 'frames' in figure_or_data:
        152         figure = tools.return_figure_from_figure_or_data(
        153             figure_or_data, False
    

    TypeError: argument of type 'function' is not iterable



```python

```


```python

```


```python

```
