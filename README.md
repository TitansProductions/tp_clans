# tp_clans

## __Tutorials & Tips:__

### How to create a blackmarket store through **tp_stores** (example):

1. When creating a blackmarket schedule, there is an option called `StoreName`, this is the name of the store that must open through **tp_stores**, which means that if our input is `BLACKMARKET`, the store on `Config.Stores` must also be named that way.

1. On `Config.Stores` add a store which is **IsCustom = true**, like so:

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
