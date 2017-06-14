Test Filters represent a selection of tests to be displayed, run or loaded. When a filter needs to be passed to the framework, it is passed as a string containing an XML fragment. This page describes the elements present in the XML for a filter.

#### &lt;filter&gt;

This is the required top-level element for any filter. If it contains no other elements, it represents an empty filter. If it contains just one element, that element is used as the filter for all tests. If it contains multiple elements, it works like an **&lt;and&gt;** element.

Child elements allowed: **&lt;and&gt;**, **&lt;or&gt;**, **&lt;not&gt;**, **&lt;id&gt;**, **&lt;tests&gt;**, **&lt;cat&gt;**.

#### &lt;and&gt;

Represents an AndFilter. All contained filter elements must pass in order for this filter to pass.

Child elements allowed: **&lt;and&gt;**, **&lt;or&gt;**, **&lt;not&gt;**, **&lt;id&gt;**, **&lt;tests&gt;**, **&lt;cat&gt;**.

#### &lt;or&gt;

Represents an OrFilter. At least one contained filter element must pass in order for this filter to pass.

Child elements allowed: **&lt;and&gt;**, **&lt;or&gt;**, **&lt;not&gt;**, **&lt;id&gt;**, **&lt;tests&gt;**, **&lt;cat&gt;**.

#### &lt;not&gt;

Represents a NotFilter. The single contained filter element must fail in order for this filter to pass.

Child elements allowed: **&lt;and&gt;**, **&lt;or&gt;**, **&lt;not&gt;**, **&lt;id&gt;**, **&lt;tests&gt;**, **&lt;cat&gt;**.

#### &lt;id&gt;

Represents an IdFilter. The text of the element contains a single test id or multiple ids separated by commas. Since test ids are an internal construct, this filter is not useful externally. However, it is used by the NUnit Gui to efficiently select tests from the list of those loaded.

Child elements allowed: None.

#### &lt;tests&gt;

Represents a selection of test names. This element contains one or more **&lt;test&gt;** elements, each holding the full name of a test as it's inner text.

Child elements allowed: None.

#### &lt;cat&gt;

Represents a CategoryFilter. The text of the element contains a single category or multiple categories separated by commas.

Child elements allowed: None.

