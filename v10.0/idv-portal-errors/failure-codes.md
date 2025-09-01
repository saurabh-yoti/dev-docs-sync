---
type: page
title: Failure Codes
listed: true
slug: failure-codes
description: 
index_title: Failure Codes
hidden: 
keywords: 
tags: 
---

---

### Mandatory Document Not Provided

**Reason:** The user does not have sufficient documents to reach the target level of identity verification.

_This may be returned as an aborted reason, or a requirements not met reason._

**Digital ID:** ✅  

**Embedded IDV:** ✅

---

### FRAUD_DETECTED

**Description:** Suspected fraud for the given identity therefore unable to reach the required identity profile. This should be reviewed.

**Digital ID:** ✅  

**Embedded IDV:** ✅

### UNABLE_TO_VALIDATE_DOCUMENT

**Description:** We have not been able to successfully validate a required document (for reasons other than suspected fraud, e.g. capture error).

**Digital ID:** ✅  

**Embedded IDV:** ✅

### MISSING_LIVENESS

**Description:** Returned if the session does not have a passed liveness check.

**Digital ID:** ❌  

**Embedded IDV:** ✅

### IDENTITY_CHECK_FAILED

**Description:** Additional checks on a user’s identity, required to meet the level of confidence, have not been successful. Will be triggered by a PEP flag or deceased flag.

**Digital ID:** ✅  

**Embedded IDV:** ✅

### UNABLE_TO_COMPLETE_CHECKS

**Description:** Required checks could not be completed.

**Digital ID:** ✅  

**Embedded IDV:** ✅

### COULD_NOT_VERIFY_ADDRESS

**Description:** Could occur if the address was not verified for any reason after the applicant leaves the session.

**Digital ID:** ❌  

**Embedded IDV:** ✅

### FACE_MATCH_VERIFICATION_FAILED

**Description:** The face match check could not be performed.

**Digital ID:** ❌  

**Embedded IDV:** ✅

### FACE_MATCH_HIGHER_THRESHOLD_VERIFICATION_FAILED

**Description:** In some circumstances, a higher level of confidence in the face match is required, such as if the presented identity is at higher risk of identity fraud. This reason code is returned if such a higher threshold could not be met.

**Digital ID:** ✅  

**Embedded IDV:** ✅

### ACTIVITY_HISTORY_SCORE_INSUFFICIENT

**Description:** The profile has not reached the required activity history score for the specified scheme.

**Digital ID:** ❌  

**Embedded IDV:** ✅

### IDENTITY_FRAUD_SCORE_INSUFFICIENT

**Description:** The profile has not reached the identity fraud score for the specified scheme.

**Digital ID:** ❌  

**Embedded IDV:** ✅

### IDENTITY_FRAUD_AND_ACTIVITY_HISTORY_SCORES_INSUFFICIENT

**Description:** The profile has not reached both the identity fraud activity history scores for the specified scheme.

**Digital ID:** ❌  

**Embedded IDV:** ✅

### MISSING_FRAUD_LIST_CHECK

**Description:** This error can arise if a technical problem occurs while checking the identity against a fraud list.

**Digital ID:** ❌  

**Embedded IDV:** ✅

### ABANDONED

**Description:**  Expired sessions will eventually be set to ABANDONED, there is approximately a two hour delay between this aborted reason appearing from expiry.