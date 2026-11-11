# Topic 3 -- Testing Results Document

## Working with Core Nodes & Data Mapping

### 1. Test Environment

-   **Platform:** n8n Cloud
-   **Workflow:** Topic 3 Core Nodes Workflow
-   **Workflow sequence:** Manual Trigger → Set Original Data → Modify &
    Map
-   **Test data:** Wireless Mouse, base price 25, availability true

### 2. Execution Verification

  --------------------------------------------------------------------------------------
  Test ID        Test scenario  Expected result    Actual result          Status
  -------------- -------------- ------------------ ---------------------- --------------
  TV-001         Execute the    Workflow executes  Workflow executed and  PASS
                 workflow       successfully       produced output        

  TV-002         Verify initial `productName` and  `Wireless Mouse` and   PASS
                 product fields `basePrice` appear `25` appeared          
                 are retained   in final output                           

  TV-003         Verify Boolean `isAvailable`      Output showed `false`  PASS
                 overwrite      changes from                              
                                `true` to `false`                         

  TV-004         Verify dynamic `inventoryLabel`   Output showed          PASS
                 mapping        matches incoming   `Wireless Mouse`       
                                `productName`                             

  TV-005         Verify tax     `priceWithTax` is  Output showed          PASS\*
                 calculation    calculated from    `27.500000000000004`   
                 expression     `25 * 1.1`                                

  TV-006         Verify final   One output item    One item contained all PASS
                 output         contains all five  five fields            
                 structure      fields                                    
  --------------------------------------------------------------------------------------

### 3. Actual Output

``` json
{
  "productName": "Wireless Mouse",
  "basePrice": 25,
  "isAvailable": false,
  "inventoryLabel": "Wireless Mouse",
  "priceWithTax": 27.500000000000004
}
```

### 4. Additional Dynamic Mapping Check

The source `productName` was temporarily changed to `Bluetooth Keyboard`
and the workflow was executed again. The output showed: - `productName`:
`Bluetooth Keyboard` - `inventoryLabel`: `Bluetooth Keyboard`

This confirms that `inventoryLabel` was dynamically mapped rather than
hardcoded. The original product name was then restored to
`Wireless Mouse`.

### 5. Test Summary

-   Total verification checks: 6
-   Passed: 6
-   Failed: 0

**Note on TV-005:** The observed result `27.500000000000004` is a minor
floating-point precision effect from JavaScript arithmetic. The
calculation expression is correct. No rounding correction was applied
because the course scope excludes floating-point rounding corrections.

### 6. Testing Limitation

These results document the execution and checks actually performed
during implementation. They are not represented as execution of a
separate formal trainer test plan. Formal test case IDs and results can
be added after the trainer's testing plan is supplied and each case is
executed.
