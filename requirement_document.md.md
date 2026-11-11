# Topic 3 -- Requirements Document

## Working with Core Nodes & Data Mapping

### 1. Objective

Build an n8n workflow that creates initial product data, modifies an
existing value, dynamically maps an incoming field, and calculates a new
value using expressions.

### 2. Scope

**In scope** - Use a Manual Trigger to start the workflow. - Use Edit
Fields nodes to create and modify data. - Create String, Number, and
Boolean fields. - Overwrite an existing field. - Map an incoming field
dynamically with an n8n expression. - Calculate a value using a simple
arithmetic expression. - Execute the workflow and inspect the final JSON
output.

**Out of scope** - Complex JavaScript logic and loops. - Nested JSON
arrays or objects. - Advanced formatting or rounding functions.

### 3. Functional Requirements

  -----------------------------------------------------------------------
  ID                                  Requirement
  ----------------------------------- -----------------------------------
  REQ-001                             The initial data node must create
                                      `productName`, `basePrice`, and
                                      `isAvailable`.

  REQ-002                             `productName` must be String,
                                      `basePrice` must be Number, and
                                      `isAvailable` must be Boolean.

  REQ-003                             The second Edit Fields node must
                                      overwrite `isAvailable` from `true`
                                      to `false`.

  REQ-004                             The second node must create
                                      `inventoryLabel` dynamically from
                                      the incoming `productName`.

  REQ-005                             The second node must create
                                      `priceWithTax` using the incoming
                                      `basePrice` multiplied by `1.1`.

  REQ-006                             The final output must retain the
                                      original product fields and include
                                      the modified and newly mapped
                                      fields in one output item.
  -----------------------------------------------------------------------

### 4. Technical Requirements

  -----------------------------------------------------------------------
  ID                                  Requirement
  ----------------------------------- -----------------------------------
  TR-001                              Use the n8n Manual Trigger node.

  TR-002                              Use Edit Fields (Set) nodes for
                                      data creation and transformation.

  TR-003                              Use the expression
                                      `{{ $json.productName }}` for
                                      dynamic mapping.

  TR-004                              Use the expression
                                      `{{ $json.basePrice * 1.1 }}` for
                                      the tax calculation.

  TR-005                              Preserve incoming fields when
                                      producing the final output.
  -----------------------------------------------------------------------

### 5. Initial Test Data

  Field           Type      Required value
  --------------- --------- ------------------
  `productName`   String    `Wireless Mouse`
  `basePrice`     Number    `25`
  `isAvailable`   Boolean   `true`

### 6. Expected Final Data

  Field              Expected value     Type
  ------------------ ------------------ ---------
  `productName`      `Wireless Mouse`   String
  `basePrice`        `25`               Number
  `isAvailable`      `false`            Boolean
  `inventoryLabel`   `Wireless Mouse`   String
  `priceWithTax`     `27.5`             Number

### 7. Assumptions and Constraints

-   The workflow uses mock product data.
-   The tax calculation is a simple multiplication by `1.1`.
-   Floating-point rounding corrections are outside the exercise scope.
-   The final value may display a minor floating-point precision
    difference in n8n.
