# W01 Assignment: Build .NET Applications with C#

## 1. ASP.NET Core Web API — Pizza List

I completed the ASP.NET Core Web API tutorial and added an additional pizza to the `Pizzas` list in `PizzaService`.

**Endpoint:** `GET http://localhost:5297/pizza`

**Response:**

```json
[
  {
    "id": 1,
    "name": "Classic Italian",
    "isGlutenFree": false
  },
  {
    "id": 2,
    "name": "Veggie",
    "isGlutenFree": true
  },
  {
    "id": 3,
    "name": "Pepperoni",
    "isGlutenFree": false
  }
]
```

*Note: This is sample output. Replace it with your actual pizza list and identify the pizza you added.*

## 2. CRUD API Testing

### GET — Retrieve All Pizzas

**Request:**

```http
GET http://localhost:5297/pizza
```

**Status Code:** 200 OK (replace with actual result)

**Response:**

```json
[
  {
    "id": 1,
    "name": "Classic Italian",
    "isGlutenFree": false
  }
]
```

### POST — Create a Pizza

**Request:**

```http
POST http://localhost:5297/pizza
Content-Type: application/json

{
  "name": "Pepperoni",
  "isGlutenFree": false
}
```

**Status Code:** 201 Created (replace with actual result)

**Response:**

Paste the actual response body and relevant response headers here.

### PUT — Update a Pizza

**Request:**

```http
PUT http://localhost:5297/pizza/1
Content-Type: application/json

{
  "id": 1,
  "name": "Updated Pepperoni",
  "isGlutenFree": false
}
```

**Status Code:** 204 No Content (replace with actual result)

**Response:** No response body, if your API returns 204.

### DELETE — Delete a Pizza

**Request:**

```http
DELETE http://localhost:5297/pizza/1
```

**Status Code:** 204 No Content (replace with actual result)

**Response:** No response body, if your API returns 204.

## 3. Sales Summary Function

I extended the file-processing application to generate a sales summary report containing the total sales and sales totals for each file.

**Function implementation:**

```csharp
// Generate Sales Summary Report
void GenerateSalesSummary(
    IEnumerable<string> salesFiles,
    double salesTotal,
    string outputDirectory)
{
    StringBuilder report = new StringBuilder();

    report.AppendLine("Sales Summary");
    report.AppendLine("----------------------------");
    report.AppendLine($"Total Sales: {salesTotal:C}");
    report.AppendLine();
    report.AppendLine("Details:");

    foreach (var file in salesFiles)
    {
        string salesJson = File.ReadAllText(file);

        SalesData? data =
            JsonConvert.DeserializeObject<SalesData>(salesJson);

        double fileTotal = data?.Total ?? 0;

        string fileName = Path.GetFileName(file);

        report.AppendLine($"{fileName}: {fileTotal:C}");
    }

    string reportPath = Path.Combine(
        outputDirectory, "totals.txt");

    File.WriteAllText(reportPath, report.ToString());
}

```

**Example generated report:**

```text
Sales Summary
----------------------------
Sales Summary
----------------------------
Total Sales: $2,012.20

Details:
sales.json: $88.88
sales.json: $501.22
salestotals.json: $0.00
sales.json: $1,234.22
salestotals.json: $0.00
sales.json: $99.00
salestotals.json: $0.00
sales.json: $88.88
salestotals.json: $0.00
```


## 4. Conclusion

I completed the .NET learning modules, implemented and tested CRUD operations in the ASP.NET Core Pizza API, and extended the file-processing application to generate a sales summary report.