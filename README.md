# UD-RangeSlider
A slider component for UD based on https://whoisandy.github.io/react-rangeslider/

## Parameters
* -Min this specifies the minimum number for the slider to start at
* -Max this specifies the maximum number which will be the last number on the slider
* -Step this is the increment the slider will increase on each movement of the slider
* -Orientation can either be horizontal or vertical

## Theme
 To get this to display I had to add the default theme.  However I thought it needed a few adjustments hence why the example
 script shows a custom theme being used

## Eample Script
Tried to make this as easier to use please note this is a test script to show how to use it, and obtain the value selected:-
```
Import-Module -Name UniversalDashboard.Community -RequiredVersion 2.8.1
Import-Module -Name UniversalDashboard.UDRangeSlider
Get-UDDashboard | Stop-UDDashboard
$theme = New-UDTheme -Name 'Basic' -Definition @{
    '.slider'                                             = @{
        height = "50px !important"
    }
    '.rangeslider'                                        = @{
        background = "#fe982c !important"
    }
    '.rangeslider-horizontal .rangeslider__handle::after' = @{
        'content' = "none !important"
    }
} -Parent "default"
Start-UDDashboard -Port 10005 -Dashboard (
    New-UDDashboard -Title "Powershell UniversalDashboard" -Theme $theme -Content {
        New-UDLayout -Columns 1 -Content {
            New-UDRangeSlider -id 'SLIDERCOMPONENT' -Min 150 -Max 200 -Step 5 -Orientation "vertical"
            New-UDButton -Text "TEST" -OnClick {
                $sliderValue = (Get-UDElement -id 'SLIDERCOMPONENT').Attributes.value
                Show-UDToast -Message "You selected $sliderValue"
            }
        }
    }
)

```
