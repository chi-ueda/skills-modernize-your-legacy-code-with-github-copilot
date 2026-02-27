# COBOL Student Account Management System - Test Plan

## Overview
This test plan documents comprehensive test cases for validating the business logic and implementation of the legacy COBOL student account management system. These test cases will serve as the basis for unit and integration tests in the modernized Node.js application.

---

## Test Cases

| Test Case ID | Test Case Description | Pre-conditions | Test Steps | Expected Result | Actual Result | Status | Comments |
|---|---|---|---|---|---|---|---|
| TC-001 | Display main menu with all options | Application started | 1. Run the program | Menu displays with options: 1. View Balance, 2. Credit Account, 3. Debit Account, 4. Exit | | | |
| TC-002 | Accept valid menu selection (1 - View Balance) | Main menu displayed | 1. Select option 1 | Program proceeds to view balance operation | | | |
| TC-003 | Accept valid menu selection (2 - Credit Account) | Main menu displayed | 1. Select option 2 | Program proceeds to credit operation | | | |
| TC-004 | Accept valid menu selection (3 - Debit Account) | Main menu displayed | 1. Select option 3 | Program proceeds to debit operation | | | |
| TC-005 | Accept valid menu selection (4 - Exit) | Main menu displayed | 1. Select option 4 | Program displays "Exiting the program. Goodbye!" and terminates | | | |
| TC-006 | Reject invalid menu selection (0) | Main menu displayed | 1. Select option 0 | Display error message "Invalid choice, please select 1-4." and return to menu | | | |
| TC-007 | Reject invalid menu selection (5) | Main menu displayed | 1. Select option 5 | Display error message "Invalid choice, please select 1-4." and return to menu | | | |
| TC-008 | Reject invalid menu selection (non-numeric) | Main menu displayed | 1. Enter non-numeric character | Handle appropriately and return to menu | | | |
| TC-009 | View balance - Display current balance | Account balance initialized to 1000.00, main menu displayed | 1. Select option 1 | Display "Current balance: 1000.00" and return to menu | | | |
| TC-010 | View balance - Display updated balance after credit | Account balance is 1000.00, credit of 500.00 applied, main menu displayed | 1. Select option 1 | Display "Current balance: 1500.00" and return to menu | | | |
| TC-011 | View balance - Display updated balance after debit | Account balance is 1000.00, debit of 250.00 applied, main menu displayed | 1. Select option 1 | Display "Current balance: 750.00" and return to menu | | | |
| TC-012 | Credit operation - Valid credit amount | Account balance is 1000.00, main menu displayed | 1. Select option 2 2. Enter amount 500 3. Confirm | Display "Amount credited. New balance: 1500.00" and return to menu; balance persists | | | |
| TC-013 | Credit operation - Credit with decimal amount | Account balance is 1000.00, main menu displayed | 1. Select option 2 2. Enter amount 50.50 3. Confirm | Display "Amount credited. New balance: 1050.50" and return to menu; balance persists | | | |
| TC-014 | Credit operation - Large credit amount | Account balance is 1000.00, main menu displayed | 1. Select option 2 2. Enter amount 999999.99 3. Confirm | Display "Amount credited. New balance: 1000999.99" and return to menu; balance persists | | | |
| TC-015 | Credit operation - Zero credit amount | Account balance is 1000.00, main menu displayed | 1. Select option 2 2. Enter amount 0 3. Confirm | Accept credit (no validation); Display "Amount credited. New balance: 1000.00" and return to menu | | | |
| TC-016 | Credit operation - Multiple consecutive credits | Account balance is 1000.00, main menu displayed | 1. Select option 2, enter 250, confirm 2. Select 1, verify balance 3. Select 2, enter 300, confirm 4. Select 1, verify balance | First credit: 1250.00; Second credit: 1550.00; Both balances display correctly | | | |
| TC-017 | Debit operation - Valid debit with sufficient funds | Account balance is 1000.00, main menu displayed | 1. Select option 3 2. Enter amount 250 3. Confirm | Display "Amount debited. New balance: 750.00" and return to menu; balance persists | | | |
| TC-018 | Debit operation - Debit with decimal amount and sufficient funds | Account balance is 1000.00, main menu displayed | 1. Select option 3 2. Enter amount 100.50 3. Confirm | Display "Amount debited. New balance: 899.50" and return to menu; balance persists | | | |
| TC-019 | Debit operation - Debit exactly equal to balance | Account balance is 500.00, main menu displayed | 1. Select option 3 2. Enter amount 500 3. Confirm | Display "Amount debited. New balance: 0.00" and return to menu; balance persists | | | |
| TC-020 | Debit operation - Debit with insufficient funds | Account balance is 500.00, main menu displayed | 1. Select option 3 2. Enter amount 600 3. Confirm | Display "Insufficient funds for this debit." and return to menu; balance remains 500.00 | | | |
| TC-021 | Debit operation - Debit amount greater than balance (large difference) | Account balance is 100.00, main menu displayed | 1. Select option 3 2. Enter amount 9999.99 3. Confirm | Display "Insufficient funds for this debit." and return to menu; balance remains 100.00 | | | |
| TC-022 | Debit operation - Debit with zero amount | Account balance is 1000.00, main menu displayed | 1. Select option 3 2. Enter amount 0 3. Confirm | Debit is accepted (0 <= 1000.00); Display "Amount debited. New balance: 1000.00" and return to menu | | | |
| TC-023 | Debit operation - Multiple consecutive debits | Account balance is 1000.00, main menu displayed | 1. Select option 3, enter 200, confirm 2. Select 1, verify balance 3. Select 3, enter 300, confirm 4. Select 1, verify balance | First debit: 800.00; Second debit: 500.00; Both balances display correctly | | | |
| TC-024 | Data persistence - Balance retained after credit operation | Account balance is 1000.00 | 1. Select option 2, enter 300, confirm 2. Return to main menu 3. Select option 1 | Balance displays as 1300.00; newly persisted value is retained | | | |
| TC-025 | Data persistence - Balance retained after debit operation | Account balance is 1000.00 | 1. Select option 3, enter 200, confirm 2. Return to main menu 3. Select option 1 | Balance displays as 800.00; newly persisted value is retained | | | |
| TC-026 | Data persistence - Balance retained through multiple operations | Account balance is 1000.00 | 1. Credit 500 2. Debit 200 3. Credit 100 4. View balance | Final balance: 1400.00; all operations persisted correctly | | | |
| TC-027 | Menu loop - Return to menu after view balance | Main menu displayed, balance is 1000.00 | 1. Select option 1 2. Observe menu redisplay | Menu redisplays after view balance operation | | | |
| TC-028 | Menu loop - Return to menu after credit operation | Main menu displayed, balance is 1000.00 | 1. Select option 2, enter 250, confirm 2. Observe menu redisplay | Menu redisplays after credit operation | | | |
| TC-029 | Menu loop - Return to menu after debit operation (sufficient funds) | Main menu displayed, balance is 1000.00 | 1. Select option 3, enter 100, confirm 2. Observe menu redisplay | Menu redisplay after successful debit operation | | | |
| TC-030 | Menu loop - Return to menu after debit operation (insufficient funds) | Main menu displayed, balance is 500.00 | 1. Select option 3, enter 999, confirm 2. Observe menu redisplay | Menu redisplays after failed debit due to insufficient funds | | | |
| TC-031 | Balance format - Initial balance has 2 decimal places | Application started, initial balance is 1000.00 | 1. Select option 1 | Display shows "Current balance: 1000.00" (with .00 suffix) | | | |
| TC-032 | Balance format - Balance displays 2 decimal places after decimal credit | Account balance is 1000.00, main menu displayed | 1. Select option 2, enter 25.75, confirm 2. Select option 1 | Balance displays as "1025.75" with exactly 2 decimal places | | | |
| TC-033 | Balance format - Balance displays 2 decimal places after decimal debit | Account balance is 1234.56, main menu displayed | 1. Select option 3, enter 100.76, confirm 2. Select option 1 | Balance displays as "1133.80" with exactly 2 decimal places | | | |
| TC-034 | Account initialization - Initial balance is 1000.00 | Fresh application start | 1. Select option 1 | Display "Current balance: 1000.00" | | | |
| TC-035 | Boundary test - Maximum credit amount | Account balance is 1000.00 | 1. Select option 2, enter 9999999.99, confirm 2. Select option 1 | Balance persists as 10000999.99; no overflow or error | | | |
| TC-036 | Boundary test - Very small debit amount | Account balance is 1000.00 | 1. Select option 3, enter 0.01, confirm 2. Select option 1 | Balance displays as "999.99"; debit accepted and persisted | | | |
| TC-037 | Integration test - Sequential credit and debit operations | Account balance is 1000.00 | 1. Credit 300 (1300.00) 2. Debit 150 (1150.00) 3. Credit 50 (1200.00) 4. Debit 200 (1000.00) 5. View balance | Final balance: 1000.00; all operations executed in sequence and persisted correctly | | | |
| TC-038 | Integration test - Debit to near-zero balance | Account balance is 1000.00 | 1. Debit 999 2. View balance 3. Debit 1 4. View balance | After first debit: 1.00; After second debit: 0.00; both displayed correctly | | | |
| TC-039 | Integration test - Recover from insufficient funds attempt | Account balance is 100.00 | 1. Attempt debit 200 (fails) 2. View balance (verify 100.00) 3. Credit 200 (300.00) 4. Debit 200 (100.00) | Failed debit does not affect balance; subsequent operations execute successfully | | | |
| TC-040 | Program exit - Graceful termination | Main menu displayed | 1. Select option 4 | Program displays "Exiting the program. Goodbye!" and terminates cleanly | | | |

---

## Test Execution Notes

### Data Setup
- Each test case assumes the DataProgram starts with initial balance of 1000.00
- Tests may be run independently or as a suite
- Balance state persists between menu operations within a single program execution
- Program restart resets balance to 1000.00

### Test Coverage Summary
- **Menu Navigation**: TC-001 through TC-008 (8 test cases)
- **View Balance Operation**: TC-009 through TC-011 (3 test cases)
- **Credit Operation**: TC-012 through TC-016 (5 test cases)
- **Debit Operation**: TC-017 through TC-023 (7 test cases)
- **Data Persistence**: TC-024 through TC-026 (3 test cases)
- **Menu Loop Behavior**: TC-027 through TC-030 (4 test cases)
- **Balance Format Validation**: TC-031 through TC-033 (3 test cases)
- **Initialization and Boundaries**: TC-034 through TC-036 (3 test cases)
- **Integration Tests**: TC-037 through TC-039 (3 test cases)
- **Program Termination**: TC-040 (1 test case)

**Total Test Cases**: 40

### Business Logic Coverage
✅ Menu selection and validation
✅ Balance inquiry
✅ Credit transactions (validation, amount handling, persistence)
✅ Debit transactions (validation, insufficient funds handling, persistence)
✅ Balance format (2 decimal places)
✅ Data persistence across operations
✅ Menu loop behavior
✅ Program termination

---

## Notes for Node.js Migration

When converting these test cases to unit and integration tests in Node.js:

1. **Menu Operation** (TC-001-TC-008): Convert to function/route tests for menu display and selection validation
2. **View Balance** (TC-009-TC-011): Convert to tests for balance retrieval API endpoint
3. **Credit Operation** (TC-012-TC-016): Convert to tests for credit endpoint with various amounts
4. **Debit Operation** (TC-017-TC-023): Convert to tests for debit endpoint including edge cases and validation
5. **Data Persistence** (TC-024-TC-026): Convert to integration tests using a database
6. **Format Validation** (TC-031-TC-033): Convert to output formatting tests
7. **Boundary Tests** (TC-034-TC-039): Convert to edge case unit tests

### Recommended Testing Framework
- **Unit Tests**: Jest or Mocha with Chai for individual business logic functions
- **Integration Tests**: Supertest for API endpoints + Jest for database interactions
- **Test Data**: Use database fixtures or factories for setup/teardown

