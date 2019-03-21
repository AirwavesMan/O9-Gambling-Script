# Over9000 Gambling Script

Over9000 Gambling Script by A Man<br>
If you use it, please give credit<br>
Free to use in Salivals modPack<br>

Works only with ZSC: https://github.com/oiad/ZSC

<br>

**Installation:**

1.	Put the scripts folder from github into your missionfile root folder where your init.sqf is located.
2.	Open your fn_selfactions.sqf and search for:

	```sqf
	//Towing with tow truck
	```

	Add this code lines **above**:

	```sqf
	_isGamble = _cursorTarget isKindOf "Hooker4"; // Define here the trader or the building where you get the gambling dialog
	if (isNil "CurrencyName") then { _gambleCurrency = "Coins"; } else { _gambleCurrency = CurrencyName;};
	if (Z_singleCurrency && _isGamble && {_isAlive}) then {
		_hasCards = "ItemCards" in magazines player;
		if (_hasCards) then {
			if (s_player_gamblefree < 0) then {
				s_player_gamblefree = player addAction [localize "STR_CL_GAMBLE_PRICEFREE", "scripts\gamble\gamble.sqf",0, 1, false, true];
			};
		};
		if (s_player_gamble1 < 0) then {
			s_player_gamble1 = player addAction [format [localize "STR_CL_GAMBLE_PRICE1x", _gambleCurrency], "scripts\gamble\gamble.sqf",1000, 1, false, true];
		};
		if (s_player_gamble2 < 0) then {
			s_player_gamble2 = player addAction [format [localize "STR_CL_GAMBLE_PRICE2x", _gambleCurrency], "scripts\gamble\gamble.sqf",2000, 1, false, true];
		};
		if (s_player_gamble3 < 0) then {
			s_player_gamble3 = player addAction [format [localize "STR_CL_GAMBLE_PRICE3x", _gambleCurrency], "scripts\gamble\gamble.sqf",3000, 1, false, true];
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
	```

3.	In fn_selfactions search for this codeblock:

	```sqf
		player removeAction s_player_fuelauto2;
		s_player_fuelauto2 = -1;
		player removeAction s_player_manageDoor;
		s_player_manageDoor = -1;
	```

	And add this **below**:

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

4.	Open your variables.sqf and search for:

	```sqf
	s_player_manageDoor = -1;
	```

	And add behind this **below**:

	```sqf
	s_player_gamblefree = -1;
	s_player_gamble1 = -1;
	s_player_gamble2 = -1;
	s_player_gamble3 = -1;
	```

5.	Open your description.ext and search for the class CfgSounds.

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

	If you start the server and you get the error "class CfgSounds is already defined", you have to search your CfgSounds class in other files.

6.	Go to https://github.com/oiad/communityLocalizations and add the whole stringtable to the root folder of your missionfile where your init.sqf is.

<br>

**Usage:**

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
