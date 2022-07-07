# O9 Gambling Script for Epoch 1.0.7.1+

O9 Gambling Script by Airwaves Man<br>

Works only if Z_singleCurrency = true;

# Index:

* [Mission folder install](https://github.com/AirwavesMan/Over9000-Gambling-Script#mission-folder-install)
* [BattlEye filter install](https://github.com/AirwavesMan/Over9000-Gambling-Script#battleye-filter-install)
* [Usage](https://github.com/AirwavesMan/Over9000-Gambling-Script#usage)

**[>> Download <<](https://github.com/AirwavesMan/Over9000-Gambling-Script/archive/refs/heads/master.zip)**

# Install:

* This install basically assumes you have a custom variables.sqf, compiles.sqf and fn_selfActions.sqf.

** If not, visit this repo and follow the steps there**
https://github.com/AirwavesMan/custom-epoch-functions


# Mission folder install:

1. 	Open your fn_selfactions.sqf and search for:

	```sqf
	// ZSC
	if (Z_singleCurrency) then {
	```

	Add this code lines above:
	
	```sqf
	if (Z_singleCurrency) then {	
		local _isGamble = _cursorTarget isKindOf "Hooker4"; // Define here the trader or the building where you get the gambling dialog
		if (_isGamble && _isAlive) then {			
			local _hasCards = "ItemCards" in magazines player;
			if (_hasCards) then {
				if (s_player_gamblefree < 0) then {
					s_player_gamblefree = player addAction [localize "STR_CL_GAMBLE_PRICEFREE", "scripts\gamble\gamble.sqf",0, 1, false, true];
				};
			};
			if (s_player_gamble1 < 0) then {
				s_player_gamble1 = player addAction [format [localize "STR_CL_GAMBLE_PRICE1x", CurrencyName], "scripts\gamble\gamble.sqf",1000, 1, false, true];
			};
			if (s_player_gamble2 < 0) then {
				s_player_gamble2 = player addAction [format [localize "STR_CL_GAMBLE_PRICE2x", CurrencyName], "scripts\gamble\gamble.sqf",2000, 1, false, true];
			};
			if (s_player_gamble3 < 0) then {
				s_player_gamble3 = player addAction [format [localize "STR_CL_GAMBLE_PRICE3x", CurrencyName], "scripts\gamble\gamble.sqf",3000, 1, false, true];
			};
		} else {
			player removeAction s_player_gamblefree;
			s_player_gamblefree = -1;
			player removeAction s_player_gamble1;
			s_player_gamble1 = -1;
			player removeAction s_player_gamble2;
			s_player_gamble2 = -1;
			player removeAction s_player_gamble3;
			s_player_gamble3 = -1;
		};
	};
	```
	
2. In fn_selfactions search for this codeblock:

	```sqf
	player removeAction s_bank_dialog3;
	s_bank_dialog3 = -1;
	player removeAction s_player_checkWallet;
	s_player_checkWallet = -1;	
	```	
	And add this below:
	
	```sqf
	player removeAction s_player_gamblefree;
	s_player_gamblefree = -1;
	player removeAction s_player_gamble1;
	s_player_gamble1 = -1;
	player removeAction s_player_gamble2;
	s_player_gamble2 = -1;
	player removeAction s_player_gamble3;
	s_player_gamble3 = -1;
	```
	
3. Open your variables.sqf and search for:

	```sqf
	s_bank_dialog3 = -1;
	s_player_checkWallet = -1;	
	```
	And add this below:
	
	```sqf
	s_player_gamblefree = -1;
	s_player_gamble1 = -1;
	s_player_gamble2 = -1;
	s_player_gamble3 = -1;
	```
	

4.	Open your description.ext and search for the class CfgSounds.

	**Inside** the class CfgSounds, add:

	```
	class tada
	{
		name="tada";
		sound[]={\scripts\gamble\tada.ogg,0.9,1};
		titles[] = {};
	};
	```

	If you don't have a CfgSounds class, add this to your description.ext:

	```
	class CfgSounds	{
		sounds[] = {tada};

		class tada
		{
			name="tada";
			sound[]={\scripts\gamble\tada.ogg,0.9,1};
			titles[] = {};
		};
	};
	```

	If you start the server and you get the error "class CfgSounds is already defined", you have to search your CfgSounds class in your other .hpp files.
<br>

# BattlEye filter install:

Not added so far

# Usage:

Define the trader or the building where you want to get the gambling option in the fn_selfactions here:

```sqf
_isGamble = _cursorTarget isKindOf "Hooker4";
```
Go to dayz_server\traders\YourMapName.sqf and add there the coordiantes and the trader you have defined above.
E.G.:

```sqf
["Hooker4",[6321,7781,0],9]
```
If you have defined a building, put it in your custom buildings you are loading on server start.

If you have Cards in your inventory, you get a free gambling try.<br>
You can gamble for 1000, 2000 and 3000 Coins and get the price 1x, 2x and 3x.<br>

The script is not optimized but it works out of the box and can be used with overpoch.
