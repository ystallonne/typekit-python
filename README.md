typekit-python
==============

This is a Python module that implements the Typekit developers API. It allows you to create, retrieve, delete, update, and publish Typekit kits in Python. You can also get information about a font family and the possible variations of a given font family. It now supports adding and removing font from a kit.

Read the source code if the documentation below isn't enough. It has okay high-level comments for each method.

## Usage

Install the library using pip:

```
pip install typekit
```

Initialize the client with your developer API token. You can get your API token [here](https://typekit.com/account/tokens). All method calls return the JSON representation of the return from calling the Typekit API.

```
from typekit import Typekit

tk = Typekit(api_token='<API token>')
```
### List kits

To list all your kits, use the following command:

```
tk.list_kits()
```

### Get kit

To get information about a specific kit, input the kit id as the argument:

```
tk.get_kit(kit_id='<kit_id>')
```

### Create kit

To create a new kit, use the method `create_kit(name, domains, families=None, badge=False)`. `Name` and `domains` fields are required, but the `families` and `badge` fields are not.

The arguments are in the following format:
- **name**: string
- **domains**: string of format 'localhost, http://domain.com, 127.0.0.1' or a Python list of strings of format ['localhost', 'http://domain.com', '127.0.0.1']
- **families**: list of dictionaries with the following key : values
  - 'id' : font family id (string)
  - (optional) 'variations' : comma separated variations (string).

An example of the families format is: `families = [{'id': 'ftnk', 'variations': 'n3,n4'}, {'id': 'pcpv', 'variations': 'n4'}]` in which case we would create a kit with the font families Futura-PT and Droid Sans with font variations normal 3 (font-weight:300 and not italicized or strong), normal 4 and normal 4, respectively.

Example usage:

```
name = 'example typekit kit'
domains = ['localhost', 'http://domain.com']
families = [{'id': 'ftnk', 'variations': 'n3,n4'}, {'id': 'pcpv', 'variations': 'n4'}]

tk.create_kit(name, domains, families)
```

### Update kit

To create a new kit, use the method `update_kit(kit_id, name=None, domains=None, families=None, badge=False)`. The only required field is `kit_id`. `Name`, `domains`, `families` and `badge` fields are not required.

Field formats are the same as `create_kit`.

Example usage:

```
tk.update_kit(kit_id='<kit_id>', name='new name', badge='true')
```

### Remove kit

To remove a kit, use the method `remove_kit(kit_id)`. The `kit_id` field is required.

```
tk.remove_kit(kit_id='<kit_id>')
```

### Publish kit

To publish a kit, use the method `publish_kit(kit_id)`. The `kit_id` field is required.
```
tk.publish_kit(kit_id='<kit_id>')
```

### Get font family

To retrieve information regarding a given font family, use the method `get_font_family(font)`. The argument `font` is a string and can be a Typekit font id or a slug of the font as named in Typekit. The method does not slugify the input, so make sure to slugify it before entering the argument.

```
tk.get_font_family('<font_id>')
```

### Get font variations

To retrieve all possible variations of a given font, use the method `get_font_variations(font)`. The argument is the same as for `get_font_family(font)`. This method returns a Python list of all possible variations of the font.

```
variations = tk.get_font_variations('futura-pt') # using font slug

or

variations = tk.get_font_variations('ftnk') # using font id

OUTPUT:
[u'n3', u'i3', u'n4', u'i4', u'n5', u'i5', u'n7', u'i7', u'n8', u'i8']

```

### Add font to kit

To add font to kit, use the method `kit_add_font(kit_id, font, variations=None)`. Arguments for this method is the same format as the ones above, BUT variations should be in list. Returns nothing.

```
tk.kit_add_font('kit_id', 'futura-pt', [n3,n5,n7])
```

### Remove font from kit

To add font to kit, use the method `kit_remove_font(kit_id, font)`. Arguments for this method is the same format as the ones above, BUT variations should be in list. Returns nothing.

```
tk.kit_remove_font('kit_id', 'futura-pt')
```

### Other methods

`get_kit_vals(kit_id)` - Retrieves kit vals in a list of format: [name, domains, families, badge]

`get_kit_fonts(kit_id)` - Retrieves a list of font ids in a given kit

`kit_contains_font(kit_id, font)` - Checks to see if a font exists in a kit.



## Licence

MIT Licence





