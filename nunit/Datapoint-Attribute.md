The <b>Datapoint</b> attribute is used
to provide data for <b>Theories</b> and is ignored for ordinary
tests - including tests with parameters.
   
When a Theory is loaded, NUnit creates arguments for each
of its parameters by using any fields of the same type
as the parameter annotated with the <b>DatapointAttribute</b>.
Fields must be members of the class containing the Theory
and their Type must exactly match the argument for which
data is being supplied.
       
#### Automatically Supplied Datapoints

It is normally not necessary to specify datapoints for 
<b>boolean</b> or <b>enum</b> arguments. 
NUnit automatically supplies values of <b>true</b> 
and <b>false</b> for <b>boolean</b> arguments and will supply all 
defined values of any enumeration.
   
If for some reason you don't wish to use all possible values, you
can override this behavior by supplying your own datapoints. If you
supply any datapoints for an argument, automatic datapoint generation 
is suppressed.
   
<h4>Example</h4>

For an example of use, see [[Theory Attribute]]
   
<h4>See also...</h4>

 * [[Theory Attribute]]
 * [[Parameterized Tests]]
   
