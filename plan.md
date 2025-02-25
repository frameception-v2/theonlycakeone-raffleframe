### Step 1: Initialize Database Schema  
```text  
- Build: Create SQL tables for Participant (fid TEXT PRIMARY KEY, entryTimestamp INTEGER) and RaffleState (totalEntries INTEGER, status TEXT)  
- Outcome: Verify via DB client that tables exist and can insert test records like INSERT INTO Participant VALUES ('123', 1717020800)  
```  

### Step 2: Create POST Entry Endpoint with Farcaster Validation  
```text  
- Build: /api/enter endpoint that:  
  1. Validates Farcaster message signature using @farcaster/hub-web package  
  2. Rejects duplicates via fid uniqueness check  
  3. Inserts new Participant record  
- Outcome: Test with valid/invalid signatures using Farcaster CLI, check DB entries increment  
```  

### Step 3: Implement Stats Endpoint  
```text  
- Build: GET /stats returning {count: X, shareUrl: "/share"} with count from SELECT COUNT(*) FROM Participant  
- Outcome: curl http://localhost/api/stats returns valid JSON, count updates after new entries  
```  

### Step 4: Build Entry Frame UI  
```text  
- Build: Frame with:  
  - Dynamic image showing "Entries: ${count}" (fetch from /stats)  
  - "Enter Raffle" button (POST to /api/enter)  
  - "View Entries" button (link to stats page)  
- Outcome: Local frame render shows live counter and functional buttons via Frame Simulator  
```  

### Step 5: Create Confirmation Frame  
```text  
- Build: Post-entry screen showing:  
  - "You're in! Entry #${fid}" image  
  - "Share Frame" button with post_redirect to share URL  
  - "Check Status" button (GET /stats)  
- Outcome: After entry submission, confirmation displays with working share button  
```  

### Step 6: Implement Shared Counter Frame  
```text  
- Build: /share endpoint frame showing persistent "Total Entries: ${count}" using data from /stats  
- Outcome: Shared link displays current count, updates when new entries occur  
```  

### Step 7: Handle Duplicate & Validation Errors  
```text  
- Build: Error responses for:  
  - 409 Conflict (duplicate entry) with "Already entered" image  
  - 401 Unauthorized (bad signature) with "Invalid signature" graphic  
- Outcome: Test double submission and invalid signatures show error states  
```  

### Step 8: Add Entry Count Caching  
```text  
- Build: Cache totalEntries with 60s TTL using Cloudflare Cache API  
- Outcome: Disable DB and verify /stats still returns cached count for 1 minute  
```  

### Step 9: Implement Rate Limiting  
```text  
- Build: Rate limiter allowing 5 requests/sec per fid using KV store counters  
- Outcome: Rapid button clicks trigger 429 response with rate limit exceeded image  
```