# netcore-csv

[![NuGet Badge](https://buildstats.info/nuget/netcore-csv)](https://www.nuget.org/packages/netcore-csv/)
[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2Fdevel0%2Fnetcore-csv.svg?type=shield)](https://app.fossa.io/projects/git%2Bgithub.com%2Fdevel0%2Fnetcore-csv?ref=badge_shield)

.NET core CSV

- [API Documentation](#api-documentation)
- [Quickstart](#quickstart)
  * [execution](#execution)
- [How this project was built](#how-this-project-was-built)

<hr/>

## API Documentation

- [CSVReader](doc/api/CSV/CsvReader-1.md)
- [CSVWriter](doc/api/CSV/CsvWriter-1.md)
- [CsvColumnHeaderAttribute](doc/api/CSV/CsvColumnHeaderAttribute.md)
- [CsvColumnOrderAttribute](doc/api/CSV/CsvColumnOrderAttribute.md)
- [Extensions](doc/api/Extensions.md)

## Quickstart

- create console project

```sh
dotnet new console -n example
cd example
```

- add reference to netcore-sci ( check latest version [here](https://www.nuget.org/packages/netcore-sci/) )

```sh
dotnet add package netcore-csv --version 0.0.2
```

if prefer to link source code directly to stepin with debugger add project reference instead

```sh
dotnet add reference path_to/netcore-csv/netcore-csv.csproj
```

for some useful sci extensions include [netcore-sci](https://github.com/devel0/netcore-sci#quickstart)

```
dotnet add package netcore-sci --version 1.0.27
```

- setup example code

```csharp
using System;
using System.Linq;
using SearchAThing;
using System.Diagnostics;
using SearchAThing.CSV;

namespace test
{

    public class MyData
    {
        public int i10 { get; set; }
        public int i20 { get; set; }
        [CsvHeader("SomeStringCol")]
        public string s1 { get; set; }
        [CsvHeader("FirstDblCol")]
        public double v1 { get; set; }
        public double v2 { get; set; }
        public double v3 { get; set; }
        public double v4 { get; set; }
        public double v5 { get; set; }
        public double v6 { get; set; }
        public double v7 { get; set; }
        public double v8 { get; set; }
        public double v9 { get; set; }
        public double v10 { get; set; }
        public double v11 { get; set; }
        public double v12 { get; set; }
        public double v13 { get; set; }
        public double v14 { get; set; }
        public double v15 { get; set; }
        public double v16 { get; set; }
        public double v17 { get; set; }
        public double v18 { get; set; }
        public double v19 { get; set; }
        public double v20 { get; set; }
        [CsvColumnOrder(0)]
        public double firstcol { get; set; }
    }

    class Program
    {
        static void Main(string[] args)
        {
            const int CNT = 500000;
            {
                var stopw = new Stopwatch();
                stopw.Start();

                using var csv = new CsvWriter<MyData>("test.csv");

                var rnd = new Random();                

                for (int i = 0; i < CNT; ++i)
                {
                    var d = new MyData
                    {
                        v1 = rnd.NextDouble() * 1e9,
                        v2 = rnd.NextDouble() * 1e9,
                        v3 = rnd.NextDouble() * 1e9,
                        v4 = rnd.NextDouble() * 1e9,
                        v5 = rnd.NextDouble() * 1e9,
                        v6 = rnd.NextDouble() * 1e9,
                        v7 = rnd.NextDouble() * 1e9,
                        v8 = rnd.NextDouble() * 1e9,
                        v9 = rnd.NextDouble() * 1e9,
                        v10 = rnd.NextDouble() * 1e9,
                        v11 = rnd.NextDouble() * 1e9,
                        v12 = rnd.NextDouble() * 1e9,
                        v13 = rnd.NextDouble() * 1e9,
                        v14 = rnd.NextDouble() * 1e9,
                        v15 = rnd.NextDouble() * 1e9,
                        v16 = rnd.NextDouble() * 1e9,
                        v17 = rnd.NextDouble() * 1e9,
                        v18 = rnd.NextDouble() * 1e9,
                        v19 = rnd.NextDouble() * 1e9,
                        v20 = rnd.NextDouble() * 1e9,
                        i10 = rnd.Next(1, 10),
                        i20 = rnd.Next(1, 20),
                        s1 = $"str:[{rnd.Next()}]"
                    };

                    csv.Push(d);
                }

                System.Console.WriteLine($"written [{CNT}] rows in {stopw.Elapsed}");
            }

            {
                var stopw = new Stopwatch();
                stopw.Start();

                using var csv = new CsvReader<MyData>("test.csv");

                csv
                    .GroupBy(w => w.i10)
                    .Select(w => new
                    {
                        i10 = w.Key,
                        i20Min = w.Min(r => r.i20),
                        i20Max = w.Max(r => r.i20),
                        v1Mean = w.Select(w => w.v1).Mean(),
                        v2Mean = w.Select(w => w.v2).Mean(),
                        v3Mean = w.Select(w => w.v3).Mean(),
                        v4Mean = w.Select(w => w.v4).Mean(),
                        v5Mean = w.Select(w => w.v5).Mean(),
                        v6Mean = w.Select(w => w.v6).Mean(),
                        v7Mean = w.Select(w => w.v7).Mean(),
                        v8Mean = w.Select(w => w.v8).Mean(),                        
                        v9Mean = w.Select(w => w.v9).Mean(),                        
                        v10Mean = w.Select(w => w.v10).Mean(),                        
                        v11Mean = w.Select(w => w.v11).Mean(),                        
                        v12Mean = w.Select(w => w.v12).Mean(),                        
                        v13Mean = w.Select(w => w.v13).Mean(),                        
                        v14Mean = w.Select(w => w.v14).Mean(),                        
                        v15Mean = w.Select(w => w.v15).Mean(),                        
                        v16Mean = w.Select(w => w.v16).Mean(),                        
                        v17Mean = w.Select(w => w.v17).Mean(),                                                
                        v18Mean = w.Select(w => w.v18).Mean(),                                                
                        v20Mean = w.Select(w => w.v20).Mean(),                       
                    }).ToCSV("result.csv");

                System.Console.WriteLine($"queried [{CNT}] rows in {stopw.Elapsed}");
            }
        }
    }

}
```

### execution

```sh
devel0@main:/opensource/devel0/netcore-csv$ cd example/
devel0@main:/opensource/devel0/netcore-csv/example$ dotnet run
written [500000] rows in 00:00:17.7151366
queried [500000] rows in 00:00:13.8399370
```

- generated input data sample

```sh
devel0@main:/opensource/devel0/netcore-csv/example$ head -n 3 test.csv 
"firstcol","i10","i20","SomeStringCol","FirstDblCol","v2","v3","v4","v5","v6","v7","v8","v9","v10","v11","v12","v13","v14","v15","v16","v17","v18","v19","v20"
0,5,12,"str:[18129689]",867557696.4707849,109447404.32754503,62481810.83355183,10286359.12122501,16821376.52152282,246951585.75053865,40531692.57963621,128706280.20200239,94060354.9098877,773084326.5415562,605406319.0731249,24301973.182848644,275546743.6628168,993341022.6336405,332197053.51265013,897891412.4415683,393898102.63826424,75625031.75606254,141746737.59459832,923235933.7262976
0,7,8,"str:[715246488]",778737590.5452006,746023428.9737527,143709297.35885435,259873150.9688651,974400662.8051404,228502796.13793957,726555496.7925677,918882383.9271824,937200791.1732424,243253674.4714033,217995068.1598834,805125237.3518074,83740469.57294479,305738162.85735846,624054313.9279143,934975130.9188899,116701281.68384604,279470807.5371901,296962312.5609766,391285082.04188436
```

- generated linq query over input data

```sh
devel0@main:/opensource/devel0/netcore-csv/example$ head -n 3 result.csv 
"i10","i20Min","i20Max","v1Mean","v2Mean","v3Mean","v4Mean","v5Mean","v6Mean","v7Mean","v8Mean","v9Mean","v10Mean","v11Mean","v12Mean","v13Mean","v14Mean","v15Mean","v16Mean","v17Mean","v18Mean","v20Mean"
5,1,19,498744375.0046595,500696328.76969767,498956994.79407644,498347553.3321365,499105076.1419511,497968869.1339944,501762405.8354361,499745779.22874564,500889471.2232371,500183490.45615464,499631274.71673,499687046.22139966,500878450.76341426,499645752.7216835,501762614.12378675,500649710.9467961,501233924.9635705,498505682.329863,499466519.5720193
7,1,19,500261473.80103374,499153526.46980953,499105413.8423311,498641774.89563894,500344995.4115497,499545597.67373264,501381194.974964,499761652.26916814,500232888.6299126,500631700.19801253,500045648.5480878,502821365.214899,500142713.6305659,499689342.6614191,498776087.82817686,498683736.7473624,498262792.1616414,500554332.6785145,500256673.0652077
```

- `test.csv` is the input data created
- `result.csv` is a linq query over that data

![](doc/test-result-comparision.png)

## How this project was built

```sh
mkdir netcore-csv
cd netcore-csv

dotnet new sln
dotnet new classlib -n netcore-csv
dotnet new console -n examples

cd netcore-csv
dotnet add package netcore-util --version 1.0.6
cd ..

cd example
dotnet add reference ../netcore-csv/netcore-csv.csproj
cd ..

dotnet sln netcore-csv.sln add netcore-csv/netcore-csv.csproj
dotnet sln netcore-csv.sln add example/example.csproj
dotnet build
```


## License
[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2Fdevel0%2Fnetcore-csv.svg?type=large)](https://app.fossa.io/projects/git%2Bgithub.com%2Fdevel0%2Fnetcore-csv?ref=badge_large)