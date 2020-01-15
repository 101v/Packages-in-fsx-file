## Using nuget packages in fsx file.

Recently, I started tinkering with F#. One of the cool thing about F# is REPL ([Read-eval-print loop](https://en.wikipedia.org/wiki/Read%E2%80%93eval%E2%80%93print_loop)). Our tool for the REPL is F# Interactive (FSI) window. We can use it two ways: we can directly type code in FSI window, or write code in an FSX (.fsx is the file extension) script file, and select the pieces of the code we want to execute. FSI window is very primitive whereas FSX is much better to use along with IntelliSense.

To write code in FSX script file, I use VSCode. VSCode with [Ionide-fsharp](https://marketplace.visualstudio.com/items?itemName=Ionide.Ionide-fsharp) is an excellent combo while playing/working with F#. However, it requires quite a bit of setup before get going. 

Following is my experience of how I went about using nuget packages in VSCode

### Install [Paket] (https://fsprojects.github.io/Paket/) globally

```
dotnet install paket -g
```

### Script folder and initial paket setup
Create a folder and intilise it with paket 
```
> mkdir fsharp_practice
> cd fsharp_practice
> paket init
```
The `paket init` command creates a paket-files folder and paket.dependecies [file](https://fsprojects.github.io/Paket/dependencies-file.html) 

In the paket.dependencies file, the default `storage` setting is by set to `none`. What it means is that by default it does not extract packages into the "packages" folder but use a globally shared directory. Update this setting as shown below
```
storage: packages
```

### Add one or more packages
Now we are ready to add required packages using following command
```
paket add FsCheck
```
This command adds `nuget FsCheck` in the paket.dependencies file, generates paket.lock, paket-files\paket.restore.cached file and packages directory with the FsCheck package content.

### Script file
1. User relative path __SOURCE_DIRECTORY__ (**not quotation around this variable**)
2. Use #I to defien assembly search path
3. Use #r to reference assembly
4. Load using open
