# Topic 3 -- Implementation Document

## Working with Core Nodes & Data Mapping

### 1. Workflow Details

**Workflow name:** Topic 3 Core Nodes Workflow

**Node sequence:** Manual Trigger → Set Original Data → Modify & Map

### 2. Manual Trigger

The Manual Trigger node starts the workflow when the user clicks the
workflow test/execute control.

### 3. Set Original Data

An Edit Fields node renamed **Set Original Data** creates the initial
product data.

  Field           Type      Value
  --------------- --------- ------------------
  `productName`   String    `Wireless Mouse`
  `basePrice`     Number    `25`
  `isAvailable`   Boolean   `true`

### 4. Modify & Map

A second Edit Fields node renamed **Modify & Map** receives the first
node's data.

#### Task A -- Modify an existing field

-   Field: `isAvailable`
-   Type: Boolean
-   Value: `false`
-   This overwrites the incoming value `true`.

#### Task B -- Dynamically map a field

-   Field: `inventoryLabel`
-   Type: String
-   Expression: `{{ $json.productName }}`
-   This copies the incoming `productName` value dynamically.

#### Task C -- Calculate a new field

-   Field: `priceWithTax`
-   Type: Number
-   Expression: `{{ $json.basePrice * 1.1 }}`
-   This calculates the base price plus 10%.

The second node is configured to retain the incoming fields so that
`productName` and `basePrice` remain in the final output.

### 5. Execution and Verification

The workflow was executed successfully. The final output contained one
item with the following values:

``` json
{
  "productName": "Wireless Mouse",
  "basePrice": 25,
  "isAvailable": false,
  "inventoryLabel": "Wireless Mouse",
  "priceWithTax": 27.500000000000004
}
```

### 6. Implementation Notes

-   The output confirms that the Boolean field was overwritten.
-   The `inventoryLabel` value was mapped from the incoming
    `productName`.
-   The calculation used the incoming numeric `basePrice`.
-   The observed calculated value has a small floating-point precision
    difference from `27.5`. This is expected in JavaScript arithmetic
    and was not rounded because rounding corrections are outside the
    exercise scope.
