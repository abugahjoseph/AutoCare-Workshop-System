# Test Plan and Results
**Test environment:** Python 3.10+, Flask test client, SQLite in-memory database, pytest.

## Test approach
- Unit/integration tests use Flask's test client and isolated in-memory SQLite.
- Manual acceptance tests should be completed by the team on the demo machine.
- Test data must be fictional.

## Test cases
| ID | Scenario | Steps / input | Expected result | Result |
|---|---|---|---|---|
| TC-01 | Dashboard loads | GET `/` | HTTP 200 and AutoCare heading | Automated |
| TC-02 | Customer registration | POST valid name and phone | Customer stored; vehicle form shown | Automated |
| TC-03 | Invalid status rejected | POST status `NotAStatus` | Existing status unchanged | Automated |
| TC-04 | Vehicle uniqueness | Register same plate twice | Duplicate rejected with message | Manual |
| TC-05 | Job creation | Select vehicle, complaint, costs | Job card appears on dashboard | Manual |
| TC-06 | Payment recording | Add positive amount and method | Payment appears in recent payments | Manual |
| TC-07 | SMS mock | Update status in mock mode | Mock notification logged; no SMS sent | Manual |
| TC-08 | Twilio sandbox | Configure approved test credentials | Provider accepts or reports error | Optional |

## Automated test results
Run `pytest -q`. The included suite contains three tests: homepage response, customer registration, and invalid status validation. Record the actual terminal output and date here after running in your environment. Do not claim a pass until the tests have been executed.

## Defect log
| Defect ID | Description | Severity | Owner | Status |
|---|---|---|---|---|
| D-01 | [Record observed defect] | [Low/Med/High] | [Name] | [Open/Closed] |

## Sign-off
Tester: [Name]  Date: [Date]  Lecturer/demo witness: [Name]
