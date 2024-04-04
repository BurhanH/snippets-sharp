# CollectionsMarshal Class

https://learn.microsoft.com/en-us/dotnet/api/system.runtime.interopservices.collectionsmarshal?view=net-8.0


```csharp
using System.Runtime.InteropServices;

List<int> list = [1, 2, 3, 4, 5]; 
var span = CollectionsMarshal.AsSpan(list); 
list.AddRange(Enumerable.Range(1, 10)); 
 
span[1] = -1; 
 
Console.WriteLine(span[1]); 
Console.WriteLine(list[1]);
```
