<h2 align="center"> The Great API Meltdown of 2024 </h2>

<p align="center">

<img src="Meme/Postmortem 1.png" width=100% height=100% />
<img src="Meme/Postmortem 2.png" width=100% height=100% />

</p>


<h4 align="center"> Issue Summary: </h4>

**Duration:**

Start: June 20, 2024, 2:00 PM EAT.
End: June 20, 2024, 4:30 PM EAT.

**Impact:**

Our API service experienced severe latency and intermittent outages, affecting approximately 75% of our user base. Users reported slow responses, timeouts, and occasional failures when trying to access our services.

**Root Cause:**

A sudden spike in API requests caused by an unintended infinite loop in a newly deployed microservice overwhelmed our servers, leading to resource exhaustion.

---

**Timeline:**

- **1:50 PM:** Issue detected through monitoring alerts indicating high API latency.
- **2:00 PM:** Engineering team notified via automated alert system.
- **2:05 PM:** Initial investigation began, focusing on network issues or potential DDoS attack.
- **2:15 PM:** Misleading path: Network team investigated potential external threats but found nothing.
- **2:30 PM:** Realized the issue was internal after checking server logs indicating high internal traffic.
- **2:35 PM:** Noticed a pattern of repeated API calls from a specific microservice.
- **2:45 PM:** Incident escalated to the microservices team.
- **3:00 PM:** Identified the offending microservice and rolled back the recent deployment.
- **3:15 PM:** API latency started to decrease, but issues persisted due to lingering server load.
- **3:45 PM:** Restarted affected servers to clear up residual resource exhaustion.
- **4:00 PM:** Full API functionality restored, monitoring for further issues.
- **4:30 PM:** Declared incident resolved after consistent normal operation for 30 minutes.

---

**Root Cause and Resolution:**

**Root Cause:**  
The root cause was traced to an infinite loop within a newly deployed microservice. This service, designed to handle background processing tasks, accidentally entered a loop due to a misconfigured endpoint, causing it to continuously send API requests.

**Resolution:**  
The issue was resolved by rolling back the deployment of the offending microservice. Further, affected servers were restarted to clear up resource exhaustion caused by the spike in traffic. The microservice code was subsequently reviewed and corrected to prevent the loop.

---

**Corrective and Preventative Measures:**

**Improvements Needed:**

- Enhance deployment review processes to catch such issues in staging environments.
- Improve monitoring to detect unusual internal traffic patterns.
- Implement rate limiting on API requests to prevent similar issues from affecting overall service.

**Specific Tasks:**

- **Review and Patch:** Conduct a thorough review of the microservice codebase and implement necessary patches to prevent infinite loops.
- **Enhance Monitoring:** Add detailed monitoring for internal traffic between services to catch unusual spikes early.
- **Rate Limiting:** Implement rate limiting on API endpoints to cap the number of requests any service can make in a given period.
- **Load Testing:** Introduce more rigorous load testing in staging environments to simulate potential failure points.
- **Incident Response Training:** Conduct incident response drills focusing on rapid identification and resolution of internal traffic issues.

---

**Conclusion:**

While the outage was a stressful and challenging experience, it provided valuable lessons on the importance of robust monitoring and thorough code reviews. By implementing the corrective measures outlined, we aim to prevent similar issues in the future and ensure a more resilient and reliable service for our users.

---
