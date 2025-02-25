# CsvReader<T> Class
**Namespace:** SearchAThing.CSV

**Inheritance:** Object → CsvReader<T>

read data from csv creating a object enumerable.
            an object template with a property foreach csv column is required with same order as they appears in csv.
            attributes CsvHeaderAttribute and CsvColumnOrderAttribute can be specified on properties to custommize header and order.

## Signature
```csharp
public class CsvReader : System.Collections.Generic.IEnumerable<T>, System.Collections.IEnumerable, System.IDisposable
```
## Constructors
|**Name**|**Summary**|
|---|---|
|[CsvReader<T>(string, string, string)](CsvReader-1/ctors.md)|read csv from given pathfilename with field and decimal separator using templated object properties as descriptor for csv column headers to expect|
## Methods
|**Name**|**Summary**|
|---|---|
|[Dispose](CsvReader-1/Dispose.md)||
|[Equals](CsvReader-1/Equals.md)||
|[GetEnumerator](CsvReader-1/GetEnumerator.md)||
|[GetHashCode](CsvReader-1/GetHashCode.md)||
|[GetType](CsvReader-1/GetType.md)||
|[ToString](CsvReader-1/ToString.md)||
## Conversions
