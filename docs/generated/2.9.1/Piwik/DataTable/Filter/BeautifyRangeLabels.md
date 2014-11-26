<small>Piwik\DataTable\Filter\</small>

BeautifyRangeLabels
===================

A DataTable filter that replaces range label columns with prettier, human-friendlier versions.

When reports that summarize data over a set of ranges (such as the
reports in the **VisitorInterest** plugin) are archived, they are
archived with labels that read as: '$min-$max' or '$min+'. These labels
have no units and can look like '1-1'.

This filter can be used to clean up and add units to those range labels. To
do this, you supply a string to use when the range specifies only
one unit (ie '1-1') and another format string when the range specifies
more than one unit (ie '2-2', '3-5' or '6+').

This filter can be extended to vary exactly how ranges are prettified based
on the range values found in the DataTable. To see an example of this,
take a look at the [BeautifyTimeRangeLabels](/api-reference/Piwik/DataTable/Filter/BeautifyTimeRangeLabels) filter.

**Basic usage example**

    $dataTable->queueFilter('BeautifyRangeLabels', array("1 visit", "%s visits"));

Methods
-------

The class defines the following methods:

- [`__construct()`](#__construct) &mdash; Constructor.
- [`beautify()`](#beautify) &mdash; Beautifies a range label and returns the pretty result.
- [`getSingleUnitLabel()`](#getsingleunitlabel) &mdash; Beautifies and returns a range label whose range spans over one unit, ie 1-1, 2-2 or 3-3.
- [`getRangeLabel()`](#getrangelabel) &mdash; Beautifies and returns a range label whose range is bounded and spans over more than one unit, ie 1-5, 5-10 but NOT 11+.
- [`getUnboundedLabel()`](#getunboundedlabel) &mdash; Beautifies and returns a range label whose range is unbounded, ie 5+, 10+, etc.

<a name="__construct" id="__construct"></a>
<a name="__construct" id="__construct"></a>
### `__construct()`

Constructor.

#### Signature

-  It accepts the following parameter(s):
    - `$table` ([`DataTable`](../../../Piwik/DataTable.md)) &mdash;
       The DataTable that will be filtered.
    - `$labelSingular` (`string`) &mdash;
       The string to use when the range being beautified is equal to '1-1 units', eg `"1 visit"`.
    - `$labelPlural` (`string`) &mdash;
       The string to use when the range being beautified references more than one unit. This must be a format string that takes one string parameter, eg, `"%s visits"`.

<a name="beautify" id="beautify"></a>
<a name="beautify" id="beautify"></a>
### `beautify()`

Beautifies a range label and returns the pretty result.

See [BeautifyRangeLabels](/api-reference/Piwik/DataTable/Filter/BeautifyRangeLabels).

#### Signature

-  It accepts the following parameter(s):
    - `$value` (`string`) &mdash;
       The range string. This must be in either a '$min-$max' format a '$min+' format.

- *Returns:*  `string` &mdash;
    The pretty range label.

<a name="getsingleunitlabel" id="getsingleunitlabel"></a>
<a name="getSingleUnitLabel" id="getSingleUnitLabel"></a>
### `getSingleUnitLabel()`

Beautifies and returns a range label whose range spans over one unit, ie 1-1, 2-2 or 3-3.

This function can be overridden in derived types to customize beautifcation
behavior based on the range values.

#### Signature

-  It accepts the following parameter(s):
    - `$oldLabel` (`string`) &mdash;
       The original label value.
    - `$lowerBound` (`int`) &mdash;
       The lower bound of the range.

- *Returns:*  `string` &mdash;
    The pretty range label.

<a name="getrangelabel" id="getrangelabel"></a>
<a name="getRangeLabel" id="getRangeLabel"></a>
### `getRangeLabel()`

Beautifies and returns a range label whose range is bounded and spans over more than one unit, ie 1-5, 5-10 but NOT 11+.

This function can be overridden in derived types to customize beautifcation
behavior based on the range values.

#### Signature

-  It accepts the following parameter(s):
    - `$oldLabel` (`string`) &mdash;
       The original label value.
    - `$lowerBound` (`int`) &mdash;
       The lower bound of the range.
    - `$upperBound` (`int`) &mdash;
       The upper bound of the range.

- *Returns:*  `string` &mdash;
    The pretty range label.

<a name="getunboundedlabel" id="getunboundedlabel"></a>
<a name="getUnboundedLabel" id="getUnboundedLabel"></a>
### `getUnboundedLabel()`

Beautifies and returns a range label whose range is unbounded, ie 5+, 10+, etc.

This function can be overridden in derived types to customize beautifcation
behavior based on the range values.

#### Signature

-  It accepts the following parameter(s):
    - `$oldLabel` (`string`) &mdash;
       The original label value.
    - `$lowerBound` (`int`) &mdash;
       The lower bound of the range.

- *Returns:*  `string` &mdash;
    The pretty range label.

