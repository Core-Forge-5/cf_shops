# cf_shops

A thin wrapper around `ox_inventory` that lets you register static shops from a config file. Just locations + item types + a price list.

---

## How it works

You define **item types** (e.g. `Hardware`, `Liquor`, `Ammo`) in `config/shared.lua` — just a table of `{ name, price, currency }` entries.  
Then in `config/shared.lua` you create shop instances that **reference one or more of those types** and give them one or more `locations` (vector3).  
Then you can enjoy the shops

---

## Configuration

### config/shared.lua

A flat list of **item types**. Each key is a type name, each value is a list of items:

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

### config/shared.lua

A list of shop instances:

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

Each `types` entry appends items from the matching key in `shared.lua`. A shop can have one or many locations — they all open the same inventory.

---

## Adding a new shop type

1. Add a new table in `config/shared.lua`:
   ```lua
   Pharmacy = {
       { name = 'bandage',   price = 50, currency = 'money' },
       { name = 'painkiller', price = 30, currency = 'money' },
   },
   ```
2. Add a shop entry in `config/shared.lua` that references it:
   ```lua
   {
       name = 'Pharmacy Plus',
       locations = { vec3(-431.83, -326.67, 34.91) },
       types = { 'Pharmacy' },
   },
   ```

---

## Dependencies

- `ox_lib`
- `ox_inventory` (runtime `RegisterShop` export)
- `ox_target` (client zones)
