# Grids

Grids output data similar to tables but allow for searching, paging and sorting the data in the grid. Grids are produced using the jQuery DataTables library. Grids are created with the New-UDGrid cmdlet and data for the grid is output using the Out-UDGridData cmdlet.

The below script selects the Name, Id, WorkingSet and CPU of ProcessInfo objects returned by Get-Process. The gird auto refreshes every minute. ![](/assets/new-grid-example-script.png)The above script produces the following grid.

![](/assets/new-grid-example.png)

