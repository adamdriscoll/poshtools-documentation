# Formatting

The New-Row and New-Column cmdlets are used for formatting a dashboard. The row and column system is a PowerShell implementation of the Grid system found in [Materialize](http://materializecss.com/grid.html). Each row is broken down into 12 equally size areas. Each column can be 1-12 in size.

For example, the definition below would create a row with a single column that stretched the width of the page.

`New-Row -Columns {    
    New-Column -Size 12 {`

`}    
}`

To create two equally sized columns, you could make them both 6 in size.

`New-Row -Columns {    
    New-Column -Size 6 {`

`}    
    New-Column -Size 6 {`

`}    
}`

You can also nest rows with in columns.

`New-Row -Columns {    
    New-Column -Size 6 {`

```
        New-Row -Columns { 
```

`New-Column -Size 12 {    
               }`  
 `}    
       }`

`}    
    New-Column -Size 6 {`

`}    
}`

