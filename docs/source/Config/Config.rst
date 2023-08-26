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

.. code-block::
    :caption: A full CfgPatches layout, feel free to copy this and use it yourself.
    
    class CfgPatches
    {
        class TestAddon
        {
            name = "My Addon";
            author = "Me";
            url = "https://community.bistudio.com/wiki/CfgPatches";

            requiredVersion = 1.60; // Minimum compatible version. When the game's version is lower, pop-up warning will appear when launching the game.
            // Required addons is used for setting load order. (CfgPatches classname NOT PBO filename!)
            // When any of the addons are missing, a pop-up warning will appear when launching the game.
            requiredAddons[] = { "A3_Functions_F" };
            
            units[] = {}; // List of objects (CfgVehicles classes) contained in the addon. Important also for Zeus content (units and groups) unlocking.
            
            weapons[] = {}; // List of weapons (CfgWeapons classes) contained in the addon.

            // Optional. If this is 1, if any of requiredAddons[] entry is missing in your game the entire config will be ignored and return no error (but in rpt) so useful to make a compat Mod.
            skipWhenMissingDependencies = 1;
        };
    };
.. code-block::
    
    testcode
    this is testing Code.cpp

.. note::
    Remember to take breaks every now and then, C++ and Arma modding can be annoying and confusing :).
