# Inputs

New-UDInput allows you to create cards on the dashboard that take user input. The input can then be processed on the server and an action can be presented to the user on the dashboard.

## Creating a new input

To create a new input, use New-UDInput and specify the Endpoint parameter. The input on the form will automatically be generated based on the Param block within the Endpoint script block.

```powershell
New-UDInput -Title "User Data" -Endpoint {
      param($Name, [bool]$Yes)

    if ($Yes) {
        New-UDInputAction -Toast "Yes, $Name"
    } else {
        New-UDInputAction -Toast "No, $Name"
    }
}
```

The above input would produce the following card.

![](/assets/new-udinput)

New-UDInput currently generates textboxes and checkboxes. You can take any action you like within the Endpoint block. For example, you could look for a module in the PowerShell Gallery. 

```powershell
New-UDInput -Title "Module Info Locator" -Endpoint {
    param($ModuleName) 

    # Get a module from the gallery
    $Module = Find-Module $ModuleName

    # Output a new card based on that info
    New-UDInputAction -Content @(
        New-UDCard -Title "$ModuleName - $($Module.Version)" -Text $Module.Description
    )
}

```



