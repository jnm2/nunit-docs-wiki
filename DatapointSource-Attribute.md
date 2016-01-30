The <b>DatapointSource</b> attribute is used
to provide data for <b>Theories</b> and is ignored for ordinary
tests - including tests with parameters.
   
Collections of datapoints may be provided by use of the <b>DatapointSourceAttribute</b>.
This attribute may be placed on methods or
properties in addition to fields. The returned value must be
either an array of the required type or an <b>IEnumerable<T></b> returning an enumeration
of the required type. The data Type must exactly match the argument 
for which data is being supplied.
   
> In earlier versions of NUnit, the obsolete <b>DatapointsAttribute</b>
> was used in place of <b>DatapointSourceAttribute</b>.
   
####Automatically Supplied Datapoints

It is normally not necessary to specify datapoints for 
<b>boolean</b> or <b>enum</b> arguments.
NUnit automatically supplies values of <b>true</b> 
and <b>false</b> for <b>boolean</b> arguments and will supply all 
defined values of any enumeration.
   
If for some reason you don't wish to use all possible values, you
can override this behavior by supplying your own datapoints. If you
supply any datapoints for an argument, automatic datapoint generation 
is suppressed.
   
####Example

For an example of use, see [[Theory Attribute]]
   
<h4>See also...</h4>

 * [[Theory Attribute]]
 * [[Parameterized Tests]]
   
