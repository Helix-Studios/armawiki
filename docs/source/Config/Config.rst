Config
=====

.. _Config:

Pre-requisites
------------
+ Basic understanding of code structure.
+ A IDE of your choice, most people use VS/VSC (Visual Studio Code).
+ Arma 3 Tools (So we can get P-Drive setup)
+ Arma 3 Samples (OPTIONAL but handy) 



The Basics
----------------
So what is Arma written in? Fundamentally Arma is written in 2 languages that modders care about; C++ and SQL/SQS (we'll touch on this later). For now this guide will focus on the former (C++).
But why?
Well, C++ is a lovely object-oriented programming language which makes it very clear and easy to understand once you get your head around it.
If you are struggling to figure out C++ i'd recommend looking at youtube or `W3Schools <https://www.w3schools.com/cpp/cpp_intro.asp>`_

In every single mod in Arma 3, there is a config.cpp file. This defines all the classes & functions inside of the mod.

They will always use a variation of the following structure:
-CfgPatches
-CfgWeapons
-CfgVehicles
-CfgAmmo
-CfgMagazines
& much much more

Fortunately, C++ is incredibly modular and makes adding all of this together very easy!


CfgPatches
----------------
The most important part of ANY config. This defines all the basic mod information such as mod name (or part of a mod name), the author, requiredaddons as well as the lists of units and weapons that are contained within your config.
Remember this is case sensitive, so if you are typing this out, pay attention.

.. code-block::
    :caption: A full CfgPatches layout, feel free to copy this and use it yourself.
    
    class CfgPatches
    {
        class TestAddon
        {
            name = "My Addon";
            author = "Me";
            url = "https://community.bistudio.com/wiki/CfgPatches";

            requiredVersion = 0.1; // Minimum compatible version. When the game's version is lower, pop-up warning will appear when launching the game.
            // Required addons is used for setting load order. (CfgPatches classname NOT PBO filename!)
            // When any of the addons are missing, a pop-up warning will appear when launching the game.
            requiredAddons[] = { "A3_Functions_F" };
            
            units[] = {}; // List of objects (CfgVehicles classes) contained in the addon. Important also for Zeus content (units and groups) unlocking.
            
            weapons[] = {}; // List of weapons (CfgWeapons classes) contained in the addon.

            // Optional. If this is 1, if any of requiredAddons[] entry is missing in your game the entire config will be ignored and return no error (but in rpt) so useful to make a compat Mod.
            skipWhenMissingDependencies = 1;
        };
    };

I will now go from top to bottom to really make sure you understand every line.

``TestAddon``: Should be defined as whatever addon is inside of it. Usually modders will come up with their own naming conventions. A simple one to follow is just Modname_itemnames E.G. ``AS_Helmets`` AS being an abbreviation for a mod name, helmets being what is inside the config.
``name``: This is the display name of the mod. E.G. ACE.
``author``: Who made the addon.
``url``: If you want to link a modpage, wiki or discord link this would be a place to do so, otherwise you can usually ommit url from your cfgpatches.
``requiredVersion[]``: This sets the minimum compatible version of Arma for the mod.
``requiredAddons[]``: This lays out the addon loading order (as well as addons required) by this mod, say for example you have a auxiliary mod utilising assets from Base Arma, RHSUSAF and CUP, you would put those addon classnames here (yes the very same TestAddon classname).
``units[]``: This lists every object contained inside of the class CfgVehicles (we'll talk about this later).
``weapons[]``: This lists every object contained inside of the class CfgWeapons (again cover this later).
``skipWhenMissingDependencies``: OPTIONAL, when set to 1 this will ignore requiredAddons[], in practice it will stop popups when you load into the main menu. By default it is set to 0.

You've also probably noticed I copied over square brackets ``[]`` from the CfgPatches, This means the class function is an array and will contain multiple variables/inputs inside of the function.

.. code-block::
    :caption: A C++ array

    requiredAddons[] = {
    		"A3_Weapons_F",
			"A3_characters_f_bootcamp",
			"A3_Characters_F",
    };

That covers everything to do with CfgPatches, if you have anything questions feel free to ask Bohemia Interactive.

.. note::
    Remember to take breaks every now and then, Arma modding can be annoying and confusing :). Especially when it doesn't work
