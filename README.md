<h1>ScrumPy Notebook</h1>
<p>This is a personal notebook for learning and training with ScrumPy, a metabolic modelling tool. It contains the background to metabolic modelling and necessary knowledge to begin using ScrumPy. A small cheat sheet is available at the end of the notebook and a complete version in a seperate notebook. This notebook assumes prior knowledge of the programming language Python.<br>
    
The information contained in this notebook is a collection of re-formatted material provided by the team behind ScrumPy and current literature (when cited). Content is repurposed from the ScrumPy documentation (http://mudshark.brookes.ac.uk/ScrumPy/Doc) and presentations from meetings found on the ScrumPy website. This notebook aims to provide clarity and comprehension of ScrumPy while also being a learning space for metabolic modelling.
</p><hr />

<h2>Introduction to ScrumPy</h2>
<p>ScrumPy is a software package used for the definition and analysis of metabolic models. It is written and interacted with using the Python programming language. ScrumPy has features for both kinetic and structural modelling with an emphasis  on structural modelling and features of most relevance for analysis of large (genome-scale) models.  (Mark Poolman, 2006. DOI: 10.1049/ip-syb:20060010) <br>

Metabolic models are computerised representations of living metabolic networks; illustrating the transformation of metabolites from substrate through intermediates to products. ScrumPy can handle models of various sizes: from small models representing a single pathway, to the entire metabolic network of a living organism (i.e. genome-scale metabolic model). In order to get useful information out of a model, ScrumPy allows the user to interact and change the model in various ways. The user can remove reactions, introduce new pathways, alter the direction of metabolites through a pathway, and create new environments for the model to respond to. This is but a short list of possibilities and should give you an idea of what can be achieved through ScrumPy. The tool has great academic and biotechnilogical application, as evident by the exhaustive list of publications involving metabolic models. <br>
    
The next chapter will explain the background behind metabolic modelling and introduces structural and kinetic modelling.
</p><hr />

<h2>The Nature of Metabolic Models</h2>

<p>Metabolic models are representations of metabolic pathways (namely networks); illustrating the flow of matter from the source (beginning) to the sink (end). There are two key components of a metabolic model: the <em>structure</em> and the <em>kinetics</em>. The structure is diagramtic represenation of a pathway (from A to B) whereby no change in metabolite concentrations occur and the enzyme kinetics are not considered. Whereas kinetics are the rates of reactions and is reflected in the fluctuations in concentration of metabolites. Throughout this notebook, we will be exploring the topology of metabolic networks: the set of enzymes and metabolites, their connections and the stoichiometry and directionality of reactions. We will start by exploring structural models.</p> <hr \>

<h3>Structural Models</h3>
<p>Structural models are investigated under a condition called <i>steady state</i>. Whereby concentrations of all the intermediates remain constant as their rate of formation equals the rate of degredation. To understand the structural model, let's use a hypothetical pathway:</p>

<img src="Simple metabolic network.png" width="400" height="180"> </img>

<p>In this network, <em>X</em> marks metabolites which are external and <em>S</em> denotes substrates. The reactions have been numbered so they can be referred back to. This is a rather small pathway and can be broken down into individual reactions, as so:<br>
    <blockquote>
    r denotes the numbered reaction<br>
    r1: X<sub>0</sub> -> S<sub>1</sub><br>
    r2: S<sub>1</sub> -> S<sub>2</sub><br>
    r3: S<sub>2</sub> -> S<sub>1</sub><br>
    r4: S<sub>2</sub> -> X<sub>1</sub><br>
    r5: S<sub>2</sub> <> S<sub>3</sub>
    </blockquote>
    
Reactions r1 - 4 are irreversible (denoted by ->), meaning the movement of metabolites within the reaction is in a single direction. However, reaction r2 and r3 interact with the same metabolites, but are not reversible as require seperate enzymes. Conversely, reaction 5 is reversible (denoted by <>). Further, the reactions can be illustrated as a table, where the gain of a substrate is given 1, the loss of substrate is -1, and no change is 0.
<table>
    <tr>
        <th></th> <th>r1</th> <th>r2</th> <th>r3</th> <th>r4</th> <th>r5</th>
    </tr>
    <tr>
        <td>S<sub>1</sub></td> <td>1</td> <td>-1</td> <td>1</td> <td>0</td> <td>0</td>
    </tr>
    <tr>
        <td>S<sub>2</sub></td> <td>0</td> <td>1</td> <td>-1</td> <td>-1</td> <td>-1</td>
    </tr>
    <tr>
        <td>S<sub>3</sub></td> <td>0</td> <td>0</td> <td>0</td> <td>0</td> <td>1</td>
    </tr>
</table><br>
This table is called the <b>stoichiometry matrix</b>, it illustrates how all the reactions relate to each other in a computer-readible form. The structural element of a model is integral and lays the foundation for kinetic models which are built on top. Kinetics will be explored next.</p>

<h3>Kinetic Models</h3>
<p>Admittedly, structural models lack the dynamic nature of <i>in vivo</i> metabolic pathways - structurals are essentially trinary in practice. While this allows simplification of metabolic networks, it is often desirable to explore the kinetics of reactions. This is why ScrumPy seperates kinetics and structural models - allowing the user to focus on one or the other, or even both. To begin, we will start with the basic foundations of enzyme kinetics: the Michaelis-Menten equation.</p>


<h4>Michaelis-Menten Enzyme Kinetics</h4>
<p>This is one of the best-known representation of enzyme kinetics (according to Wikipedia). It describes the rate of enzymatic reactions by correlating the reaction rate <em>v</em> to concentration of substrate <em>S</em>. <br>
    
<img src="https://render.githubusercontent.com/render/math?math=\begin{equation*}v=\frac{SV}{S + K_m}\end{equation*}">
    
<br>The <em>v</em> is a vector (an object with magnitude and direction) of enzyme kinetic functions, namely reaction rate (this is important for later). The upper case <em>V</em> is the <i>limiting rate</i> (or maximum velocity, <em>V<sub>m</sub></em>) and <em>K<sub>m</sub></em> is the <em>Michaelis constant</em> (concentration of substrate when the reaction velocity is equal to one half the maximal velocity of the reaction). The reasoning for a rate limiting velocity is that if an intermediate step is much slower than the other reactions, the overall rate of the net reaction will equal the rate of the slowest step (namely the rate limiting step). The implication being that increasing the concentration of the rate limiting enzyme should increase the net flux through the pathway.
    
In a kinetic model, each substrate is tied to at least one reaction, and those reactions will have an enzyme kinetic vector. We can map how each substrate relates to its surrounding enzymes' vectors using the network described in Structural modelling. Let's take S<sub>1</sub> (substrate 1) for example, its concentration gains from reactions 1 and 3, and decreases from reaction 2. If we take the enzyme kinetics associated with each reaction, we can represent it as:</p><br><br>
    
<img src="https://render.githubusercontent.com/render/math?math=\begin{equation*}\frac{dS_1}{dt}=v_1-v_2+v_3\end{equation*}">
    
<br> This equation is rather simplistic, showing how our substrate is influenced by the kinetic vector of its associated reactions. For substrates 2 and 3, it will look like this:<br><br>
    
<img src="https://render.githubusercontent.com/render/math?math=\begin{equation*}\frac{dS_2}{dt}=v_2-v_3-v_4-v_5\\\frac{dS_3}{dt}=v_5\end{equation*}">

 <p>Next we will be discussing how kinetic models relate to structural models.</p>

<h3>Relating Kinetic and Structural Models</h3>

<p>Having explored the basics of structural and kinetic models, we can begin to explore how they relate to one another. An <i>in vivo</i> metabolic pathway will consist of both structural and kinetic elements. However, ScrumPy seperates them and allows the user to investigate either element or both. But, how do the structural and kinetic elements relate? And in what way are they seperated?
    
We can observe the relationship between structural and kinetics in the following equation. The structural element is represented by the stoichiometry matrix for the substrates mentioned in the structural section, and the kinetics are represented by the enzyme kinetic vectors from the Michaelis-Menten equation.   
</p>
\begin{equation*}
\left[
\begin{matrix}
\frac{dS_1}{dt}\\
\frac{dS_2}{dt}\\
\frac{dS_3}{dt}\\
\end{matrix}
\right]
=
\left[
\begin{matrix} 
    1 & -1 & 1 & 0 & 0\\
    0 & 1 & -1 & -1 & -1\\
    0 & 0 & 0 & 0 & 1\\
\end{matrix} 
\right]
\cdot
\left[
\begin{matrix}
    v_1\\ v_2\\ v_3\\ v_4\\ v_5\\
\end{matrix}
\right]
\end{equation*}
    
<p>You may recall from the stoichiometry matrix that each number in a row (for each substrate) is associated with the change in metabolite concentration for each reaction (r1 to r5). As the stoichiometry matrix is a trinary of 1, 0 and -1, we can easily multiply the enzyme kinetic vectors to their respective reaction in the matrix. This will provide a matrix illustrating the enzyme kinetics for each reaction in our structural model, therefore relating kinetics and structural elements. When the condition is steady state, the final result will always equal 0 (just count all the numbers in the stoichiometry matrix, you'll see). A structural model involves exploring solutions of this equation, with <em>v<sub>i</sub></em> as the unknown variables. As this equation is linear, it allows one to distinguish between feasible and non-feasible states of the network (i.e. you will be able to tell what pathways are possible).</p><hr />

<h3>The Facets of Structural Models</h3>
<p>Metabolic models have a number of features, namely null spaces, elementary modes and conserved cycles. These features are present in structural models and are worth knowing about before moving onto analysis of a model. This is because they allow you to investigate the possible reactions a metabolite can go through under steady state and to better understand the roles of reactions in a model.</p>

<h4>Null Space</h4>

<p>Null space explores the possible routes a metabolite can take through a network under steady state (meaning the concentration of a internal metabolite cannot change). Going back to our original metabolic network, there are at least two ways in which the flow of metabolites could travel under steady state. Firstly, our substrate X<sub>0</sub> could flow to X<sub>1</sub> through reactions 1, 2 and 4. Alternatively, our substrate could cycle around reactions 2 and 3. We can illustrate this in a binary method, whereby if a metabolite travels through a reaction it will be denoted as 1, and 0 denotes no reaction. Reactions are in order from 1 to 5.
<blockquote><b>Possibility 1</b> &nbsp; X<sub>0</sub> to X<sub>1</sub> = [1 1 0 1 0]<br><br>
<b>Possibility 2</b> &nbsp; S<sub>1</sub> to S<sub>2</sub> and back again = [0 1 1 0 0]</blockquote>        
It is worth noting that null space is not the same as a stoichiometry matrix, null space focuses on the combination of possibilities a metabolite can travel in steady state and emphasises reactions. Any set of combinations at steady state will be a linear combination of vectors called <b>K</b> (<em>the kernel matrix</em>), which is a general term for null space and encapsulates all possible steady-state solutions. Thus, for our basic network the null space looks like this:<br><br>

\begin{equation*}
\mathbf{K} = 
\left[
\begin{matrix}
1 & 0 \\
1 & 1 \\
0 & 1 \\
1 & 0 \\
0 & 0 \\
\end{matrix}
\right]
\end{equation*}

<br>Null space establishes the relationships between reaction fluxes. However, there are some disadvantages to null-space analysis: (1) provides a rather unfocussed view of a system; (2) does not implicitly take into account thermodynamics; (3) hard to integrate experimental flux observations; (4) less interpretable for large (genome-scale) models.

Thus far, we have explored the structural aspect of null space. However, it can be combined with kinetics similarly to how it was done with the stoichiometry matrix. We can assign an arbitrary notation to each possibility, <em>a</em> and <em>b</em>, with our first possibility on the left and second on the right of the matrix.<br>

\begin{equation*}
\left[ 
\begin{matrix}
    1 & 0\\ 1 & 1\\ 0 & 1\\ 1 & 0\\ 0 & 0\\
\end{matrix} 
\right] 
\cdot 
\left[ 
\begin{matrix}
    a\\
    b\\
\end{matrix} 
\right] = 
\left[ 
\begin{matrix}
    a\\ a+b\\ b\\ a\\ 0\\
 \end{matrix} 
 \right] = 
 \left[ 
 \begin{matrix}
    v_1\\ v_2\\ v_3\\ v_4\\ v_5\\
\end{matrix} 
\right]
\end{equation*}

This representation allows us to see which reaction vectors are unique to each possibility, which are called subsets (<em>a set of reactions carrying flux in fixed ratios and a single net stoichiometry</em>). We can see that the first and fourth row are unique to possibility <em>a</em>. The last row is considered a dead vector; a reaction which can not carry flux at steady-state. If any single reaction is removed from a subset, the remaining reactions will be dead. If one or more reactions in a subset are irreversible, the whole subset is irreversible. 

The null space allows us to identify at least a couple things about our model. Firstly, identify whether viable routes exist from nutrients to any given metabolic product. Secondly, identify whether some routes remain after deletion of a particular enzyme.</p>

<h4> Elementary Modes</h4>
<p>Coincidentally, the set of reactions identified in our null space discussion happen to be what are called elementary modes. They are similar to null space, but represent minimal, indipendent paths in a system under steady state and have a number of definitions:
    <ul>
        <li>Must balance all internal metabolites</li>
        <li>Respect reversibility</li>
        <li>Metabolites can not decompose</li>
        <li>And are associated with a single net stoichiometry involving only external metabolites (or none)</li>
    </ul>
Elementary modes are useful to identify in any given reaction, particularly for biochemical application, as the conversion yield can be computed easily by calculating the net stoichiometries for the external substances (see Input-Output Stoichiometry). They also allow easy identification of all possible solutions in a metabolic network (Schuster et al., 1999).</p>

<h4>Conserved Cycles</h4>
<p>The significance of conserved cycles in metabolic models isn't entirely clear. These are a set of reactions whereby a metabolite is circled between two or more states (take ATP hydrolysis and synthesis for example) and their total concentration is fixed. This can be quite a common scenario in a model, particularly if a reaction requires a cofactor like ATP or NAD(P)H. This scenario is also called a <i>moiety conservation</i> and can be found in the stoichiometry matrix. <hr />

<h3>Forms of Analysis</h3>

<p>In order to get any meaningful information from a model, you need to be able to analyse it. Metabolic pathway analysis can be used to investigate the metabolic network structure, robustness, fragility, regulation, metabolic flux vector, and rational strain design (Trinh et al., 2009). This section aims to highlight some of the analysis methods available.</p>
      
<ul>
    <li><b>Flux balance analysis (FBA)</b> is a form of analysis done with linear programming, which finds solutions to pathways subjected to flux constraints and an objective function specified by the user.</li><br>
    <li><b>Simple knock-out analysis</b> which loops through reactions, constraining the flux of one (or a combination) of reaction(s) to zero (meaning knocked out).</li><br>
    <li><b>Flux scan analysis</b> increases the flux of a product and identifies the reactions whose flux decreases.</li><br>
    <li><b>Evolutionary algorithms (optGene)</b> is a Bio-inspired algorithm for optimising the set of knock-outs in order to maximise chemical production</li><br>
    <li><b>Metabolic flux analysis</b> discussed below.</li><br>
    <li><b>Metabolic pathway analysis:</b></li><br>
    <ul>
        <li><b>Elementary mode analysis</b> identifies all possible solutions (see <i>elementary modes</i>) of the metabolic network and finds the minimum number of knock-outs required to remove all pathways that do not produce the product.</li><br>
        <li><b>Extreme pathway analysis</b>Similar to elementary mode analysis but with additional constraint of making all extreme pathways systematically independent. This implies that none of the pathways can be expressed as a non-negative combination of at least two other extreme pathways.</li><br>
    </ul>
    <li><b>Input-Output Stoichiometry</b> discussed below</li>
</ul>

<br>
<h4>Theory of Analysing a Metabolic Network</h4>
<p>The first principle of analysing a metabolic network is mass conversion. Within any given network, no mass can be lost or gained from nothing. The general equation to describe mass conversion of metabolites can be written as:
  
\begin{equation*}
\frac{d}{dt}\underline{C} = 
\underline{\underline{S}} \cdot \underline{r} - \mu \cdot \underline{C}
\end{equation*}
<ul>
    <li>$\frac{d}{dt}$ <i>is the instantaneous rate of change of a particular physical quantity</i></li><br>
    <li>$\underline{C}$ <i>is the concentration</i> (mol/L) <i>vector of <em>m</em> internal metabolites</i></li><br>
    <li>$\underline{r}$ (mol/L/h) <i>is the reaction rate (flux) vector of <em>n</em> reactions that convert metabolites. It is defined by the cellular physiological state of a cell under a given growth condition and consists of weighted average of all elementary modes that are present.</i></li><br>
    <li>$\underline{\underline{S}}$ <i>is the stoichiometry matrix of dimension <em>m</em> x <em>n</em> whose elements <em>s<sub>ij</sub></em> represents the stoichiometry coefficient of the element </i>i<i> involved in reaction </i>j</li><br>
    <li>$\mu$ (1/h) <i>is the specific dilution rate associated with the change in volume of the system</i></li>
</ul>

<br>
Under steady state, there is no accumulation of internal metabolites and therefore the equation can be simplified to $\underline{\underline{S}} \cdot \underline{r} = 0$. As seen before, many reactions are irreversible and will have constraints placed on the positive flux value. This means that the flux of irriversible reactions (<em>r<sub>i</sub></em>) in $\underline{r}$ will have to be greater than or equal to zero (<em>r<sub>i</sub></em> $\geq$ 0). By focusing on the equation in steady state, we can note two things: the number of metabolites define the number of balanced equations (like 1A -> 1B) and the number of reactions represents the number of unknowns (Trinh et al., 2009). We can apply three popular forms of analysis to solve this equation and will be discussed as follows:</p>

<h6>Metabolic flux analysis (needs work)</h6>
<p>The concept behind <i>metabolic flux analysis</i> is to determine the unmeasurable reaction flux and stoichiometry matrix from the remaining (measurable) reaction rates and the measured stoichiometry matrix of a known condition (measurable). This is represented as: $$\underline{\underline{S}}_u \cdot \underline{r}_u = \underline{\underline{S}}_m \cdot \underline{r}_m$$ The letters have the same meaning as our first equation but include the distinction of measurable flux vector (r<sub>u</sub>) and unmeasurable flux vector (r<sub>u</sub>). This analysis will require experimental data to inform formulate the unmeasured stoichiometry matrix: $$\underline{r}_u = -\underline{\underline{S}}_u^{-1} \cdot \underline{\underline{S}}_m \cdot \underline{r}_m$$</p>

<h6>Flux balance analysis</h6>
<p>This form of analysis is covered in more detail under the <i>Linear Programming</i> section in the ScrumPy chapter. <i>Flux balance analysis</i> is about solving the metabolic flux vector $\underline{r}$ when little is known of the measurable vector $\underline{r}_m$ and the unmeasurable stoichiometry matrix cannot be inverted to offer a unique solution. It only identifies one optimal solution and other optimal solutions or sub-optimal solutions are often missed but can exist. This form of analysis takes a number of restraints imposed by the user. </p>

<h6>Metabolic pathway analysis</h6>
<p>This form of analysis can identify all metabolic flux vectors existing in a metabolic network withou requiring knowledge of any fixed flux rates or imposing objective functions for cellular metabolism. However, by applying the constraints of non-decomposability and systematic independence can form a finite set of solutions. Two forms of analysis apply these constraints to identify feasible pathways: elementary mode analysis and extreme pathway analysis. </p>
    
    
<h6>Determination of Metabolic Flux Vector (Trinh, Wlaschin and Scrienc, 2009)</h6>
<p>A metabolic flux vector is defined by the cellular physiological state of a cell under a given growth condition and consists of a weighted average of all elementary modes that are present. It shows what participating reactions are active and how fluxes through these reactions describe the physiological state. Knowledge of the metabolic flux vector helps in understanding the cell physiology when perturbations such as genetic modifications and growth conditions are imposed on cell growth. Since metabolic pathway analysis can identify all genetically independent pathways inherent in a metabolic network, any pathway or a non-negative linear combination of pathways such as elementary modes or extreme pathways can describe the physiological states of cellular metabolism under different growth conditions. However, the challenging tasks are to figure out how to assign weighting factors to elementary modes or extreme pathways to describe a physiological state of interest and how to determine these weighting factors when they change from one physiological state to another in response to growth perturbations. Several different approaches using metabolic pathway analysis have been reported with encouraging results.</p>


<h6>The Principles of Flux Minimisation (Holzh&uuml;tter, 2004)</h6>
<p>Linear programming and flux balance analysis (FBA) are two concepts discussed a number of times in this notebook and for good reason. It allows for exploration of how the metabolic network adapts to changes when a metabolite constraint is applied or excitation of a given pathway. Flux minimisation explores the metabolic network in a "stationary phase", whereby a microbe might downregulate functions in order to adapt to nutrient limitation. Ultimately, investigating how a metabolic network maintains vital cellular functions with minimal effort. This has been converted into a mathematical method whereby the total flux in a network is measured by a weighted linear combination of all individual fluxes and the thermodynamic equilibrium constants are used as weighting factors. This is useful for assessing stationary flux rates when a detailed kinetic model is not available.</p>

<h4>Input-Output Stoichiometry</h4>
<p>There is some biotechnical applications to be made with modelling; if we focus on all the individual elements (like oxygen, hydrogen and so on) in a reaction, we can determine the efficiency of production. For example, lets take the production of lysine used in animal feed. To make lysine we need glucose, oxygen and ammonia, this will produce lysine, carbon dioxide and water. Let's put this into an equation; each molecule is assigned a letter (except lysine) representing the number to balance the equation, and the addition/loss of a molecule is represented by plus or minus:</p>
<blockquote>-<em>a</em>.C<sub>6</sub>H<sub>12</sub>O<sub>6</sub> - <em>b</em>.O<sub>2</sub> - <em>c</em>.NH<sub>3</sub> + C<sub>6</sub>H<sub>14</sub>N<sub>2</sub>O<sub>2</sub> + <em>d</em>.CO<sub>2</sub> + <em>e</em>.H<sub>2</sub>O = 0<br>
Glucose - Oxygen - Ammonia + Lysine + Carbon Dioxide + Water = 0</blockquote>
<p>This is quite different from a typical balanced representation of a reaction (this equation isn't balanced for starters). The zero implies there is no net loss or gain of elements as they have all been converted into another molecule (obeying laws of mass conversion). The equation is not balanced as you can see it would take two ammonia to meet the nitrogen requirement for lysine.<br><br>
    
Let's explore reaction balancing a bit further. Starting with Nitrogen (N), we would need two ammonia for the equation to balance $-c+2=0$. The number 2 represents the number atoms of that element are present in lysine, and <em>c</em> refers to ammonia (which is also 2 to balance the equation).
    
<br>The balanced equation for hydrogen (H) is: $$a = \frac{e+4}{6}$$
<br>For one molecule of glucose (<em>a</em>), one hydrogen per ammonia is given to lysine and two hydrogen towards water (meaning <em>e</em> is 2) which balances the equation. 
    
For carbon (<em>C</em>) to balance, it is carbon dioxide (<em>d</em>) in relation to glucose (<em>a</em>) - which somehow works.<br>
For oxygen (O) to balance, substituting <em>a</em>, <em>c</em> and <em>d</em> gives $b=e-3$. If we assume <em>b</em> cannot be negative (no oxygen evolution) then <em>e</em> &#8805; 3. 

By using these kinds of equations, we can work out the largest theoretical molar yield of lysine per glucose. We will represent lysine as <em>1</em> and glucose as <em>a</em> as per our equation:
\begin{equation*} 
    \frac{1}{a} = \frac{6}{e+4} = \frac{6}{7} = 86\% 
\end{equation*}
    
This is how we can start to apply modelling to biotechnology and manipulate the model to find ways of improving yield.</p><hr />
    

<h1>ScrumPy</h1>
<h3>Introduction</h3>
<p>At the start of this notebook, I described what ScrumPy is and what it can be used for. Thus far, we've talked about the background of metabolic models and what we can do with them. It's time to start applying this knowledge to ScrumPy. This chapter discusses how to make a metabolic model, the terminology used in ScrumPy and how to use ScrumPy for your analysis of metabolic models.</p>


<h3>Construction of Genome-Scale Models</h3>
<p>Compared to the small, customised model used so far, genome-scale models are much bigger in scope and we don't define or know the contents of the model. Although we can pick our favourite organism and get the data from a database (see Data Sources for Metabolic Models), there are notable problems to be aware of. (1) Mis-annotation of reactions, absent reactions or false reactions; (2) non-specific metabolites (e.g. "some-tRNA", "Long-chain-fatty-acids", "an alcohol"); and (3) incorrect stoichiometries. Polymers can be problematic in terms of getting the correct stoichiometry and sometimes violates mass conversion. For homopolymers, the solution can be to rewrite reactions in terms of monomeric units. These problems can be identified through analysis of the left null-space or via linear programming.</p>

<h3>Data Sources for Metabolic Models</h3>
<p>There are numerous sources to go to for reactions and metabolites. More generally, these can be the biochemical literature like books, reviews and journal articles. Alternatively, there are several databases:
    <ul>
        <li>BioCyc: http://biocyc.org/</li>
        <li>KEGG: http://www.genome.jp/kegg/</li>
        <li>IntEnz: http://www.ebi.ac.uk/intenz/</li>
        <li>EXPASY Enzyme: https://enzyme.expasy.org/</li>
        <li>Brenda: http://www.brenda-enzymes.info</li>
</ul>
Enzyme-finding tools based on sequence signature (alternatives to BLAST homology searching):
<ul>
    <li>PRIAM</li>
    <li>theSEED (part of KBASE http://kbase.us)</li>
    <li>EfiCAZ</li>
</ul>
A valid structural models requires a reaction list in which:
<ul>
    <li>Every internal metabolite is both produced and consumed, either by an enzyme or a transporter</li>
    <li>The metabolites that exchange with the environment or between compartments, usually via transporters, can be identified</li>
    <li>Every enzyme/transporter in the list has a role in at least one pathway</li>
    <li>The metabolic network should form a single connected component</li>
</ul>
    </p>

<h3>Loading and Defining Models</h3>

<p>
    The ScrumPy modelling tool is started through the command terminal (type <em>ScrumPy</em> or <em>ScrumPy2&</em> in your chosen directory) and will start up a window. Upon launch, you will be greeted with two bodies of text: a blue text containing the ScrumPy details and version, and a black text showing the version of Python. You may also notice some diagnostics appearing in the command prompt; this can largely be ignored. ScrumPy will generate a lot of output to the terminal and can be suppressed by redirecting as stdout or stderr when starting through the command terminal (ScrumPy 2&>/dev/null).
    
To load or create a model, use the command <b>m = ScrumPy.Model('file.spy')</b>, provided the file was stored in the directory from where ScrumPy was launched. If a file is not provided, a GUI will open for selecting a model. If you wish to try out a small model, use the following text when prompted to define a model:<br>
<pre>Structural()
    
A_tx:
    x_A -> A
    ~
R_1:
    A -> B
    ~
R_2:
    B -> C
    ~
R_3:
    C -> E
    ~
R_4:
    B -> D
    ~
R_5:
    D -> E
    ~
R_6:
    D -> F
    ~
E_tx:
    E -> x_E
    ~</pre>
Once you have pasted this small model into the editor, use Compile in the ScrumPy drop down menu.</p>

<h3>ScrumPy Definitions</h3>
<p>In ScrumPy, a model is defined by one or more text files containing the following:<br>
<ul>
    <li><b>Comments</b> (text read by the user and ignored by the computer)</li>
    <li><b>Reactions</b></li>
    <li><b>Identifiers</b></li>
    <li><b>Initialisations</b> </li>
    <li><b>Directives</b></li>
</ul>
    
    
<h4>Reactions</h4>
<p>A reaction is a building block of a metabolic network (alongside metabolites); ScrumPy requires reactions to be given with three components: its name, stoichiometry and kinetic statement (strictly in that order):
<pre>Reac1:
      a -> b
      V1 * (a-b/keq1)</pre>
The reaction's name is on the first line. Line 2 contains the stoichiometry, showing one mol of <em>a</em> converting into one mol <em>b</em> and the direcion of transformation. A number can be placed before the substrate to specify how many moles of each are coverted (i.e. 3 a -> 2 b). These numbers can be represented as integers, floats or rational numbers. Line 3 contains the kinetic (or rate) law, our example is specifying the rate constant V1 and an equilibrium constant of keq1. In our example, the stoichiometry specifies the reaction is irriversible, but the rate law is reversible. This does not cause any problems in Scrumy because kinetic and structural functionallity are seperated from each other. In instances where the modeller wishes to only carry out structural analysis on the model, the kinetic statement can be replaced with a tilde (~) as seen in our toy model.


<h4>Identifiers</h4>
<p>The named components of a reaction (reaction name, metabolites and parameters) are collectively referred to as identifiers. These can be quoted ("example") or unquoted (example). For an unquoted identifier, it must start with a letter, can contain letters, digits and underscores, but cannot include spaces (likely due to how strings are spliced with Python). If a model is going to be strictly used for structural analysis, then it will likely be more convenient to use quoted identifiers. Define parameter values and initial metabolite concentrations for only kinetic models. In ScrumPy, the reaction and substrate names will have identifiers; transport reactions will have the suffix "_tx". Extracellular metabolites will also have the prefix "x_" to distinguish them.</p>


<h4>Initialisations</h4>
<p>Parameters and concentrations can be assigned values of numbers or other defined values (like equations) - this is referred to as initialisation.<br>
<pre>V1 = 42
V2 = V1 * 5</pre>
Values will be treated as concentrations if they have appeared in stoichiometry of at least one reaction. Any other value will be assumed to be a parameter. A parameter left unitialised will be set to the internal value of 'NaN' (meaning not a number) and no valid kinetic analysis can be performed until set. Concentrations left unitialised will be set to a default value of zero but this can lead to severe problems in networks containing cycles.</p>


<h4>Directives</h4>
<p>Directives are user instructions to the model, you can find a list of these in the cheat sheet at the bottom of this page. In Python, these would be described as functions/methods.
    
Within the model, the stoichiometry matrices will use rational numbers (i.e. fractions). Thus, they will be represented as 1/2 or mpq(1,2). This can be changed with ElType(), for large genome scale models it is more common to use real numbers and will require EiType(float).<br>
You can print sections of the stoichiometry matrix with the following:

<pre>>>> print(model.sm[0]) #prints the first row of the matrix as a list
    [mpq(1,1), mpq(0,1), ...]
    
>>> print(model.sm["Substrate"]) #prints the row as a dictionary
    [mpq(1,1), mpq(0,1),...]</pre>
    
Individual elements can be accessed as matrix[row, col]
<pre>>>> print(model.sm[0,0])
    1/1</pre>
The null space of a matrix can be accessed with <em>matrix.NullSpace()</em></p>

<h3>Linear Programming with ScrumPy</h3>
<p>This section aims to discuss how linear programming can be utilised in ScrumPy for Flux Balance Analysis (FBA). Linear programming tries to calculate solutions to the equation $Nv = 0$ (<em>N</em> stoichiometry matrix; <em>v</em> vector of enzyme kinetics) when additional information is supplied by the user. The concept is to define some limits for the flux of reactions and specify whether you want the model to aim for the maximum or minimum boundary of your defined limits. To perform linear programming in ScrumPy, generate a linear programme associated with a model and assign to an object:<br>
    
<pre>lp = model.GetLp()</pre>

This generates an instance object representing the linear programme of the model and allows manipulation of the <em>lp</em> object.

Advantages: (1) very fast; (2) integrates flux data; (3) easy to reformulate the problem and solve again; (4) the reactions in a solution can be extracted from the main model for more detailed analysis. Disadvantages: (1) only provides a single solution; (2) potential for numerical instability; (3) potential for multiple optima; (4) choice of the objective is subjective.</p>


<h4>Setting Constraints</h4>
<p>To begin with, the <em>lp</em> object has two sets of constraints: (1) the steady state assumption and (2) for irreversible reactions to carry positive or zero flux. Reversible reactions are handled internally and there is no need to explicitly split reversible reactions into their forward and reverse components. Flux bounds represent the upper and lower limits of flux a reaction can have. To set up flux bounds, use <em>lp.SetFluxBounds(BDict)</em> method whereby <em>BDict</em> is a Python dictionary (keys = reaction names, values = tuple of lower and upper flux bound). For example:</p>


```python
lp = model.GetLP()

Bounds = {
    "Glucose_tx" : (0, 1),
    "CO2_tx" : (-1, 0),
    "EtOH_tx" : (-2, 0)
}

lp.SetFluxBounds(Bounds)
```

<p>In the example above, you will notice that transport reactions contain flux. A positive flux represents import of a metabolite and, conversely, negative flux represents export. While the example uses transport reactions, flux bounds can be applied to any reaction. The flux bounds can also be removed at any time by specifying the Python constant <em>None</em>. Setting a negative bound on an irreversible reaction will generate an exception (and can be ignored). If you wish to set the upper and low bounds to the same value, you can do so with the <em>SetFluxBounds()</em> method, alternatively, the <em>SetFixedFlux(Dict)</em> method can be used. A constraint (flux bound) can be removed from a reaction with the <em>ClearFluxConstraint(reac)</em> method.</p>

<h4>Setting the Objective Function</h4>
<p>After the constraints have been made for our reactions, a direction/function is given to the linear programme as to whether the model should maximise or minimise the activity of a single reaction. This is achieved with setting the objective direction <em>SetObjDirec()</em>. Let's have a look:</p>


```python
lp.SetObjDirec("Min") #minimisation of a reaction flux
lp.SetObjDirec("Max") #maximisation of a reaction flux
lp.SetObjDirec()      #default = minimisation

#if any other argument is given, it will be ignored and an exception generated. 
#This sets the direction we want a reaction to go in.

#Specify which reactions are to be minimised/maximised with a list:
lp.SetObjective(["CO2_tx"]) #assign direction to this reaction, i.e. minimise or maximise CO2 loss/gain.

#The linear programme can then be solved with the following:
lp.Solve()
sol = lp.GetPrimSol()
len(sol)
print(sol)

#Filtering solutions - examples of printing transport reactions:
#1
for r in sol:
    if r.endswith("_tx"):
        print(r, sol[r])

#2
for r in filter(lambda s: s.endswith("_tx"), sol):
    print(r, sol[r])
```

<h2>Notes</h2>
<p>This section provides a space for taking notes not strictly related to the material covered in this notebook. For example, material from published articles or books about ideas or methods which you would like to take note of.</p>
<br><br>
<h5>Metabolic modelling ATP</h5>
<p>This material comes from Hartman et al., (2014) with notes regarding ATP synthesis and energy status of metabolic models. In their model, they use the equation:<br><br>
&nbsp; &nbsp; 4NADH + 9H<sub>i</sub><sup>+</sup> + 2O<sub>2</sub> + 5ADP + 5P<sub>i</sub> -> 4NAD + 9H<sub>2</sub>O + 5ATP<br>
Giving a P/O ration of 1.25 which compares to reported value of 1.33. In their methodology, they used linear programming (FBA) on ATP synthesis:<br>
    
minimise : $|v|$ (objective function)<br>
subject to $\begin{cases} N_v = 0 & \quad \text{(steady state)} \\ v_j = t_j;0\leq j \leq X  & \quad \text{(biomass production)} \end{cases}$ <br>
    
Their objective was to minimise the sum of all fluxes to the steady-state constraint (no metabolites allowed to accumulate) and producing the X biomass precursors at a rate determined by their relative abundance specified in the vector <em>t</em>, which collects the experimentally determined concentrations of all major biomass components, multiplied by a growth rate. The authors note that it is possile for the model to violate laws of energy conservation as a result of reactions with incorrectly defined directionality or reversibility leading to cycles that can generate ATP with no net consumption of substrate. Therefore, they modified the equation above to test for such conditions:<br>

minimise : $|v|$<br>
subject to $\begin{cases} N_v = 0 \\ v_{ATPase}=1 \\ v_j = t_j ; 0 \leq j \leq Y \end{cases}$ <br>
    
where $v_{ATPase}$ represents the flux in an arbitrary ATPase reaction and <em>Y</em> is the number of all transporters. Any possible solution represents an energetic inconsistency, and reactions therein examined and the model consequently corrected.</p>
    
    
<br><br> 
    
<h5>Kinetics of Firefly Luciferase</h5>
<p>This material comes from Lundin (2000) and covers the enzymatics and kinetics of luciferase firefly, a biolminescent enzyme which emits light in the prescence of ATP. The firefly luciferase goes through four reactions to emit light:<br>
    <pre>
           Luciferase + ATP + D-luciferin > luciferase(luciferyl-adenylate) + PP<sub>i</sub>              (1)
     Luciferase(luciferyl-adenylate) + O<sub>2</sub> > luciferase(oxyluciferin; AMP) + CO<sub>2</sub>                (2)
            Luciferase(oxyluciferin; AMP) > luciferase(oxyluciferin; AMP) + photon             (3) 
            Luciferase(oxyluciferin; AMP) > luciferase + oxyluciferin + AMP                    (4)
    </pre>
    
The quantum yield from this reaction is 0.88, almost one photon per ATP (Seliger and McElroy, 1960). Reaction 4 is inherintly slow without an enhancer like DTT and coenzyme A, or some nucleotides. If no enhancer is provided, only a flash of light is obtained. For reaction 2, the presence of enhancers like PP<sub>i</sub> causes the reaction to be rate limiting. A stoichiometry matrix of this reaction:</p>

<!--This is the HTML containing the stoichiometry matrix for luciferase reactions-->
<table>
    <th><td>ATP</td> <td>D-luciferin</td> <td>luciferyl-adenylate</td> <td>PP<sub>i</sub></td> <td>O<sub>2</sub></td> <td>Oxyluciferin; AMP</td> <td>CO<sub>2</sub></td> <td>Photon</td> <td>Oxyluciferin</td> <td>AMP</td><th>
    <tr>
		<td>R1</td>
		<td>-1</td>
		<td>-1</td>
		<td>1</td>
		<td>1</td>
		<td>0</td>
		<td>0</td>
		<td>0</td>
		<td>0</td>
		<td>0</td>
		<td>0</td>
	</tr>
    <tr>
		<td>R2</td>
		<td>0</td>
		<td>0</td>
		<td>-1</td>
		<td>0</td>
		<td>-1</td>
		<td>1</td>
		<td>1</td>
		<td>0</td>
		<td>0</td>
		<td>0</td>
	</tr>
    <tr>
		<td>R3</td>
		<td>0</td>
		<td>0</td>
		<td>0</td>
		<td>0</td>
		<td>0</td>
		<td>0</td>
		<td>0</td>
		<td>1</td>
		<td>0</td>
		<td>0</td>
	</tr>
    <tr>
		<td>R4</td>
		<td>0</td>
		<td>0</td>
		<td>0</td>
		<td>0</td>
		<td>0</td>
		<td>-1</td>
		<td>0</td>
		<td>0</td>
		<td>1</td>
		<td>1</td>
	</tr>  
</table>

<p>Under the conditions of where luciferase causes a flash of light (in contrast to sustained light), kinetics can be used to determine the rate of ATP degredation. A few assumptions apply: firstly, luciferase is not inactivated by the formation of enzyme-product complexes nor by sample components. Secondly, there are no ATP-degrading enzymes other than luciferase. If we assume fireflu luciferase follows the Michaelis-Menten equation (as discussed previously in this notebook), the rate of ATP degredation is: <br><br>
    
\begin{equation*} \frac{v}{V_{max}} = \frac{S}{S+K_m} \quad \text{(5)} \end{equation*}
    
<br>This equation can be simplified because in most cases the ATP concentration (S) is very low compared to the Michaelis-Menten constant (<em>K<sub>m</sub></em>), therefore:<br><br>
    
\begin{equation*} \frac{v}{S} = \frac{V_{max}}{K_m} \quad \textrm{or} \quad v=k \cdot S \quad \text{(6)} \end{equation*}
<br>
Whereby $k = V_{max}/K_m$ is the first order rate constant for the degredation of ATP. The unit is min<sup>-1</sup> and is a measure of the fraction of ATP degraded per minute when ATP concentraion is $ATP \ll K_m$. Because $v=-d[ATP]/dt$ and $S=[ATP]$, it can be simplified as such:<br><br>
    
$$-d[ATP]/dt = k[ATP] \quad \text{or} \quad -d[ATP]/[ATP] = kdt \quad \text{(7)}$$
    <br>
    $$=$$
    <br>
    $$[ATP_t] = [ATP_0]e^{-kt} \quad \text{(8)}$$
    
<br>If we assume the factor between light intensity (<em>I</em>) and ATP concentration is the same throughout the measurement, we can replace ATP concentration with light intensity:<br><br>
    
\begin{equation*} I_t = I_0e^{-kt} \quad \text{(9)} \end{equation*}
    
<br>The exponential decay of light emission will have the same <em>k</em> value regardless of where on the curve it is measured. Therefore, <em>k</em> can be calculated from light emission values obtained at any two times (t1 and t2):<br><br>
    
\begin{equation*} k = \frac{ln I_{t1} - lnI_{t2}}{t2-t1} \quad \text{(10)} \end{equation*}
    <br>
    
Using the <em>k</em> value from the above equation and measuring the light emission <em>I<sub>t1</sub></em> at time <em>t1</em>, an extrapolated peak light intensity, <em>I<sub>0</sub></em>, can be calcuted from equation 9:<br><br>
    
\begin{equation*} I_0 = \frac{I_{t1}}{e^{-kt1}} \quad \text{(11)} \end{equation*}

   

<h2>References</h2>


<h2>Cheat Sheet for ScrumPy</h2>
<p>Listed here are methods (functions) associated with the model. Some methods can be used with a variable like <em>m = ScrumPy.Model('toy_model.spy')</em> and use m.method() to call the method.<br><br>
    <table> 
        <tr><td><b>.Model([File (optional)])</b></td> <td> open/create model.</td></tr>
        <tr><td><b>.sm</b> and <b>.smexterns</b></td> <td>Fields for the internal and external stoichiometry metrices associated with the model.</td></tr>
        <tr><td><b>.ConsMoieties()</b></td><td> returns a list of conserved moieties.</td></tr>
        <tr><td><b>.DeadReactions()</b></td> <td>returns a list of reactions that cannot carry steady state flux.</td></tr>
        <tr><td><b>.FindIsoforms()</b></td> <td>identifies reactions that are redundant (set of reactions with identical stoichiometry).</td></tr>
        <tr><td><b>.ElModes()</b> .mo .sto .Modes() .Stos()</td> <td>ElModes can be called with a model and assigned to a variable. Using <em>mo</em> returns a matrix, similar to null space, from the model of the elementary modes of the network. <em>sto</em> returns a matrix of the relationship between modes and metabolites. Methods <em>Modes()</em> and <em>Stos()</em> return a string of their respective function.</td></tr>
        <tr><td><b>External(metabolite_id)</b></td> <td>Specify external metaboltes. Takes a comma delimited list.</td></tr>
        <tr><td><b>.Externals()</b></td> <td>returns a list of external metabolites</td></tr>
        <tr><td><b>.ElType()</b></td> <td>Changes the value within a stoichiometry matrix (options: rat, float, int, str, bool). Default=rat, arbitrary precision rational which has the advantage of eliminating rounding errors. </td></tr>
        <tr><td><b>.NullSpace()</b></td> <td>To access the null-space from the matrix</td></tr>
        <tr><td><b>Structural()</b></td> <td>Specifies the model will only be subjected to structural analysis. Saving time and memory and should always be used for genome-scale models.</td></tr>
        <tr><td><b>DeQuote()</b></td> <td>Removes quotation marks from identifiers.</td></tr>
        <tr><td><b>Include(FileNames)</b></td> <td>Allows modularisation of the model by splitting into seperate files. Example: a genome scale model where one set of reactions originate from a database and the other file contains reactions added by the user.</td></tr>
        <tr><td><b>.cnames</b></td> <td>Returns the column names of the stoichiometry matrix.</td></tr>
        <tr><td><b>.rnames</b></td> <td>Returns the row names of the stoichiometry matrix</td></tr>
        <tr><td><b>.ReacToStr()</b></td> <td>Is a method of the matrix (sm.ReacToStr(reac)) which returns the reaction as it was inputted into the model.</td></tr>
        <tr><td><b>.InvolvedWith(name)</b></td> <td>Returns the neighbouring elements, either neighbouring reactions or substrates depending on the input. If a reaction is given, the adjacent substrates will be returned. Vice versa if a substrate is given.</td></tr>
        <tr><td><b>.GetIrrevs()</b></td> <td>Returns a list of irreversible reactions from the stoichiometry matrix (i.e. reactions without <>)</td></tr>
        <tr><td><b>.MakeRevers(reac)</b></td> <td>Converts an irriversible reaction to a reversible one from the stoichiometry matrix.</td></tr>
        <tr><td><b>.Reload()</b></td> <td>Reloads the model and reverses the unsaved changes.</td></tr>
        <tr><td><b>.OrphanMets()</b></td> <td>An orphan metabolite is a metabolite that cannot be balanced at steady state as it is involved in only one reaction. It can only be consumed or produced. This function returns a list of those metabolites from the model.</td></tr>
        <tr><td><b>.EnzSubsets()</b></td> <td>Returns a dictionary of nested dictionaries of all the enzymatic subsets in the model. The reaction names are keys and the flux ratio is the value. The key <em>DeadReacs</em> is a list of dead reactions</td></tr>
        <tr><td><b>.GetLP()</b></td> <td>Generates a linear programme associated with a model</td></tr>
        <tr><td><b>.SetFluxBounds(dict)</b></td> <td>Sets the flux bounds of a linear programme. Takes a Python dictionary as an argument whereby keys = reaction name, values = a tuple of upper and lower flux bounds.</td></tr>
        <tr><td><b>.SetFixedFlux(dict)</b></td> <td>In linear programming, the fluxes of reaction can be fixed to a single value using a dictionary whereby keys = reaction name, values = flux.</td></tr>
        <tr><td><b>.ClearFluxConstraint(reac)</b></td> <td>Clears the flux bounds applied to a reaction. Takes the reaction's name as an argument.</td></tr>
        <tr><td><b>.SetObjDirec()</b></td> <td>Takes arguments "Min" and "Max", defaults to min if left blank. Assigns the direction of flux for reactions in a linear programme.</td></tr>
        <tr><td><b>.SetObjective([list])</b></td> <td>Takes a list of reactions as an argument. The object directive is then applied to the list of reactions once set.</td></tr>
        <tr><td><b>.Solve()</b></td> <td>Solves the linear programme</td></tr>
        <tr><td><b>.GetPrimSol()</b></td> <td>In linear programming, this function returns an optimal solution set after .Solve() has been called</td></tr>
        <tr><td><b>.Eval()</b></td> <td>Forces a re-evaluation of the rates with current parameters and concentration values. Must be called upon when changes are made in order to take effect.</td></tr>
        <tr><td><b>.GetVec()</b></td><td></td></tr>
        <tr><td><b>.SetVec()</b></td> <td></td></tr>     
</table>

</p>


```python

```
