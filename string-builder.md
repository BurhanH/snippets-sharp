# String Builder

```csharp
using System;
using System.Security.Cryptography;
using System.Text;
using BenchmarkDotNet.Attributes;
using BenchmarkDotNet.Running;

namespace MyBenchmarks
{
    public class StringPerformance
    {
        private string[] arrOfStr;
        private byte[] data;

        [Params(1000, 10000)] public int N;

        [GlobalSetup]
        public void Setup()
        {
            arrOfStr = new string[N];
            data = new byte[N];
            new Random(42).NextBytes(data);
            arrOfStr = data.Select(x => x.ToString()).ToArray();
        }
        
        [Benchmark]
        public string StrConcat()
        {
            string result = string.Empty;
            foreach (var str in arrOfStr)
            {
                result += str;
            }
            return result;
        }

        [Benchmark]
        public string StrBuilder()
        {
            StringBuilder builder = new StringBuilder();
            foreach (var str in arrOfStr)
            {
                builder.Append(str);
            }
            return builder.ToString();
        }
    }

    public class Program
    {
        public static void Main(string[] args)
        {
            var summary = BenchmarkRunner.Run<StringPerformance>();
        }
    }
}
```

Result:

```console
| Method     | N     | Mean         | Error      | StdDev     |
|----------- |------ |-------------:|-----------:|-----------:|
| StrConcat  | 1000  |   121.961 us |  0.6417 us |  0.5689 us |
| StrBuilder | 1000  |     2.599 us |  0.0177 us |  0.0166 us |
| StrConcat  | 10000 | 9,691.438 us | 63.9225 us | 56.6656 us |
| StrBuilder | 10000 |    36.846 us |  0.7274 us |  0.6804 us |

// * Hints *
Outliers
  StringPerformance.StrConcat: Default -> 1 outlier  was  removed (123.96 us)
  StringPerformance.StrConcat: Default -> 1 outlier  was  removed (10.13 ms)

// * Legends *
  N      : Value of the 'N' parameter
  Mean   : Arithmetic mean of all measurements
  Error  : Half of 99.9% confidence interval
  StdDev : Standard deviation of all measurements
  1 us   : 1 Microsecond (0.000001 sec)
```
