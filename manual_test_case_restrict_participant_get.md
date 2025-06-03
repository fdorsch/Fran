# Manual Test Case: GET /api/v1/restrictParticipant/{contextId}

## Test Case ID
TC_RESTRICT_PARTICIPANT_GET_01

## Title
Verify GET /api/v1/restrictParticipant/{contextId} returns 200 and restriction status JSON for a valid request

## Preconditions
- The Letters Service is running and accessible.
- The user executing the test is authenticated and has necessary permissions.
- There exists a valid {contextId} for a participant, both restricted and unrestricted.

## Test Steps

1. **Prepare a valid contextId**
   - Identify or create a participant with a known restricted status (both restricted and unrestricted cases should be tested).

2. **Send GET request**
   - Endpoint: `/api/v1/restrictParticipant/{contextId}`
   - Method: `GET`
   - Headers:
     - `Authorization: Bearer <valid_token>`
     - `Accept: application/json`

3. **Observe the response**

## Expected Result

- Response code is **200 OK**.
- Response body is a JSON object with the restriction evaluation status.
- Example for a restricted participant:
  ```json
  {
    "restricted": true,
    "reason": "User does not have access to this participant"
  }
  ```
- Example for an unrestricted participant:
  ```json
  {
    "restricted": false
  }
  ```
- The response contains only the allowed fields (no sensitive information leaked).
- The `restricted` field accurately reflects the participant's restriction status.

## Postconditions
- No changes are made to the system (GET is read-only).

## Notes
- Repeat the test with both restricted and unrestricted participants.
- If the contextId does not exist, verify that the service returns an appropriate error (e.g., 404 Not Found).
- If the user is not authorized, verify a 401 or 403 response is returned.
