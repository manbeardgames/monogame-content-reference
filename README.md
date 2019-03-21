# MonoGame Content Reference T4 Templete
This T4 templete will generate a public static class called ContentRefrence in your project with const string fields whos values are the path string needed to load your content using the ContentManager object.

For Example, if your Content hierarchy is as follows
```
|-  Content
    |-  Textures
        |-  player_01.png
        |-  player_02.png
    |-  Audio
        |-  SFX
            |-  menu click.ogg
            |-  ding.ogg
```

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
2. Add the ContentReference.tt file to your project in the Content directory

# Configuration
After adding the ContentReference.tt file to your project, there are a few configurations options you can use to customize the output of the generated class file.  To adjust these options, open the ContentRefrence.tt file. Find the section called **Generator Settings** and adjust the values of the settings.  

The following are the default values if you need them for refrence.  

```
// -------------------------------------------------------------
//	Generator Settings
//	Adjust the settings below. Explinations are provided
// -------------------------------------------------------------

//	Set this to true if you want the generated class to be 
//	encapsulated by a namespace
INCLUDE_NAMESPACE = false;

//	If you set the above to true, enter the name of the namespace
//	you wish to use. 
NAMESPACE = "";

//	This determines how Class Names are generated
//	CLASS_STYLE.FirstCharUpper = Only the first character of the class name is upper case
//	CLASS_STYLE.MatchName = Name is the same casing as the directory name its based on
CLASS_STYLE = ClassStyle.FirstCharUpper;

//	This determines how Field Names are generated
//	FIELD_STYLE.Proper = Name is camel case
//	FIELD_STYLE.MatchName = Name is the same casing as the directory/filename
FIELD_STYLE = FieldStyle.MatchName;

//	This determines how to handle spaces in file names
//	SpaceStyle.Remove = Removes all spaces
//	SpaceStyle.Underscore = Replaces all spaces with _ 
SPACE_STYLE = SpaceStyle.Remove;


//	This determines how to handle file names that match a 
//	reseved C# keyword
//	ReservedStyle.AtSymbol = Places an @ symbole in front of the generated name
//	ReservedStyle.Underscore = Places an _ in front of the generated name
RESERVED_STYLE = ReservedStyle.AtSymbol;


//	This is the directory where the content tool outputs the .xnb files it builds
//	For MonoGame Cross Platform Desktop Project it's "bin\DesktopGl"
CONTENT_DIR = @"bin\DesktopGL";
```

**Be sure to include the semi-colon (;) at the end of each line if you adjust the values.**  

The table below explains the different options and their values

| Option | Description |
|---|---|
| INCLUDE_NAMESPACE |  <p>Set this to `true` or `false`.  If `true`, then the generated class file will be encapsulated by a namespace statement</p> |
| NAMESPACE | <p>If the `INCLUDE_NAMESPACE` option is set to `true`, then this determines the name of the namespace to use</p> |
| CLASS_STYLE | <p>Determines how class names are generated. Available values are `ClassStyle.FirstCharUpper` and `ClassStyle.MatchName`</p><p>`ClassStyle.FirstCharUpper` will force the name of the class generad to have the first character in upper case and the reset in lower case.</p><p> `ClassStyle.MatchName` will force the name of the class to be the same as the name of the directory it is based on</p> |
| FILED_STYLE | <p>Determins how filed names are generated.  Available values are `FieldStyle.Proper` and `FieldStyle.MatchName`.</p><p>`FieldStyle.Proper` will use camel casing for the field name.</p><p>`FieldStyle.MatchName` will force the name of the field to be the same as the name of the file it is based on</p> |
| SPACE_STYLE | <p>Determines how spaces in class and field names are handled.  Available values are `SpaceStyle.Remove` and `SpaceStyle.Underscore`.</p><p>`SpaceStyle.Remove` will just remove all spaces.</p><p>`SpaceStyle.Underscore` will replace all spaces with underscores</P> |
| RESERVED_STYLE | <p>Determins how class and field names are handles if they match a reserved C# keyword.  Availalbe values are `ReservedStyle.AtSymbol` and `ReservedStyle.Underscore`.</p><p>`ReservedStyle.AtSymbol` will place an @ symbol at the beginning of the name.</p><p>`ReservedStyle.Underscore` will place an _ at the beginning of the name.</p> |
| CONTENT_DIR | <p>This is the directory where the content pipelien tool outputs the .xnb files it builds relative to the Content directory (e.g. For MonoGame Cross Platform Desktop Project the value is `@"bin\DesktopGL"`)</p> |




# Usage
This template will auto generate a class .cs file called ContentReference.cs that you can use in your project to load content in as follows (example below uses the content hierarchy described at the top of the readme)

```csharp
var texture = Content.Load<Texture2D>(ContentReference.Textures.Player_01);
```
