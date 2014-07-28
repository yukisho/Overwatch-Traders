Overwatch-Traders
=================

Installation:
(credits go to xBowBii & kat http://epochmod.com/forum/index.php?/topic/14090-tutorialmethod-how-to-add-itemsvehiclesweapons-to-traders-method-2/ )

Required
- Acces to Epoch Client files, namely "dayz_epoch_b" PBO.
- PBO Manager, to unpack that PBO.
- Server files that are going to get modified:
      - Description.Ext
      - Init.sqf
 
Attention
By using this technique, the traders are not going to use the database anymore (ex: Epoch will not check the trader prices of the DB anymore, but the ones of our files.)
So if you already added items to traders, you will have to add them back, but knowing the future ones will be eaiser to add ;-)
 
Explanation of how the system works.
Using external files, we are going to modify the traders using their own prices, own configs.
Example:

    type = "trade_weapons";
    buy[] = {1,"ItemGoldBar10oz"};
    sell[] = {5,"ItemGoldBar"};
    display = "DMR";
    qty[] = 1;

 
Easier tutorial for those who are more confortable with scripting:

1. UnPBO "dayz_epoch_b" located in your client files

2. Copy the "CfgTraderConfig" folder in your mission pbo

3. Add the following to your init.sqf, or set it to true if you already added that variable but set to false.

      DZE_ConfigTrader = true;
 
4. Open description.ext and add

      #include "CfgServerTrader\cfgServerTrader.hpp"

5. After downloading, unpack the zip file.
Copy over all contents to CfgServerTrader\Category\
You can edit the files to your liking.
To load these files you need to add the following to CfgServerTrader\cfgServerTrader.hpp

      #include "Category\OverwatchACR.hpp"
      #include "Category\OverwatchAK.hpp"
      #include "Category\OverwatchG3.hpp"
      #include "Category\OverwatchAmmo.hpp"
      #include "Category\Overwatch417.hpp"
      #include "Category\Overwatch416.hpp"
      #include "Category\OverwatchScar.hpp"
      #include "Category\OverwatchPistols.hpp"
      #include "Category\OverwatchSniper.hpp"
      #include "Category\OverwatchMasada.hpp"
      #include "Category\OverwatchLMG.hpp"
	
6. Done
 
Extended tutorial:

Step 1 (Assuming you already installed PBO Manager.)
Find your Arma 2 Operation Arrowhead folder, where your Epoch Client files are located.
For steam users it should be:

C:\Program Files (x86)\Steam\SteamApps\common\Arma 2 Operation Arrowhead\@DayZ_Epoch
Once you found that folder, go into the 'Addons' folder located in @DayZ_Epoch.
You should find a file called "dayz_epoch_b" with .pbo as extention.
Right clic on it, you should see a 'PBO Manager' option. Get on that option, and select

"Extract to dayz_epoch_b\".
 
Step 2
Once that files in UnPBO'd you should see in the UnPBO'd folder called "dayz_epoch_b" a folder called
"CfgServerTrader". Copy that folder into your unPBO'd mission file so that the "CfgServerTrader" folder is in the same folder as init.sqf, mission.sqm and Description.ext.
 
Step 3
Open up init.sqf using a GOOD file editor, as Notepad++ or even Sublime Text 2 ( :wub: )
Find a line called "// DayZ Epoch config"
Under it, you should see some Epoch Variables as DZE_requireplot, DZE_vehicleAmmo etc.
First of all, be sure to check if you don't already have that Epoch Variable but set to false.
If not, write

    DZE_ConfigTrader = true;  

under "// DayZ Epoch config".
If you already have 

    DZE_ConfigTrader = false;

put it to true so it looks like 

    DZE_ConfigTrader = true;


Step 4
Open Description.Ext, again using a GOOD text editor :lol:
Before ALL the other lines, put

      #include "CfgServerTrader\cfgServerTrader.hpp"

Done!! Now I am going to explain in-depth how it works. 
 
Once these steps above are done, you can modify the trader prices, the easy way.
Lets explain how the system works but more in depth:
 

I will use "BanditAmmunition.hpp" as example.
First of all, open the file of your choice (in our case "BanditAmmunition.hpp")

    class Category_577 {

As you can see, this hpp file is the config of the Ammunition that the Bandit Trader is selling with as TID 577.
 

After that it is really easy to use;
in case you want to sell "5Rnd_127x99_AS50" (as50 ammo) you will have to create a new class, under

    class Category_577 {

so it will look like:

    class Category_577 {
        class 5Rnd_127x99_AS50 {

After creating a new class under the Category_TID you can add kind of 'variables' to it;

    type =
    buy[] =
    sell[] =

As type, you will have to put

    type = "trade_items";
    type = "trade_any_vehicle";
    type = "trade_backpacks";
    type = "trade_weapons";

depending on if you are selling/buying a vehicle, an item, a backpack or a weapon.
 
After type, there is buy[] and sell[].
These have to be in this format:
HowMuchX,"X"
Example for our AS50 ammo;

    buy[] = {1,"ItemGoldBar10oz"};
    sell[]= {1,"ItemGoldBar10oz"};

You can use all kind of items, I suggest ItemGoldBar,ItemGoldBar10oz,ItemBriefcase100oz but ya know, you could use ItemMap as economy
