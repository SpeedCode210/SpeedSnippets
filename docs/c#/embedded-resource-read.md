# Lecture d'une EmbeddedResource

Voici une fonction permettant de lire simplement un fichier texte en EmbeddedResource en C#

## Fonction

```cs
using System.Reflection;

...

static string ReadEmbeddedResource(string res){
    var asm = Assembly.GetExecutingAssembly();
    using var stream = asm.GetManifestResourceStream(asm.GetName().Name+"."+res.Replace('/', '.'))!;
    using var reader = new StreamReader(stream);
    string result = reader.ReadToEnd();
    return result;
}
```

## Exemple

Sur un projet ayant la structure suivante avec File1.txt et File2.txt en EmbeddedResource :

```
TestProject.csproj
 |
 |- File1.txt
 |
 |- Folder1
 |  |
 |  |- File2.txt
 |
 |- Program.cs
```

Pour accéder au contenu des deux fichiers, rien de plus simple :

```cs
string file1 = ReadEmbeddedResource("File1.txt");
string file2 = ReadEmbeddedResource("Folder1/File2.txt");
```