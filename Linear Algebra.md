<h1>Linear algebra</h1>
<p>An essential piece of background knowledge for metabolic modelling that is often eluded to is a component of mathematics called linear algebra. Some of the termonology used in metabolic modelling like <i>matrices</i>, <i>vectors</i>, <i>linear combinations</i> and <i>null space</i> are derived from linear algebra. By understanding linear algebra, you will hopefuly begin to understand many of the concepts and literature surrounding metabolic modelling.  For those from an engineering, mathematics or computer science background, linear algebra will likely be familiar to you and you will have your own perspective on it as well. Some may see arrows moving through a plane, a list of co-ordinates, or vectors which can be multiplied and added. Those from a biology background, like me, will be strangers to many of these ideas, which is why I have created a Notebook dedicated to the topic.
    
The material in this notebook references a video series on YouTube by 3Blue1Brown who provides excellent explanations on linear algebra. Here's a link to that series: https://www.youtube.com/watch?v=fNk_zzaMoSs&list=PLZHQObOWTQDPD3MizzM2xVFitgF8hE_ab&index=1.</p>

<h3>Vectors</h3>
<p>The keystone of linear algebra is vectors, objects with both direction and magnitude. Vectors relate to enzymatic reactions because a reaction has direction (forward or backward) and magnitude (reaction rate), hence kinetic models involve the vector of enzyme kinetic function. Vectors are often easier to visualise by using arrows on a grid, whereby the angle is direction and length is magnitude.</p>


```python
#Admittedly, matplotlib isn't the prettiest for illustrating vectors, but it makes the point. 
import matplotlib.pyplot as plt
ax = plt.axes()
axes = [0, 1, 2, 3, 4]
ax.arrow(0, 0, 2, 3, head_width = 0.3, head_length = 0.1, lw=3, overhang=0.1, color = 'b', length_includes_head=True)
plt.annotate(r'$\vec{V}$', xy = (1.5,3))
plt.xticks(axes)
plt.yticks(axes)
plt.grid()
plt.title("Figure 1")
plt.show();
```


![png](output_2_0.png)


<p>While vectors are defined by direction and magnitude, they are actually written as coordinates. In figure 1, the vector ($\vec{v}$) has the coordinates (2, 3) representing <em>x</em> and <em>y</em>, respectively. However, vectors are not written this way, we write vectors as a list in a matrix: $\left[ \begin{matrix} 2 \\ 3 \end{matrix} \right]$. 

For multiple vectors, we can visualise it as either all the vectors starting at the origin or joined together. The latter can often be easier as it allows us to show an arrow that is the sum of both vectors</p>


```python
import matplotlib.pyplot as plt

yaxes = [-3, -2, -1, 0, 1, 2, 3, 4]
xaxes = [0, 1, 2, 3, 4]
fig, (ax1, ax2) = plt.subplots(1, 2, constrained_layout=True, figsize = (8, 4))

def Draw_arrow(axes, a1, a2, b1, b2, colour):
    axes.arrow(a1, a2, b1, b2, head_width = 0.3, head_length = 0.1, lw=3, overhang=0.1, color = colour, length_includes_head=True)

def set_ticks(axes):
    axes.set_xticks(xaxes)
    axes.set_yticks(yaxes)

spine = ['left', 'right', 'bottom', 'top', 'zero', 'none']
def spines(axes):
    for i in range(0, 3, 2):
        axes.spines[spine[0+i]].set_position(spine[4])
        axes.spines[spine[1+i]].set_color(spine[5])
    
#ax1
Draw_arrow(ax1, 0, 0, 2, 3, 'b')
Draw_arrow(ax1, 0, 0, 1, -2, 'r')

#formatting
set_ticks(ax1)
ax1.annotate(r'$\vec{V}$', xy = (1.5,3))
ax1.annotate(r"$\vec{W}$", xy = (1.5, -1.5))
spines(ax1)
ax1.set_title("Figure 2")


#ax2
Draw_arrow(ax2, 0, 0, 2, 3, 'b')
Draw_arrow(ax2, 2, 3, 1,-2, 'r')
Draw_arrow(ax2, 0, 0, 3, 1, 'g')


#formatting
set_ticks(ax2)
ax2.annotate(r"$\vec{V}$", xy=(1,3))
ax2.annotate(r"$\vec{W}$", xy=(3, 2))
ax2.annotate(r"$\vec{V} + \vec{W}$", xy=(2.2, 0.2))
spines(ax2)
ax2.set_title("Figure 3")

ax1.grid()
ax2.grid()
plt.show()
```


![png](output_4_0.png)


$$\vec{v} = \left[ \begin{matrix} 2 \\ 3 \end{matrix} \right] \text{, } \vec{w} = \left[ \begin{matrix} 1 \\ -2 \end{matrix} \right] \text{ and } \vec{v} + \vec{w} =\left[ \begin{matrix} 3 \\ 1 \end{matrix} \right]$$

<p>
Figure 2 illustrates vectors $\vec{v}$  and $\vec{w}$ starting from the origin and Figure 3 with both vectors joined to form the resulting vector $\vec{v} + \vec{w}$.

<h3>Scalers</h3>
<p>Vectors can be scaled (multiplied) by using "scalers": $2 \cdot \left[ \begin{matrix} 2 \\ 1 \end{matrix} \right]$ gives us $\left[ \begin{matrix} 4 \\ 2 \end{matrix} \right] $. A negative scalar flips the vector, whereas fraction scalers shrink the vector. Let's imagine our vector coordinates are scalers of $\hat{i}$ and $\hat{j}$ which represent a scale on our graph, lets say it represents one on the y axis and one on the x axis. $\left[ \begin{matrix} 3 \\ 3 \end{matrix} \right] = (3)\hat{i} + (3)\hat{j}$. $\hat{i}$ and $\hat{j}$ are called "basis vectors" of the xy coordinate system. So when vector coordinates are seen as scalers, it's the basis vectors they are scaling. So whenever we are scaling vectors and adding them, this is called a <i>linear combination</i> (a term you will find frequently in metabolic modelling literature). If we randomly picked different basis vectors, we can get an infinite amount of new co-ordinate systems. This set of linear combinations of all possible vectors that can be reached (through scaling) is called the "span".</p>

<h3>Linear transformation</h3>
<p>Linear transformations transform an input vector and outputs an output vector. They are not so important for metabolic modelling but are key concepts in linear algebra (see playlist linked at the start).</p>
    
<h3>Matrices</h3>
<p>One mathematical representation you will see often is matrices, they illustrate vectors or lists of numbers in a "boxed" form. If we take a list of equations, the usefulness of matrices can be understood:
$$2x + 5y + 3z = -3 \\
4x + 0y + 8z = 0 \\
1x + 3y + 0z = 2$$
A list of equations like this is called a "linear system of equations" and xyz can be solved using Gaussian elimination.
We can break down these equations into seperate matrices so that constants (A), variables ($\vec{x}$) and lingering constants ($\vec{v}$) (the numbers on the right of the equation) can be placed in their own matrices:

$$ \left[ \begin{matrix} 2 & 5 & 3 \\ 4 & 0 & 8 \\ 1 & 3 & 0 \end{matrix} \right] 
\left[ \begin{matrix} x \\ y \\ z \end{matrix} \right] = 
\left[ \begin{matrix} -3 \\ 0 \\ 2 \end{matrix} \right] \\ 
A\vec{x} = \vec{v}$$

The set of all possible outputs of $A\vec{v}$ is called the "column space". $\left[ \begin{matrix} 0 \\ 0 \end{matrix} \right]$ is always in the column space because linear transformations must always keep the origin fixed in place. In contrast, the "null space" is the set of vectors that land on zero $A\vec{x} = \left[ \begin{matrix} 0 \\ 0 \end{matrix} \right]$. The null space provides all possible solutions to the linear system of equations.</p>

<h3>Gaussian Elimination</h3>
<p>Gaussian Elimination is the process of solving a linear system of equations to determine the unknown variables. Read the rules in the following Python script and run the code, it will talk you through how to solve a randomly generated linear system of equations</p>


```python
#Performs Gaussian elimination of a linear system of equations
#Written by Cailean Carter

#Rules:
# - Can multiply any row by a constanant (other than zero)
# - Can switch any two rows
# - Can add any two rows together

from random import randint

Linear_system_of_equations = {} #keys are equation index and values are a list containing constanants and last value being the lingering constant

number_of_equations = 3

#Create randomised equations:

xyz = [randint(-10, 10) for _ in range(number_of_equations)] #creates xyz "unknown variables"

for index in range(1, number_of_equations + 1):

    Linear_system_of_equations[index] = [randint(-10, 10) for _ in range(number_of_equations)] #created randomised constants
    Linear_system_of_equations[index].append(0) 

    for num in range(number_of_equations):
        Linear_system_of_equations[index][3] += (Linear_system_of_equations[index][num] * xyz[num])  #calculates the lingering constant

########

def Print_equations():
    for equation in Linear_system_of_equations.keys():
        Row = "Row {row} : {a}x + {b}y + {c}z = {lingering_constant}"
        print(
            Row.format(
            row = equation,
            a= round(Linear_system_of_equations[equation][0]),
            b= round(Linear_system_of_equations[equation][1]), 
            c= round(Linear_system_of_equations[equation][2]),
            lingering_constant= round(Linear_system_of_equations[equation][3])
            ))
    print("")
            
def Print_matrix():
    for equation in Linear_system_of_equations.keys():
        matrix = "{a} {b} {c} : {lingering_constant}"
        print(
            matrix.format(
            a = round(Linear_system_of_equations[equation][0], 2),
            b = round(Linear_system_of_equations[equation][1], 2),
            c = round(Linear_system_of_equations[equation][2], 2),
            lingering_constant = round(Linear_system_of_equations[equation][3], 2)
            ))
    print("")

def Output():
    SolvedEquations = "The equations have been solved for: x = {x}, y = {y} and z = {z}."
    print(SolvedEquations.format(
        x = round(Linear_system_of_equations[1][3]),
        y = round(Linear_system_of_equations[2][3]),
        z = round(Linear_system_of_equations[3][3])
    ))
    Print_equations()

def Gaussian_elimination(column, row, value=0):
    
    eq_row = Linear_system_of_equations[row] #eq_row means equation row

    if eq_row[column-1] == value: #if the value is already what is wanted, the script moves on to next number.
        print("No action required - number already " + str(value))
        return

    elif value == 1 and eq_row[column-1] != 0:
        #checks all numbers in the equation that aren't zero can be times by a constant to give value 1. 
        if all(number % eq_row[column-1] == 0 for number in eq_row if number != 0) or column == row: 
            Linear_system_of_equations[row] = [] #clears row
            for number in eq_row:
                Linear_system_of_equations[row].append(number / eq_row[column-1] if number!= 0 else 0)
            
            statement = "Row {row} was multiplied by 1 over " + str(round(eq_row[column-1], 2)) + " from column {column}, row {row}"
            print(statement.format_map(vars()))
            return
        
    for equation in Linear_system_of_equations.keys(): 
        #checks if can swap rows/equations
        if equation != row:
    
            #checks if can multiply another row and add
            if all(number == 0  for number in Linear_system_of_equations[equation][:column-1]) or Linear_system_of_equations[equation][column-1] == 1:
                Linear_system_of_equations[row] = [eq_row[number] - (Linear_system_of_equations[equation][number] * ((eq_row[column-1] - value) / Linear_system_of_equations[equation][column-1])) for number in range(len(eq_row))]
                
                statement = "Row {equation} was multiplied by " + str(-round((eq_row[column-1] - value) / Linear_system_of_equations[equation][column-1], 2)) + " and added to row {row}"
                print(statement.format_map(vars()))
                return
     
            elif Linear_system_of_equations[equation][equation-1] != 1 and Linear_system_of_equations[equation][column-1] == value: #the first part is checking that it doesn't have a 1 as to not disturb the diaganol 1 trend
                Linear_system_of_equations[row] = Linear_system_of_equations[equation] #current row is swapped with a suitable row
                Linear_system_of_equations[equation] = eq_row #old row is swapped with current row
                    
                statement = "Swapped rows {row} and {equation}"
                print(statement.format_map(vars()))
                return

def Start():

    print("Starting Gaussian elimination...\n")
    Print_equations()
    
    post_row_echelon_form_queue = [] 

    for column in range(1, number_of_equations + 1):
        for row in range(1, number_of_equations + 1):

            if row == column:
                Gaussian_elimination(column, row, 1)
                Print_matrix()
            elif row > column:
                Gaussian_elimination(column, row)
                Print_matrix()
            elif row < column: 
                post_row_echelon_form_queue.append([column, row])
    
    for remainder in post_row_echelon_form_queue:
        column, row = remainder
        Gaussian_elimination(column, row)
        Print_matrix()
    
    Output()
           
Start()
```

    Starting Gaussian elimination...
    
    Row 1 : 5x + -6y + -1z = 2
    Row 2 : -9x + -3y + -5z = -113
    Row 3 : -6x + 9y + 6z = 51
    
    Row 1 was multiplied by 1 over 5 from column 1, row 1
    1.0 -1.2 -0.2 : 0.4
    -9 -3 -5 : -113
    -6 9 6 : 51
    
    Row 1 was multiplied by 9.0 and added to row 2
    1.0 -1.2 -0.2 : 0.4
    0.0 -13.8 -6.8 : -109.4
    -6 9 6 : 51
    
    Row 1 was multiplied by 6.0 and added to row 3
    1.0 -1.2 -0.2 : 0.4
    0.0 -13.8 -6.8 : -109.4
    0.0 1.8 4.8 : 53.4
    
    Row 2 was multiplied by 1 over -13.8 from column 2, row 2
    1.0 -1.2 -0.2 : 0.4
    0 1.0 0.49 : 7.93
    0.0 1.8 4.8 : 53.4
    
    Row 2 was multiplied by -1.8 and added to row 3
    1.0 -1.2 -0.2 : 0.4
    0 1.0 0.49 : 7.93
    0.0 0.0 3.91 : 39.13
    
    Row 3 was multiplied by 1 over 3.91 from column 3, row 3
    1.0 -1.2 -0.2 : 0.4
    0 1.0 0.49 : 7.93
    0 0 1.0 : 10.0
    
    Row 2 was multiplied by 1.2 and added to row 1
    1.0 0.0 0.39 : 9.91
    0 1.0 0.49 : 7.93
    0 0 1.0 : 10.0
    
    Row 3 was multiplied by -0.39 and added to row 1
    1.0 0.0 0.0 : 6.0
    0 1.0 0.49 : 7.93
    0 0 1.0 : 10.0
    
    Row 3 was multiplied by -0.49 and added to row 2
    1.0 0.0 0.0 : 6.0
    0.0 1.0 0.0 : 3.0
    0 0 1.0 : 10.0
    
    The equations have been solved for: x = 6, y = 3 and z = 10.
    Row 1 : 1x + 0y + 0z = 6
    Row 2 : 0x + 1y + 0z = 3
    Row 3 : 0x + 0y + 1z = 10
    
    


```python

```
