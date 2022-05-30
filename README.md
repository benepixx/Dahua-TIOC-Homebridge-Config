# Dahua-TIOC-Homebridge-Config

Im just parking this config here so i dont forget how i did it. 

Status URL

http://{IPADDRESS}/cgi-bin/configManager.cgi?action=getConfig&name=DisableLinkage

Disable Linkage

http://{IPADDRESS}/cgi-bin/configManager.cgi?action=setConfig&DisableLinkage[0].Enable=false

Enable Linkage

http://{IPADDRESS}/cgi-bin/configManager.cgi?action=setConfig&DisableLinkage[0].Enable=true


This means disarmed “table.DisableLinkage.Enable=true”

This means armed “table.DisableLinkage.Enable=false”

So this was a lot more difficult. Firstly to the parse into usable data I had to stack a regex and a simple mapper. 

First mapper chomps the result of the GET status url. Essentially meaning anything that comes after a semicolon AND is True OR false, to move onto the next step. The simple mapper just then maps True/false to the correct number in HomeKit. 

Correct number in HomeKit is as follows:

* "0": stay armed
* "1": away armed
* "2": night armed
* "3": disarmed
* "4": alarm has been triggered

Im yet to implement the “triggered” state but could easily do this with alarm feedback. So stay tuned. 

Ive added the HTTP Switch config as seperate config file as that uses the "Homebridge Http Switch" Plugin to work

Im yet to Implement any other arming modes, such as not having the siren activate in home mode, so every arming state other than off is armed fully. (Away Mode) so even if you hit home mode it’ll change to away mode when the polling catches up with your request.
