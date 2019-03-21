# MonoGame Content Reference T4 Templete
This T4 templete will generate a public static class called ContentRefrence in your project with const string fields whos values are the path string needed to load your content using the ContentManager object.

For Example, if your Content hierarchy is as follows
|- Content
  |- Textures
    |- player_01.png
    |- player_02.png
  |- Audio
    |- SFX
      |- menu click.ogg
      |- ding.ogg

The generated ContentReference.cs file would be as follows  

```csharp
public static class ContentReference
{
    public static class Textures
    {
        public const string Player_01 = @"textures/player_01";
        public const string Player_02 = @"textures/player_02";
    }

    public static class Audio
    {
        public static class SFX
        {
            public const string Menu_click = @"audio/sfx/menu click";
            public const string Ding = @"audio/sfx/ding";
        }
    }
}
```

# Install
1. Clone or Download the repo
2. Add teh ContentReference.tt file to your project in the Content directory

# Configuration
After adding the ContentReference.tt file to your project, there are a few configurations options you can use to customize the output of the generated class file.  To adjust these options, open the ContentRefrence.tt file. Find the section called **Generator Settings** and adjust the values of the settings.  The table below explains the different options and their values

| Option | Description |
|---|---|
INCLUDE_NAMESPACE |  <p>Set this to `true` or `false`.  If `true`, then the generated class file will be encapsulated by a namespace statement</p> |
NAMESPACE | If the `INCLUDE_NAMESPACE` option is set to `true`, then this determines the name of the namespace to use
CLASS_STYLE | Determines how class names are generated. Available values are `ClassStyle.FirstCharUpper` and `ClassStyle.MatchName`
  
  `ClassStyle.FirstCharUpper` will force the name of the class generad to have the first character in upper case and the reset in lower case  
  
  `ClassStyle.MatchName` will force the name of the class to be the same as the name of the directory it is based on |
FILED_STYLE | Determins how filed names are generated.  Available values are `FieldStyle.Proper` and `FieldStyle.MatchName`  
  
  `FieldStyle.Proper` will use camel casing for the field name  
  `FieldStyle.MatchName` will force the name of the field to be the same as the name of the file it is based on |
SPACE_STYLE | Determines how spaces in class and field names are handled.  Available values are `SpaceStyle.Remove` and `SpaceStyle.Underscore`  
  
  `SpaceStyle.Remove` will just remove all spaces  
  `SpaceStyle.Underscore` will replace all spaces with underscores |
RESERVED_STYLE | Determins how class and field names are handles if they match a reserved C# keyword.  Availalbe values are `ReservedStyle.AtSymbol` and `ReservedStyle.Underscore`  
  
  `ReservedStyle.AtSymbol` will place an @ symbol at the beginning of the name.  
  `ReservedStyle.Underscore` will place an _ at the beginning of the name. |
CONTENT_DIR | This is the directory where the content pipelien tool outputs the .xnb files it builds relative to the Content directory (e.g. For MonoGame Cross Platform Desktop Project the value is `@"bin\DesktopGL"`) |

# Usage
This template will auto generate a class .cs file called ContentReference.cs that you can use in your project to load content in as follows (example below uses the content hierarchy described at the top of the readme)

```csharp
var texture = Content.Load<Texture2D>(ContentReference.Textures.Player_01);
```