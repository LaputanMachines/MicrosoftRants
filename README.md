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
    - [Azure App Insights](#azure-app-insights)
- [Microsoft KeyVault](#microsoft-keyvault)
    - [Secrets](#secrets)
- [VSCode with PowerShell](#vscode-with-powershell)
    - [Azure PowerShell Function Development](#azure-powershell-function-development)
- [Microsoft Outlook](#microsoft-outlook)
    - [Focus Time](#focus-time)
- [Powershell](#powershell)
    - [General Performance](#general-performance)
- [PowerBI](#powerbi)
    - [Filters](#filters)

## Microsoft Teams

### General Messaging

1. Clicking on an image in a chat works 40% of the time.
    - The other 60% of the time, Teams just opens a blank tab and refuses to load anything. This issue is way worse on Mobile devices too (Android -- I haven't tested iOS).
    ![image](https://user-images.githubusercontent.com/8591722/154140702-4f7105f2-492d-481a-b013-b4abffd3602d.png)
2. Lack of MD support while typing.
3. If you write some text, drop down to a new line, and then add a code block, you cannot write more regular text below the code block.
    - You have to delete the whole message and re-write it, or you have to switch to Slack because Slack isn't completely broken.
    ![image](https://user-images.githubusercontent.com/8591722/154123550-afc44e78-9a62-411c-8005-98b8fd03acc9.png)
4. Chat bubble pictures sometimes display incorrectly when you first start Teams
    - This only seems to affect bubbles with custom images -- default images aren't affected by this issue
    ![image](https://user-images.githubusercontent.com/8591722/163034842-2297117f-18f7-48b6-96a1-d28d304c6dfe.png)

### Mobile-Specific Issues

1. The "typing" animation thing plays atop message previews in the Chat list.
    - This looks incredibly lazy and I'm shocked this was even released. The simplest solution is to hide the preview text while someone is typing.

## Microsoft Azure

### Azure Functions

1. Errors take 1+ minutes to appear in the Invocations list.
    - When something fails to execute, you have to wait a while before any logs appear in the Monitor > Invocations screen.

### Azure Groups

1. Adding members to a group doesn't immediately display them once you save.
    - You have to either refresh the page explicitly (which works around 50% of the time), or you have to wait for around 1 minute to see your changes reflected in the page.

### Azure APIM

1. You cannot add groups directly to an APIM product.
    - You have to add a group to your API first and then switch back to the Products page. Why it can't just let you search for groups from within the Products page is beyond me.
2. Opening the Azure APIM Developer Portal as an admin enabled Edit Mode with no way to disable it.
    - Microsoft's "official" workflow is to use CTRL + CLICK to navigate the site, like some sort of animal. I rarely want to edit the portal page--I mainly want to test my API via the portal (what clients use). 

### Azure Vault

1. Access Policies list takes forever to load because Azure fetches the names of each principal ID in real-time.
    - Every time you want to add/remove/update an access policy, you have to wait an extra minute for all the names to load in. The physical list itself moved around as this happens to it's not like you can make changes while it's doing this.

### Azure App Insights

1. Hovering over existing Insights when attempting to change your resource does not change your cursor to a "pointer" icon
    - When you hover over something you can click on, your cursor should always turn into a little pointy finger

## Microsoft KeyVault

### Secrets

1. Deleting a secret via the API and then hitting the Refresh button in the Portal UI doesn't show that the secret was deleted
    - To reproduce this: create a secret in your vault. Then, use the Graph API to delete the secret. In the UI, click the Refresh button. Observe that the secret is still listed in the list -- if you click on the secret, Azure tells you that it no longer exists. You have to refresh the page to see the change. Why have a refresh button if it doesn't work? 

## VSCode with PowerShell

### Azure PowerShell Function Development

1. The debugger will reliably crash between runs unless I explicitly kill all existing PowerShell terminals in the editor.
    - This has to happen every time a change is made to the code. As you can imagine, this gets old quick. If you don't do this, either VSCode will explode (a flood of error messages related to reusing the old PS1 terminal) or the debugger will disconnect from the executing function. The latter is particularly upsetting. If you set some breakpoints and try to trigger them via a Postman request, you'll be stuck scratching your head wondering why none of them pause execution.
2. When debugging Azure Functions with PowerShell, breakpoints set inside functions only work like half the time. I'm serious.
    - You have to set breakpoints in the main caller and then manually step-into the function you want to debug. Of course, when you go to show this to someone, the debugger magically gets its shit together. Maybe I need to pair-program full-time...
    - UPDATE The debugger will never hit a breakpoint if it's on the first line of a function.

## Microsoft Outlook

### Focus Time

1. The automatically-created _focus time_ slots in the Calendar only capitalizes the first word
    - It would look much better if it read "Focus Time" instead of "Focus time"
    ![image](https://user-images.githubusercontent.com/8591722/159354205-6fe09d87-8e60-4eec-8524-85a4b825bd97.png)

## Powershell

### General Performance

1. The `Import-PSSession` function is known to leak memory 
    - We have always-online PS1 FunctionApps that need to be configured to auto-heal because `PSSessions` eat up a profound amount of memory and never relinquish resources. We contacted Microsoft and they confirmed that the function is leaky-af.

## PowerBI

### Filters

1. Unchecking month filters does not remove the selection from the dataset
    - Regardless of the months selected, the original selection remains checked. The worst part is that the data does not change to reflect your filter selections!
    ![powerbi-filter-issue](https://user-images.githubusercontent.com/8591722/175993273-fa5aca97-8cc9-4b95-9cd5-16886dd2c036.gif)
