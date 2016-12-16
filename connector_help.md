### neutriNote Connector User Guide

1. [Getting Started](#started)
1. [Tasker Support](#tasker)
1. [Support](#support)

#### <a name="started">Getting Started</a>
**neutriNote Connector** is the easiest way to sync **neutriNote** with **Dropbox**.  Just follow these steps:

1. Point to **Local Repository** of **neutriNote** under **Settings**.
1. Link to **Dropbox** using the button on the main screen.
1. Enable sync by going to your device's Settings, click **neutriNote Connector** under **Accounts**, and check the checkbox.  
    * The first sync would take a while to finish depending on the quantity of notes.  It also may reset the last modified time of notes.
    * If the above steps fail to trigger sync, tap **Resync All** from the menu.
    * Once the first sync completes, you can manual sync anytime by doing a pull-to-refresh from the main screen of **neutriNote**.

#### <a name="tasker">Tasker Support</a>
The syncing of **neutriNote Connector** can also alternatively be triggered by Tasker.  Simply create a new Tasker task similar to the one below:
```
A1: Send Intent [ 
Action:com.appmindlab.connector.ACTION_REQUEST_SYNC 
Cat:None 
Mime Type: 
Data: 
Extra: 
Extra: 
Extra: Package:com.appmindlab.connector
Class: Target:Broadcast Receiver ] 
```
#### <a name="support">Support</a>
What's next?  Join [Google+ community](https://plus.google.com/u/0/communities/117565395761503074053) to keep up with the app's latest development.

