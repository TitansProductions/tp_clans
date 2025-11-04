
# __Tutorials & Tips:__

### How to create a blackmarket store through **tp_stores** (example):

1. When creating a blackmarket schedule, there is an option called `StoreName`, this is the name of the store that must open through **tp_stores**, which means that if our input is `BLACKMARKET`, the store on `Config.Stores` must also be named that way.

__Example:__

```lua
-- The location - coords for the merchant to spawn.
RandomCoords = {
    { Coords = { x = -3955.85, y = -2133.93, z = -5.578, h = 97.171997 }, StoreName = 'BLACKMARKET'}, -- <---------------
},
```

2. On `Config.Stores` add a store which is **IsCustom = true**, like so:

```lua
    ['BLACKMARKET'] = {

        StoreName = "BLACKMARKET",

        -- THE SPECIFIED STORE IS AN EXAMPLE FOR CUSTOM STORES, A CUSTOM STORE IS FOR GETTING OPENED THROUGH AN EXPORT OR EVENT.
        -- IT DOES NOT HAVE BLIPS, COORDS, DISTANCE TO OPEN, NPC OR ANYTHING, ONLY PRODUCTS.
        IsCustom  = true, -- <---------

        Categories = { 
            { category = "tools",  types = {"buy" } },
            { category = "jewerly",  types = {"sell" } },
        }, 

        StoreProductsPackage = "blackmarket",
    },
```

3. When creating the store, now we have to create the store products to be sold, bought or be exchanged on `Config.StoreProductPackages ` (**tp_Stores**)

```lua
Config.StoreProductPackages = {

    ['blackmarket'] = {

        ['buy'] = {
            { label = "Shovel",         item = "shovel",       currency = "dollars",   price = 17,   limit = 5,  dynamic = false, category = "tools" },
            { label = "Golden Pan",     item = "goldpan",      currency = "dollars",   price = 5,    limit = 5,  dynamic = false, category = "tools" },
            { label = "Miner Hat",      item = "miner_hat",    currency = "dollars",   price = 1,    limit = 10, dynamic = false, category = "tools" },
            { label = "Lockpick",       item = "lockpick",     currency = "dollars",   price = 1,    limit = 10, dynamic = false, category = "tools" },
            { label = "Hearing Tool",   item = "hearingtool",  currency = "dollars",   price = 1,    limit = 10, dynamic = false, category = "tools" },

        },

        ['sell'] = {

            { label = "Gold Tooth",    item = "goldtooth",     currency = "dollars",   price = 1,  canGiveItems = false, givenItem = {},  givenAmount = {}, givenDisplay = {},  category = "jewerly" },
            { label = "Gold Ring",     item = "goldring",      currency = "dollars",   price = 2,  canGiveItems = false, givenItem = {},  givenAmount = {}, givenDisplay = {},  category = "jewerly" },
            { label = "Gold Bracelet", item = "goldbracelet",  currency = "dollars",   price = 3,  canGiveItems = false, givenItem = {},  givenAmount = {}, givenDisplay = {},  category = "jewerly" },
            { label = "Gold Necklace", item = "goldnecklace",  currency = "dollars",   price = 3,  canGiveItems = false, givenItem = {},  givenAmount = {}, givenDisplay = {},  category = "jewerly" },
            { label = "Gold Bar",      item = "goldbar",       currency = "dollars",   price = 10, canGiveItems = false, givenItem = {},  givenAmount = {}, givenDisplay = {},  category = "jewerly" },

        },

    },
}
```

