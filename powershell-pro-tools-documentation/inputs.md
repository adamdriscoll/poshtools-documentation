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
}
```

## Returning Actions to the User

There are three actions you can return to the user. They include sending a toast message, redirecting to a URL and replacing the Input card's content with different content. 

### Sending a toast message

To send a toast message, simply call New-UDInputAction with the -Toast parameter and pass in text you would like to toast the user with. 

```powershell
New-UDInput -Title "Find module version" -Endpoint {
    param($ModuleName) 

    # Get a module from the gallery
    $Module = Find-Module $ModuleName

    New-UDInputAction -Toast $Module.Version
}

```

### Redirecting to a URL

To redirect to a URL, use the RedirectUrl parameter of New-UDInputAction. 

```powershell
New-UDInput -Title "Find module version" -Endpoint {
    param($ModuleName) 

    # Get a module from the gallery
    $Module = Find-Module $ModuleName

    New-UDInputAction -RedirectUrl $Module.ProjectUri
}

```

If you provide a relative path, you can redirect the user to a dynamic page. 

```powershell
New-UDInput -Title "Find module version" -Endpoint {
    param($ModuleName) 

    # Get a module from the gallery
    $Module = Find-Module $ModuleName

    New-UDInputAction -RedirectUrl "/module/$ModuleName"
}

```

### Replacing the contents of the input card

You can replace the contents of the input card with different content by using the Content parameter and returning one or more components. 

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



