<small>Piwik\DataTable\Filter\</small>

ColumnCallbackDeleteRow
=======================

Deletes all rows for which a callback returns true.

**Basic usage example**

    $labelsToRemove = array('label1', 'label2', 'label2');
    $dataTable->filter('ColumnCallbackDeleteRow', array('label', function ($label) use ($labelsToRemove) {
        return in_array($label, $labelsToRemove);
    }));

Methods
-------

The class defines the following methods:

- [`__construct()`](#__construct) &mdash; Constructor.
- [`filter()`](#filter) &mdash; Manipulates a DataTable in some way.
- [`enableRecursive()`](#enablerecursive) &mdash; Enables/Disables recursive filtering. Inherited from [`BaseFilter`](../../../Piwik/DataTable/BaseFilter.md)
- [`filterSubTable()`](#filtersubtable) &mdash; Filters a row's subtable, if one exists and is loaded in memory. Inherited from [`BaseFilter`](../../../Piwik/DataTable/BaseFilter.md)

<a name="__construct" id="__construct"></a>
<a name="__construct" id="__construct"></a>
### `__construct()`

Constructor.

#### Signature

-  It accepts the following parameter(s):
    - `$table` ([`DataTable`](../../../Piwik/DataTable.md)) &mdash;
       The DataTable that will be filtered eventually.
    - `$columnsToFilter` (`array`|`string`) &mdash;
       The column or array of columns that should be passed to the callback.
    - `$function` (`Piwik\DataTable\Filter\callback`) &mdash;
       The callback that determines whether a row should be deleted or not. Should return `true` if the row should be deleted.
    - `$functionParams` (`array`) &mdash;
       deprecated - use an [anonymous function](http://php.net/manual/en/functions.anonymous.php) instead.

<a name="filter" id="filter"></a>
<a name="filter" id="filter"></a>
### `filter()`

Manipulates a DataTable in some way.

#### Signature

-  It accepts the following parameter(s):
    - `$table` ([`DataTable`](../../../Piwik/DataTable.md)) &mdash;
      
- It does not return anything.

<a name="enablerecursive" id="enablerecursive"></a>
<a name="enableRecursive" id="enableRecursive"></a>
### `enableRecursive()`

Enables/Disables recursive filtering.

Whether this property is actually used
is up to the derived BaseFilter class.

#### Signature

-  It accepts the following parameter(s):
    - `$enable` (`bool`) &mdash;
      
- It does not return anything.

<a name="filtersubtable" id="filtersubtable"></a>
<a name="filterSubTable" id="filterSubTable"></a>
### `filterSubTable()`

Filters a row's subtable, if one exists and is loaded in memory.

#### Signature

-  It accepts the following parameter(s):
    - `$row` ([`Row`](../../../Piwik/DataTable/Row.md)) &mdash;
       The row whose subtable should be filter.
- It does not return anything.

