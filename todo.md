#### Setup
- [x] Task 1: Initialize Database Schema  
  - Build SQL tables for Participant and RaffleState  
  - **Outcome**: Verify tables exist and test records can be inserted.

#### Core Features
- [ ] Task 2: Create POST Entry Endpoint with Farcaster Validation  
  - Depends on: Task 1  
  - **Build**: `/api/enter` endpoint with signature validation and fid uniqueness checks.  
  - **Outcome**: Test with valid/invalid signatures and check DB updates.
  
- [ ] Task 3: Implement Stats Endpoint  
  - Depends on: Task 1  
  - **Build**: GET `/stats` returning entry count and share URL.  
  - **Outcome**: Confirm JSON response updates with new entries.

- [ ] Task 4: Build Entry Frame UI  
  - Depends on: Task 2, Task 3  
  - **Build**: Frame with dynamic entry count, "Enter Raffle" button, and "View Entries" link.  
  - **Outcome**: Verify live counter and button functionality in Frame Simulator.

- [ ] Task 5: Create Confirmation Frame  
  - Depends on: Task 2  
  - **Build**: Post-entry screen showing entry number, share button, and stats link.  
  - **Outcome**: Test confirmation display and share redirect after submission.

- [ ] Task 6: Implement Shared Counter Frame  
  - Depends on: Task 3  
  - **Build**: `/share` endpoint displaying persistent total entries.  
  - **Outcome**: Confirm shared link reflects real-time count updates.

#### API Integration
- [ ] Task 7: Handle Duplicate & Validation Errors  
  - Depends on: Task 2  
  - **Build**: Error responses (409/401) with user-friendly images.  
  - **Outcome**: Test duplicate entries and invalid signatures for error states.

- [ ] Task 8: Add Entry Count Caching  
  - Depends on: Task 3  
  - **Build**: Cache totalEntries with 60s TTL.  
  - **Outcome**: Validate cached count works after DB disable.

- [ ] Task 9: Implement Rate Limiting  
  - Depends on: Task 2  
  - **Build**: 5 requests/sec limit per fid.  
  - **Outcome**: Confirm 429 responses on excessive requests.

#### UI/UX
*(No additional tasks—UI components are covered under Core Features)*  

---

### Implementation Plan  
1. **Database Setup**: Complete Task 1 first to enable all subsequent features.  
2. **Core API Endpoints**: Prioritize Tasks 2 and 3 to unblock UI development.  
3. **Frames**: Implement Tasks 4–6 immediately after API endpoints for rapid user testing.  
4. **Enhancements**: Add error handling (Task 7), caching (Task 8), and rate limiting (Task 9) post-MVP.  

**Critical Path**: Task 1 → Task 2/Task 3 → Task 4 → Task 5/Task 6.