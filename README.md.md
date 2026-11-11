# Topic 3 -- Core Nodes & Data Mapping

## Project Overview

This n8n workflow demonstrates how to create initial data with the
**Manual Trigger** and **Edit Fields** nodes, modify an existing field,
map incoming data dynamically, and calculate a new numeric value using
an expression.

## Workflow

`Manual Trigger` → `Set Original Data` → `Modify & Map`

## Workflow Data

### Set Original Data

  Field           Type      Value
  --------------- --------- ------------------
  `productName`   String    `Wireless Mouse`
  `basePrice`     Number    `25`
  `isAvailable`   Boolean   `true`

### Modify & Map

  Field              Type      Value / Expression
  ------------------ --------- -------------------------------
  `isAvailable`      Boolean   `false`
  `inventoryLabel`   String    `{{ $json.productName }}`
  `priceWithTax`     Number    `{{ $json.basePrice * 1.1 }}`

The second Edit Fields node retains the incoming fields while updating
and adding the required fields.

## Verified Output

The executed workflow returned one item containing: - `productName`:
`Wireless Mouse` - `basePrice`: `25` - `isAvailable`: `false` -
`inventoryLabel`: `Wireless Mouse` - `priceWithTax`:
`27.500000000000004`

The calculated value is the result observed in n8n. The small
floating-point precision difference from the mathematically expected
`27.5` is normal for JavaScript number arithmetic. No rounding
correction was added, in keeping with the stated course scope.

## Concepts Demonstrated

-   String, Number, and Boolean data types
-   Updating an existing field
-   Passing incoming fields through
-   Dynamic mapping with n8n expressions
-   Basic arithmetic expressions
-   Workflow execution and output inspection

## Files in This Repository

-   `README.md` -- Project overview and verified output
-   `requirement.md` -- Functional and technical requirements
-   `implementation.md` -- Workflow setup and configuration
-   `testing-results.md` -- Actual implementation verification results

## Platform

n8n (cloud workflow editor)

## Note

This repository documents the workflow implementation and the execution
result observed during development. The trainer's separate formal test
plan can be added to the testing record when it is provided and
executed.
