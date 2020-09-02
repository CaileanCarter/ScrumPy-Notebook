<h2>Cheat Sheet for ScrumPy</h2>
<p>Listed here are methods (functions) associated with the model. Some methods can be used with a variable like <em>m = ScrumPy.Model('toy_model.spy')</em> and use m.method() to call the method.<br><br>



<table>
    <th><h2><b>Model</b></h2></th>
	<tr><td><b>AddDynMonitor</b></td> <td></td></tr>
	<tr><td><b>AddStatMonitor</b></td> <td></td></tr>
	<tr><td><b>ConsMoieties</b></td> <td>returns a list of conserved moieties.</td></tr>
	<tr><td><b>Core</b></td> <td></td></tr>
	<tr><td><b>DeadReactions</b></td> <td>returns a list of reactions that cannot carry steady state flux.</td></tr>
	<tr><td><b>DelIsoforms</b></td> <td></td></tr>
	<tr><td><b>DelReactions</b></td> <td></td></tr>
    <tr><td><b>DeQuote</b></td> <td>Removes quotation marks from identifiers.</td></tr>
	<tr><td><b>Destroy</b></td> <td></td></tr>
	<tr><td><b>DisconnectsK</b></td> <td></td></tr>
	<tr><td><b>ElModes .mo .sto .Modes() .Stos()</b></td> <td>ElModes can be called with a model and assigned to a variable. Using <em>mo</em> returns a matrix, similar to null space, from the model of the elementary modes of the network. <em>sto</em> returns a matrix of the relationship between modes and metabolites. Methods <em>Modes()</em> and <em>Stos()</em> return a string of their respective function.</td></tr>
    <tr><td><b>ElType</b></td> <td>Changes the value within a stoichiometry matrix (options: rat, float, int, str, bool). Default=rat, arbitrary precision rational which has the advantage of eliminating rounding errors. </td></tr>
	<tr><td><b>EnzSubsets</b></td> <td>Returns a dictionary of nested dictionaries of all the enzymatic subsets in the model. The reaction names are keys and the flux ratio is the value. The key <em>DeadReacs</em> is a list of dead reactions</td></tr>
	<tr><td><b>Eval</b></td> <td>Forces a re-evaluation of the rates with current parameters and concentration values. Must be called upon when changes are made in order to take effect.</td></tr>
    <tr><td><b>Externals</b></td> <td>returns a list of external metabolites</td></tr>
    <tr><td><b>External</b></td> <td>Specify external metaboltes. Takes a comma delimited list.</td></tr>
	<tr><td><b>FindIsoforms</b></td> <td>identifies reactions that are redundant (set of reactions with identical stoichiometry).</td></tr>
	<tr><td><b>FindSS</b></td> <td></td></tr>
	<tr><td><b>GetAllNames</b></td> <td></td></tr>
	<tr><td><b>GetConsMets</b></td> <td></td></tr>
	<tr><td><b>GetDepSols</b></td> <td></td></tr>
	<tr><td><b>GetEigValsJ</b></td> <td></td></tr>
	<tr><td><b>GetEquilDeps</b></td> <td></td></tr>
	<tr><td><b>GetFluxDesc</b></td> <td></td></tr>
	<tr><td><b>GetFluxDic</b></td> <td></td></tr>
	<tr><td><b>GetInitState</b></td> <td></td></tr>
	<tr><td><b>GetJac</b></td> <td></td></tr>
	<tr><td><b>GetLP</b></td> <td>Generates a linear programme associated with a model</td></tr>
	<tr><td><b>GetVals</b></td> <td></td></tr>
    <tr><td><b>GetVec</b></td> <td></td></tr>
	<tr><td><b>Hide</b></td> <td>Closes the model GUI (not the IDLE GUI)</td></tr>
    <tr><td><b>Include</b></td> <td>Allows modularisation of the model by splitting into seperate files. Example: a genome scale model where one set of reactions originate from a database and the other file contains reactions added by the user.</td></tr>
	<tr><td><b>Init</b></td> <td></td></tr>
	<tr><td><b>InitKin</b></td> <td></td></tr>
	<tr><td><b>IsIrrev</b></td> <td></td></tr>
	<tr><td><b>IsOK</b></td> <td>Checks if the model is OK.</td></tr>
	<tr><td><b>MaxCycles</b></td> <td></td></tr>
	<tr><td><b>NetSto</b></td> <td></td></tr>
	<tr><td><b>OrphanMets</b></td> <td>An orphan metabolite is a metabolite that cannot be balanced at steady state as it is involved in only one reaction. It can only be consumed or produced. This function returns a list of those metabolites from the model.</td></tr>
	<tr><td><b>PingConc</b></td> <td></td></tr>
	<tr><td><b>ReacTree</b></td> <td></td></tr>
	<tr><td><b>Reload</b></td> <td>Reloads the model and reverses the unsaved changes.</td></tr>
	<tr><td><b>RemMon</b></td> <td></td></tr>
	<tr><td><b>ScaledSensits</b></td> <td></td></tr>
	<tr><td><b>SetInitState</b></td> <td></td></tr>
	<tr><td><b>SetVals</b></td> <td></td></tr>
    <tr><td><b>SetVec</b></td> <td></td></tr>
	<tr><td><b>Show</b></td> <td>Shows the model GUI.</td></tr>
	<tr><td><b>ShowDepInfo</b></td> <td></td></tr>
	<tr><td><b>SimTo</b></td> <td></td></tr>
	<tr><td><b>Simulate</b></td> <td></td></tr>
    <tr><td><b>Structural</b></td> <td>Specifies the model will only be subjected to structural analysis. Saving time and memory and should always be used for genome-scale models.</td></tr>
	<tr><td><b>Transporters</b></td> <td></td></tr>
	<tr><td><b>Update</b></td> <td></td></tr>
	<tr><td><b>UpdateDynMons</b></td> <td></td></tr>
	<tr><td><b>UpdateStatMons</b></td> <td></td></tr>
	<tr><td><b>keys</b></td> <td></td></tr>
	<tr><td><b>md</b></td> <td></td></tr>
	<tr><td><b>sm</b></td> <td></td></tr>
	<tr><td><b>smx</b></td> <td></td></tr>
</table>
<br><br><br>

<table>
    <th><b><h2>Internal Stoichiometry Matrix</h2></b></th>
	<tr><td><b>AddAndRemoveRows</b></td> <td></td></tr>
	<tr><td><b>AddCol</b></td> <td></td></tr>
	<tr><td><b>AddRow</b></td> <td></td></tr>
	<tr><td><b>AdjMtx</b></td> <td></td></tr>
	<tr><td><b>AsEqn</b></td> <td></td></tr>
	<tr><td><b>AsEqns</b></td> <td></td></tr>
	<tr><td><b>AugCol</b></td> <td></td></tr>
	<tr><td><b>AugRow</b></td> <td></td></tr>
	<tr><td><b>ChangeType</b></td> <td></td></tr>
	<tr><td><b>Clear</b></td> <td></td></tr>
	<tr><td><b>ColDict</b></td> <td></td></tr>
	<tr><td><b>ColNZIdxs</b></td> <td></td></tr>
	<tr><td><b>ColNamesFromIdxs</b></td> <td></td></tr>
	<tr><td><b>ColReorder</b></td> <td></td></tr>
	<tr><td><b>ConnectedNet</b></td> <td></td></tr>
	<tr><td><b>ConnectedNets</b></td> <td></td></tr>
	<tr><td><b>Connectedness</b></td> <td></td></tr>
	<tr><td><b>Conv</b></td> <td></td></tr>
	<tr><td><b>Copy</b></td> <td></td></tr>
	<tr><td><b>DelCol</b></td> <td></td></tr>
	<tr><td><b>DelDupRows</b></td> <td></td></tr>
	<tr><td><b>DelReac</b></td> <td></td></tr>
	<tr><td><b>DelRow</b></td> <td></td></tr>
	<tr><td><b>Delete</b></td> <td></td></tr>
	<tr><td><b>Dims</b></td> <td></td></tr>
	<tr><td><b>DivCol</b></td> <td></td></tr>
	<tr><td><b>DivRow</b></td> <td></td></tr>
	<tr><td><b>DupRows</b></td> <td></td></tr>
	<tr><td><b>El2Str</b></td> <td></td></tr>
	<tr><td><b>ElTypeAsScrumPy</b></td> <td></td></tr>
	<tr><td><b>ElimCol</b></td> <td></td></tr>
	<tr><td><b>Externs</b></td><td>Returns a list of externals (which is none because this is intracellular)</td></tr>
	<tr><td><b>Filter</b></td> <td></td></tr>
	<tr><td><b>FindIsoforms</b></td> <td></td></tr>
	<tr><td><b>FromDicDic</b></td> <td></td></tr>
	<tr><td><b>FromDynMatrix</b></td> <td></td></tr>
	<tr><td><b>FromNumPyMtx</b></td> <td></td></tr>
	<tr><td><b>FromSciMtx</b></td> <td></td></tr>
	<tr><td><b>FunAllRows</b></td> <td></td></tr>
	<tr><td><b>FunCol</b></td> <td></td></tr>
	<tr><td><b>FunRow</b></td> <td></td></tr>
	<tr><td><b>GetCol</b></td> <td></td></tr>
	<tr><td><b>GetIrrevs</b></td> <td>Returns a list of irreversable reactions.</td></tr>
	<tr><td><b>GetRevs</b></td> <td></td></tr>
	<tr><td><b>GetRow</b></td> <td></td></tr>
	<tr><td><b>InitRows</b></td> <td></td></tr>
	<tr><td><b>InsertRow</b></td> <td></td></tr>
	<tr><td><b>IntegiseC</b></td> <td></td></tr>
	<tr><td><b>IntegiseR</b></td> <td></td></tr>
	<tr><td><b>IntegiseReacs</b></td> <td></td></tr>
	<tr><td><b>InvolvedWith</b></td> <td></td></tr>
	<tr><td><b>IsIrrev</b></td> <td></td></tr>
	<tr><td><b>LNullSpace</b></td> <td></td></tr>
	<tr><td><b>LOrthNullSpace</b></td> <td></td></tr>
	<tr><td><b>LoTriNames</b></td> <td></td></tr>
	<tr><td><b>MakeExtern</b></td> <td></td></tr>
	<tr><td><b>MakeFirstCol</b></td> <td></td></tr>
	<tr><td><b>MakeFirstRow</b></td> <td></td></tr>
	<tr><td><b>MakeIdent</b></td> <td></td></tr>
	<tr><td><b>MakeIrrev</b></td> <td>Make a reaction irreversable </td></tr>
	<tr><td><b>MakeLastCol</b></td> <td></td></tr>
	<tr><td><b>MakeLastRow</b></td> <td></td></tr>
	<tr><td><b>MakeRevers</b></td> <td></td></tr>
	<tr><td><b>MakeSeqSelfType</b></td> <td></td></tr>
	<tr><td><b>MakeZero</b></td> <td></td></tr>
	<tr><td><b>MaxCountRow</b></td> <td></td></tr>
	<tr><td><b>MaxInCol</b></td> <td></td></tr>
	<tr><td><b>MaxInRow</b></td> <td></td></tr>
	<tr><td><b>MinInCol</b></td> <td></td></tr>
	<tr><td><b>MinInRow</b></td> <td></td></tr>
	<tr><td><b>Mul</b></td> <td></td></tr>
	<tr><td><b>MulCol</b></td> <td></td></tr>
	<tr><td><b>MulRow</b></td> <td></td></tr>
	<tr><td><b>NZeroesInCol</b></td> <td></td></tr>
	<tr><td><b>NamesNonZeroesInCols</b></td> <td></td></tr>
	<tr><td><b>Neighbours</b></td> <td></td></tr>
	<tr><td><b>NewCol</b></td> <td></td></tr>
	<tr><td><b>NewEl</b></td> <td></td></tr>
	<tr><td><b>NewReaction</b></td> <td></td></tr>
	<tr><td><b>NewRow</b></td> <td></td></tr>
	<tr><td><b>NiceOrder</b></td> <td></td></tr>
	<tr><td><b>NonZeroR</b></td> <td></td></tr>
	<tr><td><b>NonZeroesInCols</b></td> <td></td></tr>
	<tr><td><b>NullSpace</b></td> <td></td></tr>
	<tr><td><b>OrphanMets</b></td> <td></td></tr>
	<tr><td><b>OrthNullSpace</b></td> <td></td></tr>
	<tr><td><b>OrthSubSysts</b></td> <td></td></tr>
	<tr><td><b>Orthogonalise</b></td> <td></td></tr>
	<tr><td><b>PosOfValsInCol</b></td> <td></td></tr>
	<tr><td><b>PosOfValsInRow</b></td> <td></td></tr>
	<tr><td><b>Products</b></td> <td>Takes a string reaction as argument and returns list of products in reaction</td></tr>
	<tr><td><b>PseudoInverse</b></td> <td></td></tr>
	<tr><td><b>RandColOrder</b></td> <td></td></tr>
	<tr><td><b>RandOrder</b></td> <td></td></tr>
	<tr><td><b>RandRowOrder</b></td> <td></td></tr>
	<tr><td><b>Range</b></td> <td></td></tr>
	<tr><td><b>RateVector</b></td> <td></td></tr>
	<tr><td><b>ReacToStr</b></td> <td></td></tr>
	<tr><td><b>Reactants</b></td> <td>Takes a string reaction as argument and returns list of reactants in reaction</td></tr>
	<tr><td><b>ReactionNJTree</b></td> <td></td></tr>
	<tr><td><b>ReadFile</b></td> <td></td></tr>
	<tr><td><b>RedRowEch</b></td> <td></td></tr>
	<tr><td><b>ReplaceNames</b></td> <td></td></tr>
	<tr><td><b>ResetRowNames</b></td> <td></td></tr>
	<tr><td><b>RevProps</b></td> <td></td></tr>
	<tr><td><b>RowDict</b></td> <td></td></tr>
	<tr><td><b>RowDiffMtx</b></td> <td></td></tr>
	<tr><td><b>RowDiffMtx2</b></td> <td></td></tr>
	<tr><td><b>RowDiffMtxFull</b></td> <td></td></tr>
	<tr><td><b>RowNZIdxs</b></td> <td></td></tr>
	<tr><td><b>RowNamesFromIdxs</b></td> <td></td></tr>
	<tr><td><b>RowReorder</b></td> <td></td></tr>
	<tr><td><b>RowsMatching</b></td> <td></td></tr>
	<tr><td><b>RowsWithSingCols</b></td> <td></td></tr>
	<tr><td><b>SetCol</b></td> <td></td></tr>
	<tr><td><b>SetEl</b></td> <td></td></tr>
	<tr><td><b>SetElStrRep</b></td> <td></td></tr>
	<tr><td><b>SetPivot</b></td> <td></td></tr>
	<tr><td><b>SetRow</b></td> <td></td></tr>
	<tr><td><b>SetSto</b></td> <td></td></tr>
	<tr><td><b>Sort</b></td> <td></td></tr>
	<tr><td><b>SortBy</b></td> <td></td></tr>
	<tr><td><b>SubCol</b></td> <td></td></tr>
	<tr><td><b>SubMtx</b></td> <td></td></tr>
	<tr><td><b>SubRow</b></td> <td></td></tr>
	<tr><td><b>SubSys</b></td> <td></td></tr>
	<tr><td><b>Substrates</b></td> <td></td></tr>
	<tr><td><b>SwapCol</b></td> <td></td></tr>
	<tr><td><b>SwapRow</b></td> <td></td></tr>
	<tr><td><b>ToCMtx</b></td> <td></td></tr>
	<tr><td><b>ToColDict</b></td> <td></td></tr>
	<tr><td><b>ToColList</b></td> <td></td></tr>
	<tr><td><b>ToDicDic</b></td> <td></td></tr>
	<tr><td><b>ToDict</b></td> <td></td></tr>
	<tr><td><b>ToFile</b></td> <td></td></tr>
	<tr><td><b>ToList</b></td> <td></td></tr>
	<tr><td><b>ToNJTree</b></td> <td></td></tr>
	<tr><td><b>ToNJTreeOld</b></td> <td></td></tr>
	<tr><td><b>ToOctaveMtx</b></td> <td></td></tr>
	<tr><td><b>ToSciMtx</b></td> <td></td></tr>
	<tr><td><b>ToScrumPy</b></td> <td></td></tr>
	<tr><td><b>ToStr</b></td> <td></td></tr>
	<tr><td><b>ToTexTab</b></td> <td></td></tr>
	<tr><td><b>Transporters</b></td> <td></td></tr>
	<tr><td><b>Transpose</b></td> <td></td></tr>
	<tr><td><b>Unbals</b></td> <td></td></tr>
	<tr><td><b>UpTri</b></td> <td></td></tr>
	<tr><td><b>UpTriNames</b></td> <td></td></tr>
	<tr><td><b>WriteFile</b></td> <td></td></tr>
	<tr><td><b>ZapZeroes</b></td> <td></td></tr>
	<tr><td><b>cnames</b></td> <td></td></tr>
	<tr><td><b>index</b></td> <td></td></tr>
	<tr><td><b>rnames</b></td> <td>Not a callable method (i.e. is an object). Returns list of metabolites.</td></tr>
	<tr><td><b>rows</b></td> <td></td></tr>
</table>


<table>
    <th><b><h2>External Stoichiometry Matrix</h2></b></th>
	<tr><td><b>AddAndRemoveRows</b></td> <td></td></tr>
	<tr><td><b>AddCol</b></td> <td></td></tr>
	<tr><td><b>AddRow</b></td> <td></td></tr>
	<tr><td><b>AdjMtx</b></td> <td></td></tr>
	<tr><td><b>AsEqn</b></td> <td></td></tr>
	<tr><td><b>AsEqns</b></td> <td></td></tr>
	<tr><td><b>AugCol</b></td> <td></td></tr>
	<tr><td><b>AugRow</b></td> <td></td></tr>
	<tr><td><b>ChangeType</b></td> <td></td></tr>
	<tr><td><b>Clear</b></td> <td></td></tr>
	<tr><td><b>ColDict</b></td> <td></td></tr>
	<tr><td><b>ColNZIdxs</b></td> <td></td></tr>
	<tr><td><b>ColNamesFromIdxs</b></td> <td></td></tr>
	<tr><td><b>ColReorder</b></td> <td></td></tr>
	<tr><td><b>ConnectedNet</b></td> <td></td></tr>
	<tr><td><b>ConnectedNets</b></td> <td></td></tr>
	<tr><td><b>Connectedness</b></td> <td></td></tr>
	<tr><td><b>Conv</b></td> <td></td></tr>
	<tr><td><b>Copy</b></td> <td></td></tr>
	<tr><td><b>DelCol</b></td> <td></td></tr>
	<tr><td><b>DelDupRows</b></td> <td></td></tr>
	<tr><td><b>DelReac</b></td> <td></td></tr>
	<tr><td><b>DelRow</b></td> <td></td></tr>
	<tr><td><b>Delete</b></td> <td></td></tr>
	<tr><td><b>Dims</b></td> <td></td></tr>
	<tr><td><b>DivCol</b></td> <td></td></tr>
	<tr><td><b>DivRow</b></td> <td></td></tr>
	<tr><td><b>DupRows</b></td> <td></td></tr>
	<tr><td><b>El2Str</b></td> <td></td></tr>
	<tr><td><b>ElTypeAsScrumPy</b></td> <td></td></tr>
	<tr><td><b>ElimCol</b></td> <td></td></tr>
	<tr><td><b>Externs</b></td> <td></td></tr>
	<tr><td><b>Filter</b></td> <td></td></tr>
	<tr><td><b>FindIsoforms</b></td> <td></td></tr>
	<tr><td><b>FromDicDic</b></td> <td></td></tr>
	<tr><td><b>FromDynMatrix</b></td> <td></td></tr>
	<tr><td><b>FromNumPyMtx</b></td> <td></td></tr>
	<tr><td><b>FromSciMtx</b></td> <td></td></tr>
	<tr><td><b>FunAllRows</b></td> <td></td></tr>
	<tr><td><b>FunCol</b></td> <td></td></tr>
	<tr><td><b>FunRow</b></td> <td></td></tr>
	<tr><td><b>GetCol</b></td> <td></td></tr>
	<tr><td><b>GetIrrevs</b></td> <td>Returns a list of irreversible reactions from the stoichiometry matrix (i.e. reactions without <>)</td></tr>
	<tr><td><b>GetRevs</b></td> <td></td></tr>
	<tr><td><b>GetRow</b></td> <td></td></tr>
	<tr><td><b>InitRows</b></td> <td></td></tr>
	<tr><td><b>InsertRow</b></td> <td></td></tr>
	<tr><td><b>IntegiseC</b></td> <td></td></tr>
	<tr><td><b>IntegiseR</b></td> <td></td></tr>
	<tr><td><b>IntegiseReacs</b></td> <td></td></tr>
	<tr><td><b>InvolvedWith</b></td> <td>Returns the neighbouring elements, either neighbouring reactions or substrates depending on the input. If a reaction is given, the adjacent substrates will be returned. Vice versa if a substrate is given.</td></tr>
	<tr><td><b>IsIrrev</b></td> <td></td></tr>
	<tr><td><b>LNullSpace</b></td> <td></td></tr>
	<tr><td><b>LOrthNullSpace</b></td> <td></td></tr>
	<tr><td><b>LoTriNames</b></td> <td></td></tr>
	<tr><td><b>MakeExtern</b></td> <td></td></tr>
	<tr><td><b>MakeFirstCol</b></td> <td></td></tr>
	<tr><td><b>MakeFirstRow</b></td> <td></td></tr>
	<tr><td><b>MakeIdent</b></td> <td></td></tr>
	<tr><td><b>MakeIrrev</b></td> <td></td></tr>
	<tr><td><b>MakeLastCol</b></td> <td></td></tr>
	<tr><td><b>MakeLastRow</b></td> <td></td></tr>
	<tr><td><b>MakeRevers</b></td> <td>Converts an irriversible reaction to a reversible one from the stoichiometry matrix.</td></tr>
	<tr><td><b>MakeSeqSelfType</b></td> <td></td></tr>
	<tr><td><b>MakeZero</b></td> <td></td></tr>
	<tr><td><b>MaxCountRow</b></td> <td></td></tr>
	<tr><td><b>MaxInCol</b></td> <td></td></tr>
	<tr><td><b>MaxInRow</b></td> <td></td></tr>
	<tr><td><b>MinInCol</b></td> <td></td></tr>
	<tr><td><b>MinInRow</b></td> <td></td></tr>
	<tr><td><b>Mul</b></td> <td></td></tr>
	<tr><td><b>MulCol</b></td> <td></td></tr>
	<tr><td><b>MulRow</b></td> <td></td></tr>
	<tr><td><b>NZeroesInCol</b></td> <td></td></tr>
	<tr><td><b>NamesNonZeroesInCols</b></td> <td></td></tr>
	<tr><td><b>Neighbours</b></td> <td></td></tr>
	<tr><td><b>NewCol</b></td> <td></td></tr>
	<tr><td><b>NewEl</b></td> <td></td></tr>
	<tr><td><b>NewReaction</b></td> <td></td></tr>
	<tr><td><b>NewRow</b></td> <td></td></tr>
	<tr><td><b>NiceOrder</b></td> <td></td></tr>
	<tr><td><b>NonZeroR</b></td> <td></td></tr>
	<tr><td><b>NonZeroesInCols</b></td> <td></td></tr>
	<tr><td><b>NullSpace</b></td> <td>To access the null-space from the matrix</td></tr>
	<tr><td><b>OrphanMets</b></td> <td></td></tr>
	<tr><td><b>OrthNullSpace</b></td> <td></td></tr>
	<tr><td><b>OrthSubSysts</b></td> <td></td></tr>
	<tr><td><b>Orthogonalise</b></td> <td></td></tr>
	<tr><td><b>PosOfValsInCol</b></td> <td></td></tr>
	<tr><td><b>PosOfValsInRow</b></td> <td></td></tr>
	<tr><td><b>Products</b></td> <td></td></tr>
	<tr><td><b>PseudoInverse</b></td> <td></td></tr>
	<tr><td><b>RandColOrder</b></td> <td></td></tr>
	<tr><td><b>RandOrder</b></td> <td></td></tr>
	<tr><td><b>RandRowOrder</b></td> <td></td></tr>
	<tr><td><b>Range</b></td> <td></td></tr>
	<tr><td><b>RateVector</b></td> <td></td></tr>
	<tr><td><b>ReacToStr</b></td> <td>Is a method of the matrix (sm.ReacToStr(reac)) which returns the reaction as it was inputted into the model.</td></tr>
	<tr><td><b>Reactants</b></td> <td></td></tr>
	<tr><td><b>ReactionNJTree</b></td> <td></td></tr>
	<tr><td><b>ReadFile</b></td> <td></td></tr>
	<tr><td><b>RedRowEch</b></td> <td></td></tr>
	<tr><td><b>ReplaceNames</b></td> <td></td></tr>
	<tr><td><b>ResetRowNames</b></td> <td></td></tr>
	<tr><td><b>RevProps</b></td> <td></td></tr>
	<tr><td><b>RowDict</b></td> <td></td></tr>
	<tr><td><b>RowDiffMtx</b></td> <td></td></tr>
	<tr><td><b>RowDiffMtx2</b></td> <td></td></tr>
	<tr><td><b>RowDiffMtxFull</b></td> <td></td></tr>
	<tr><td><b>RowNZIdxs</b></td> <td></td></tr>
	<tr><td><b>RowNamesFromIdxs</b></td> <td></td></tr>
	<tr><td><b>RowReorder</b></td> <td></td></tr>
	<tr><td><b>RowsMatching</b></td> <td></td></tr>
	<tr><td><b>RowsWithSingCols</b></td> <td></td></tr>
	<tr><td><b>SetCol</b></td> <td></td></tr>
	<tr><td><b>SetEl</b></td> <td></td></tr>
	<tr><td><b>SetElStrRep</b></td> <td></td></tr>
	<tr><td><b>SetPivot</b></td> <td></td></tr>
	<tr><td><b>SetRow</b></td> <td></td></tr>
	<tr><td><b>SetSto</b></td> <td></td></tr>
	<tr><td><b>Sort</b></td> <td></td></tr>
	<tr><td><b>SortBy</b></td> <td></td></tr>
	<tr><td><b>SubCol</b></td> <td></td></tr>
	<tr><td><b>SubMtx</b></td> <td></td></tr>
	<tr><td><b>SubRow</b></td> <td></td></tr>
	<tr><td><b>SubSys</b></td> <td></td></tr>
	<tr><td><b>Substrates</b></td> <td></td></tr>
	<tr><td><b>SwapCol</b></td> <td></td></tr>
	<tr><td><b>SwapRow</b></td> <td></td></tr>
	<tr><td><b>ToCMtx</b></td> <td></td></tr>
	<tr><td><b>ToColDict</b></td> <td></td></tr>
	<tr><td><b>ToColList</b></td> <td></td></tr>
	<tr><td><b>ToDicDic</b></td> <td></td></tr>
	<tr><td><b>ToDict</b></td> <td></td></tr>
	<tr><td><b>ToFile</b></td> <td></td></tr>
	<tr><td><b>ToList</b></td> <td></td></tr>
	<tr><td><b>ToNJTree</b></td> <td></td></tr>
	<tr><td><b>ToNJTreeOld</b></td> <td></td></tr>
	<tr><td><b>ToOctaveMtx</b></td> <td></td></tr>
	<tr><td><b>ToSciMtx</b></td> <td></td></tr>
	<tr><td><b>ToScrumPy</b></td> <td></td></tr>
	<tr><td><b>ToStr</b></td> <td></td></tr>
	<tr><td><b>ToTexTab</b></td> <td></td></tr>
	<tr><td><b>Transporters</b></td> <td></td></tr>
	<tr><td><b>Transpose</b></td> <td></td></tr>
	<tr><td><b>Unbals</b></td> <td></td></tr>
	<tr><td><b>UpTri</b></td> <td></td></tr>
	<tr><td><b>UpTriNames</b></td> <td></td></tr>
	<tr><td><b>WriteFile</b></td> <td></td></tr>
	<tr><td><b>ZapZeroes</b></td> <td></td></tr>
	<tr><td><b>_getrc</b></td> <td></td></tr>
	<tr><td><b>cnames</b></td> <td>Returns the column names of the stoichiometry matrix.</td></tr>
	<tr><td><b>index</b></td> <td></td></tr>
	<tr><td><b>rnames</b></td> <td>Returns the row names of the stoichiometry matrix</td></tr>
	<tr><td><b>rows</b></td> <td></td></tr>
</table>
<br><br><br>
<table>
    <th><b><h2>Linear Programming</h2></b></th>
	<tr><td><b>AddCols</b></td> <td></td></tr>
	<tr><td><b>AddRows</b></td> <td></td></tr>
	<tr><td><b>AddSumConstraint</b></td> <td></td></tr>
	<tr><td><b>CheckReac</b></td> <td></td></tr>
	<tr><td><b>CleanReacDic</b></td> <td></td></tr>
	<tr><td><b>CleanReacList</b></td> <td></td></tr>
	<tr><td><b>ClearFluxConstraint</b></td> <td>Clears the flux bounds applied to a reaction. Takes the reaction's name as an argument.</td></tr>
	<tr><td><b>ClearFluxConstraints</b></td> <td></td></tr>
	<tr><td><b>DelCols</b></td> <td></td></tr>
	<tr><td><b>DelRows</b></td> <td></td></tr>
	<tr><td><b>FiniteBoundFlux</b></td> <td></td></tr>
	<tr><td><b>GetClass</b></td> <td></td></tr>
	<tr><td><b>GetCol</b></td> <td></td></tr>
	<tr><td><b>GetColDual</b></td> <td></td></tr>
	<tr><td><b>GetColIdxs</b></td> <td></td></tr>
	<tr><td><b>GetColKind</b></td> <td></td></tr>
	<tr><td><b>GetColNames</b></td> <td></td></tr>
	<tr><td><b>GetColPrimal</b></td> <td></td></tr>
	<tr><td><b>GetDims</b></td> <td></td></tr>
	<tr><td><b>GetName</b></td> <td></td></tr>
	<tr><td><b>GetNumCols</b></td> <td></td></tr>
	<tr><td><b>GetNumRows</b></td> <td></td></tr>
	<tr><td><b>GetObjDir</b></td> <td></td></tr>
	<tr><td><b>GetObjName</b></td> <td></td></tr>
	<tr><td><b>GetObjVal</b></td> <td></td></tr>
	<tr><td><b>GetPrimSol</b></td> <td>In linear programming, this function returns an optimal solution set after .Solve() has been called</td></tr>
	<tr><td><b>GetReacNames</b></td> <td></td></tr>
	<tr><td><b>GetRow</b></td> <td></td></tr>
	<tr><td><b>GetRowDual</b></td> <td></td></tr>
	<tr><td><b>GetRowIdxs</b></td> <td></td></tr>
	<tr><td><b>GetRowName</b></td> <td></td></tr>
	<tr><td><b>GetRowNames</b></td> <td></td></tr>
	<tr><td><b>GetRowPrimal</b></td> <td></td></tr>
	<tr><td><b>GetRowsAsLists</b></td> <td></td></tr>
	<tr><td><b>GetSimplexAsMtx</b></td> <td></td></tr>
	<tr><td><b>GetStatus</b></td> <td></td></tr>
	<tr><td><b>GetStatusMsg</b></td> <td></td></tr>
	<tr><td><b>GetStatusSym</b></td> <td></td></tr>
	<tr><td><b>HasCol</b></td> <td></td></tr>
	<tr><td><b>HasRow</b></td> <td></td></tr>
	<tr><td><b>IsStatusOptimal</b></td> <td></td></tr>
	<tr><td><b>Klass</b></td> <td></td></tr>
	<tr><td><b>LoadMtxFromDic</b></td> <td></td></tr>
	<tr><td><b>LoadMtxFromLists</b></td> <td></td></tr>
	<tr><td><b>MatchFlux</b></td> <td></td></tr>
	<tr><td><b>ObjVal</b></td> <td></td></tr>
	<tr><td><b>PrintMtx</b></td> <td></td></tr>
	<tr><td><b>Read</b></td> <td></td></tr>
	<tr><td><b>SetColBounds</b></td> <td></td></tr>
	<tr><td><b>SetColName</b></td> <td></td></tr>
	<tr><td><b>SetFixedFlux</b></td> <td>In linear programming, the fluxes of reaction can be fixed to a single value using a dictionary whereby keys = reaction name, values = flux.</td></tr>
	<tr><td><b>SetFluxBounds</b></td> <td>Sets the flux bounds of a linear programme. Takes a Python dictionary as an argument whereby keys = reaction name, values = a tuple of upper and lower flux bounds.</td></tr>
	<tr><td><b>SetName</b></td> <td></td></tr>
	<tr><td><b>SetObjCoef</b></td> <td></td></tr>
	<tr><td><b>SetObjCoefsFromDic</b></td> <td></td></tr>
	<tr><td><b>SetObjCoefsFromLists</b></td> <td></td></tr>
	<tr><td><b>SetObjDir</b></td> <td></td></tr>
	<tr><td><b>SetObjDirec</b></td> <td>Takes arguments "Min" and "Max", defaults to min if left blank. Assigns the direction of flux for reactions in a linear programme.</td></tr>
	<tr><td><b>SetObjName</b></td> <td></td></tr>
	<tr><td><b>SetObjective</b></td> <td>Takes a list of reactions as an argument. The object directive is then applied to the list of reactions once set.</td></tr>
	<tr><td><b>SetRowBounds</b></td> <td></td></tr>
	<tr><td><b>SetRowName</b></td> <td></td></tr>
	<tr><td><b>SetRowVals</b></td> <td></td></tr>
	<tr><td><b>SetSumFluxConstraint</b></td> <td></td></tr>
	<tr><td><b>SolRateVector</b></td> <td></td></tr>
	<tr><td><b>SolStoDic</b></td> <td></td></tr>
	<tr><td><b>Solve</b></td> <td>Solves the linear programme</td></tr>
	<tr><td><b>UnboundFlux</b></td> <td></td></tr>
	<tr><td><b>Write</b></td> <td></td></tr>
	<tr><td><b>cidxs</b></td> <td></td></tr>
	<tr><td><b>cnames</b></td> <td></td></tr>
	<tr><td><b>lpx</b></td> <td></td></tr>
	<tr><td><b>model</b></td> <td></td></tr>
	<tr><td><b>ridxs</b></td> <td></td></tr>
	<tr><td><b>rnames</b></td> <td></td></tr>
	<tr><td><b>sm</b></td> <td></td></tr>
</table>




```python

```
