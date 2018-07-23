# Over9000 Gamling Script

Over9000 Gambling Script by A Man
If you use it please give credit
Free to use in Salivals modPack

Works only with ZSC: https://github.com/oiad/ZSC

Installation:

1.	Put the scripts folder from github in your missionfile root folder where your init.sqf is.
2.	Open your fn_selfactions.sqf and search for: //Towing with tow truck

	Add this code lines above:
	```
	_isGamble = _cursorTarget isKindOf "Hooker4"; // Define here the trader or the building where you get the gambling dialog
	if (_isGamble && _canDo) then {
		_hasCards = "ItemCards" in magazines player;
		if (_hasCards) then {
			if (s_player_gamblefree < 0) then {
				s_player_gamblefree = player addAction [localize "STR_GAMBLE_PriceFree", "scripts\gamble\gamble.sqf",0, 1, false, true];
			};
		};	
		if (s_player_gamble1 < 0) then {
			s_player_gamble1 = player addAction [localize "STR_GAMBLE_Price1x", "scripts\gamble\gamble.sqf",1000, 1, false, true];
		};
		if (s_player_gamble2 < 0) then {
			s_player_gamble2 = player addAction [localize "STR_GAMBLE_Price2x", "scripts\gamble\gamble.sqf",2000, 1, false, true];
		};
		if (s_player_gamble3 < 0) then {
			s_player_gamble3 = player addAction [localize "STR_GAMBLE_Price3x", "scripts\gamble\gamble.sqf",3000, 1, false, true];
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
	```
		player removeAction s_player_fuelauto2;
		s_player_fuelauto2 = -1;
		player removeAction s_player_manageDoor;
		s_player_manageDoor = -1;	
	```	
	And add behind:
	```
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
	```
	s_player_manageDoor = -1;
	```
	And add behind:
	```
	s_player_gamblefree = -1;
	s_player_gamble1 = -1;
	s_player_gamble2 = -1;
	s_player_gamble3 = -1;
	```
5.	Open your description.ext and search for class CfgSounds

	Add inside class CfgSounds 
	```
	class tada
	{
		name="tada";
		sound[]={\scripts\gamble\tada.ogg,0.9,1};
		titles[] = {};
	};
	```
	If you have not a class CfgSounds add:
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
	If you get on server start the error class CfgSounds is alreday defined, search your files for class CfgSounds.
	
6.	Go to https://github.com/oiad/communityLocalizations and add the whole stringtable to the root folder of your missionfile where your init.sqf is.

Usage:

Define here in the fn_selfactions the trader or the building where you get the gambling dialog.
	
	_isGamble = _cursorTarget isKindOf "Hooker4";
	
If you have Cards you get a try gambling try.

You can gamble for 1000, 2000 and 3000 Coins and get the price 1x, 2x and 3x. The script is not optimized but it works out of the box and can be used with overpoch.




	
