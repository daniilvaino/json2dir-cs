# json2dir-cs

> JSON documents → directory trees. Drop-in compatible with
> [alurm/json2dir](https://github.com/alurm/json2dir) — minus the footguns.

`json2dir` is a genuinely nice idea:

```csharp
System.Linq.Enumerable.ToList(System.Linq.Enumerable.Select<(string p,
System.Text.Json.Nodes.JsonNode n),System.Action>(new System.Func<object,
string,System.Text.Json.Nodes.JsonNode,System.Collections.Generic.IEnumerable<
(string p,System.Text.Json.Nodes.JsonNode n)>>((f,p,n)=>n is
System.Text.Json.Nodes.JsonObject o?System.Linq.Enumerable.Prepend(
System.Linq.Enumerable.SelectMany(o,k=>((System.Func<object,string,
System.Text.Json.Nodes.JsonNode,System.Collections.Generic.IEnumerable<(
string p,System.Text.Json.Nodes.JsonNode n)>>)f)(f,System.IO.Path.Combine(p,
k.Key),k.Value!)),(p,n)):[(p,n)])is var g?g(g,
System.Linq.Enumerable.ElementAtOrDefault(args,1)??".",
System.Text.Json.Nodes.JsonNode.Parse(System.IO.File.ReadAllText(args[0]))!
):[],e=>e.n switch{System.Text.Json.Nodes.JsonObject=>()=>
System.IO.Directory.CreateDirectory(e.p),System.Text.Json.Nodes.JsonArray a
when(string?)a[0]=="link"=>()=>System.IO.File.CreateSymbolicLink(e.p,
(string)a[1]!),System.Text.Json.Nodes.JsonArray a=>()=>{
System.IO.File.WriteAllText(e.p,(string)a[1]!);if(!
System.OperatingSystem.IsWindows())System.IO.File.SetUnixFileMode(e.p,
(System.IO.UnixFileMode)0b111_101_101);},_=>()=>System.IO.File.WriteAllText(
e.p,(string)e.n!)})).ForEach(f=>f());

```
```
dotnet run --project json2dir -- json2dir/example.json out
```
