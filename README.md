There are countless strange issues with Microsoft products. 
Most of the bad ones can be found in Azure and Teams. 
Here's a running list of issues I have with Microsoft products.
**This is a living list; I update it constantly.**

- [Microsoft Teams](#microsoft-teams)
    - [General Messaging](#general-messaging)
    - [Mobile-Specific Issues](#mobile-specific-issues)
- [Microsoft Azure](#microsoft-azure)
    - [Azure Groups](#azure-groups)
    - [Azure APIM](#azure-apim)
- [VSCode with PowerShell](#vscode-with-powershell)
    - [Azure PowerShell Function Development](#azure-powershell-function-development)

## Microsoft Teams

Teams drives me crazy. 
Some things, like the Teams themselves, work really well, while most everything else makes me want to pull my hair out.

### General Messaging

These issues relate to sending and receiving messages in Teams.

1. Clicking on an image in a chat works 40% of the time.
    - The other 60% of the time, Teams just opens a blank tab and refuses to load anything.
    - This issue is way worse on Mobile devices too (Android -- I haven't tested iOS).

### Mobile-Specific Issues

These issues are specific to the Teams mobile app.

1. The "typing" animation thing plays atop message previews in the Chat list.
    - This looks incredibly lazy and I'm shocked this was even released.
    - The simplest solution is to hide the preview text wh

## Microsoft Azure

Not a day goes by without a fresh Azure issue cropping up. 
I keep a running tally of issues as I go about my day.

### Azure Groups

These issues relate to the Groups feature in Azure.

1. Adding members to a group doesn't immediately display them once you save.
    - You have to either refresh the page explicitly (which works around 50% of the time), or you have to wait for around 1 minute to see your changes reflected in the page.

### Azure APIM

These issues relate to the API manager in Azure.

1. You cannot add groups directly to an APIM product.
    - You have to add a group to your API first and then switch back to the Products page. Why it can't just let you search for groups from within the Products page is beyond me.

## VSCode with PowerShell

VSCode is absolutely amazing, when you're not writing PowerShell.

### Azure PowerShell Function Development

These issues relate to developing Azure PowerShell Functions in VSCode.

1. The debugger will reliably crash between runs unless I explicitly kill all existing PowerShell terminals in the editor.
    - This has to happen every time a change is made to the code. As you can imagine, this gets old quick. 
    - If you don't do this, either VSCode will explode (a flood of error messages related to reusing the old PS1 terminal) or the debugger will disconnect from the executing function. The latter is particularly upsetting. If you set some breakpoints and try to trigger them via a Postman request, you'll be stuck scratching your head wondering why none of them pause execution.
2. When debugging Azure Functions with PowerShell, breakpoints set inside functions only work like half the time. I'm serious.
    - You have to set breakpoints in the main caller and then manually step-into the function you want to debug. Of course, when you go to show this to someone, the debugger magically gets its shit together. Maybe I need to pair-program full-time...
