# cf_shops

A modern shop UI for FiveM built around `ox_inventory`.

`cf_shops` gives your static shops a cleaner NUI without changing the way you configure them. Shops, locations, item groups, prices, and currencies stay in your config while the UI handles the actual browsing and checkout experience.

Built with React and Tailwind CSS, with `ox_inventory` item images pulled directly into the shop.

## Demo

[Watch the cf_shops demo](docs/showcase.mkv)

## Features

* Modern NUI shop interface
* Real-time item search
* Item categories
* Multi-currency support
* Cart system
* `ox_inventory` item images
* Multiple shop locations using one configuration
* Reusable item types
* Config-driven shops
* Lightweight client/server setup
* Built for `ox_lib` / `ox_inventory`

The goal is pretty simple: **configure the shop once and let the UI do the rest.**

## Configuration

Shops are configured in `config/shared.lua`.

### Item types

Create reusable groups of items:

```lua
return {

    Hardware = {
        { name = 'lockpick',       price = 50, currency = 'money' },
        { name = 'screwdriverset', price = 50, currency = 'money' },
    },

    Liquor = {
        { name = 'beer',    price = 15, currency = 'money' },
        { name = 'whiskey', price = 25, currency = 'money' },
    },

}
```

You can then reuse these groups across multiple shops instead of maintaining the same item list over and over.

### Shops

Create your shop locations and attach the item types you want:

```lua
return {

    debug = true,

    shops = {

        {
            name = '24/7 Supermarket',

            locations = {
                vec3(25.7, -1347.3, 29.49),
                vec3(373.87, 325.56, 103.57),
            },

            types = { 'Hardware', 'Liquor' },
        },

        {
            name = 'Ammu-Nation',

            locations = {
                vec3(252.63, -50.72, 69.94),
                vec3(-662.33, -935.58, 21.83),
            },

            types = { 'Ammo', 'Hardware' },
        },

    },

}
```

Every location using the same shop entry opens the same inventory.

## Adding another shop

Add an item type:

```lua
Pharmacy = {
    { name = 'bandage',    price = 50, currency = 'money' },
    { name = 'painkiller', price = 30, currency = 'money' },
},
```

Then reference it from a shop:

```lua
{
    name = 'Pharmacy Plus',

    locations = {
        vec3(-431.83, -326.67, 34.91),
    },

    types = { 'Pharmacy' },
},
```

That's it.

## Why use cf_shops?

If you're already using `ox_inventory`, you don't need to rebuild your shop system around another inventory framework just to get a better storefront.

`cf_shops` keeps the backend simple and puts the work where players actually see it — the shop interface.

It's also designed around reusable configuration, so adding another 24/7, hardware store, pharmacy, or other shop doesn't mean copying a giant item list into every location.

## Dependencies

* `ox_lib`
* `ox_inventory`
* `ox_target`

`ox_inventory` is used for item data/images and shop registration.

`ox_target` handles the shop interaction zones.

## Installation

1. Download the resource.
2. Place `cf_shops` in your resources folder.
3. Ensure the required dependencies are started first.
4. Configure your shops in `config/shared.lua`.
5. Add the resource to your server configuration.

Example:

```cfg
ensure ox_lib
ensure ox_inventory
ensure ox_target
ensure cf_shops
```

## Get cf_shops

Want the shop UI shown in the demo on your server?

**[Purchase cf_shops on Tebex](https://core-forge.tebex.io/)**

The purchase includes the resource.

---

Made for FiveM servers using the `ox_*` ecosystem.
