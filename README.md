# Online Price Level User Event Script

## Description
This script is a User Event Script in the NetSuite SuiteScript 2.1 API. It is used to set the online price level of an inventory item. This price level is stored in a custom field (`custitem_onlineprice_for_schema`) on the item record, and is updated every time the item is created or edited. The value is formatted as a number with two decimal places.

## How it works
The script listens to the `beforeSubmit` event of the item record. In this event, it checks the new and old item records, and compares the online price levels between them. If there's a change in the online price level, the script updates the custom field with the new value. If there's no change, the script does nothing.

## Usage
To use this script, upload it to your NetSuite account and attach it as a User Event Script to the item record. The script will automatically run when the item is created or edited.

## Code Explanation

### Module Loading
The script begins by loading two standard modules, `N/record` and `N/ui/serverWidget`.

### The `beforeSubmit` Function
This function is called before the item record is submitted. It performs the main functionality of the script.

#### Variables
- `newRecord`: This is the item record that is about to be submitted.
- `oldRecord`: This is the item record as it was before the current editing session.
- `pricingSublistLineLevel`: This is the line number in the pricing sublist where the online price level is found.
- `newItemOnlinePrice`: This is the new online price level, as entered by the user in the current editing session.
- `oldItemOnlinePrice`: This is the old online price level, as it was before the current editing session.

#### If the record is newly created
If the item record is newly created (`context.type == context.UserEventType.CREATE`), the script sets the custom field to the new online price level and ends.

#### If the record is being edited
If the item record is being edited, the script first checks if the online price level has changed. If it hasn't, the script ends. If it has, the script updates the custom field to the new online price level.

---
**Disclaimer**: This script is provided as-is without any warranty. Always test scripts in a controlled environment before deploying.
Made By:
 ,--.-,,-,--,             .-._        ,--.--------.    ,----.                           ,--.-,  ,---.       _,.----.     _,.---._                 ,-,--.  
/==/  /|=|  |.--.-. .-.-./==/ \  .-._/==/,  -   , -\,-.--` , \  .-.,.---.              |==' -|.--.'  \    .' .' -   \  ,-.' , -  `.    _..---.  ,-.'-  _\ 
|==|_ ||=|, /==/ -|/=/  ||==|, \/ /, |==\.-.  - ,-./==|-  _.-` /==/  `   \             |==|- |\==\-/\ \  /==/  ,  ,-' /==/_,  ,  - \ .' .'.-. \/==/_ ,_.' 
|==| ,|/=| _|==| ,||=| -||==|-  \|  | `--`\==\- \  |==|   `.-.|==|-, .=., |          __|==|, |/==/-|_\ | |==|-   |  .|==|   .=.     /==/- '=' /\==\  \    
|==|- `-' _ |==|- | =/  ||==| ,  | -|      \==\_ \/==/_ ,    /|==|   '='  /       ,--.-'\=|- |\==\,   - \|==|_   `-' \==|_ : ;=:  - |==|-,   '  \==\ -\   
|==|  _     |==|,  \/ - ||==| -   _ |      |==|- ||==|    .-' |==|- ,   .'        |==|- |=/ ,|/==/ -   ,||==|   _  , |==| , '='     |==|  .=. \ _\==\ ,\  
|==|   .-. ,\==|-   ,   /|==|  /\ , |      |==|, ||==|_  ,`-._|==|_  . ,'.        |==|. /=| -/==/-  /\ - \==\.       /\==\ -    ,_ //==/- '=' ,/==/\/ _ | 
/==/, //=/  /==/ , _  .' /==/, | |- |      /==/ -//==/ ,     //==/  /\ ,  )       \==\, `-' /\==\ _.\=\.-'`-.`.___.-'  '.='. -   .'|==|   -   /\==\ - , / 
`--`-' `-`--`--`..---'   `--`./  `--`      `--`--``--`-----`` `--`-`--`--'         `--`----'  `--`                       `--`--''  `-._`.___,'  `--`---'  
