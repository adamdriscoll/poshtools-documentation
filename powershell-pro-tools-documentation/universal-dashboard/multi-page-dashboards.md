# Multi-Page Dashboards

## Creating a dashboard with multiple pages

Dashboards can be broken down into multiple pages by using the New-UDPage cmdlet along with New-UDDashboard's Pages parameter. Each page can have a name and icon. The name provides both the name of the page in the navigation bar but also the  URL for the page. The icon is displayed in the navigation bar along side the name.

An example multi-page dashboard would be as follows.

`$Page1 = New-UDPage -Name "Home" -Icon home -Content { New-UDCard }    
$Page2 = New-UDPage -Name "Links" -Icon link -Content { New-UDCard }    
New-UDDashboard -Pages @($Page1, $Page2)`

## Navigating Between Pages

Once you have created your multi-page dashboard, you will now have a hamburger menu icon available in the bottom left corner of the dashboard. Click the icon will pop out the dashboard navigation pane. Clicking the links will take you to the different pages of your dashboard. 

![](/assets/hamburger-menu.png)

![](/assets/navigation.png)

## Automatically Cycling Through Pages

Since dashboards may often be used for display purposes only, you can also enable auto-cycling of pages. On New-UDDashboard, specify the CyclePages and CyclePagesInterval parameters. CyclePagesInterval is the number of seconds to wait while displaying a dashboard page. 



