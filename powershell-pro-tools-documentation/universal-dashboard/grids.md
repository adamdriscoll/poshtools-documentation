# Grids

Grids output data similar to tables but allow for paging and sorting the data in the grid. Grids are produced using the [Griddle ](https://griddlegriddle.github.io/Griddle/docs/)library. Grids are created with the New-UDGrid cmdlet and data for the grid is output using the Out-UDGridData cmdlet.

The below script selects the Name, Id, WorkingSet and CPU of ProcessInfo objects returned by Get-Process. The gird auto refreshes every minute.

```powershell
New-UdGrid -Title "Processes" -Headers @("Name", "ID", "Working Set", "CPU") -Properties @("Name", "Id", "WorkingSet", "CPU") -AutoRefresh -RefreshInterval 60 -Endpoint {
       Get-Process | Out-UDGridData
}
```

The above script produces the following grid.

![](/assets/griddle.png)

