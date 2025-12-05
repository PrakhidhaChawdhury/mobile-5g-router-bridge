# mobile-5g-router-bridge

A structured log of reverse-engineering an idle home gateway router to capture, amplify, and distribute an unlimited mobile 5G data hotspot, followed by tracking the physical and network layer constraints encountered during hardware isolation.

---

## 1. The Background Incentive (The Why)

* **The Core Strategy:** Entering Class 12, I made a calculated decision to attend a government school and rely entirely on self-directed online learning. Because the syllabus is national, the core educational material is easily accessible via the internet, a capability highly amplified by utilizing AI tools.
* **The Tuition Experiment:** Joining private tuition classes is the heavy societal norm in my community. To ensure my calculation wasn't blind, I enrolled in tuition for a 2-month trial period to evaluate the actual reality. The experience confirmed that the return on investment (ROI) was low, giving me the objective data needed to completely opt out.
* **The Long-Term ROI:** My parents offered to enroll me multiple times, but I denied the offers. By bypassing private school and tuition fees, my goal is to save that massive chunk of capital now so it can be reallocated to my future college education, where its impact will be significantly higher.
* **The Infrastructure Bottleneck:** Optimizing expenses meant a dedicated home Wi-Fi subscription or an independent heavy data plan wasn't a viable option. I had to rely entirely on the unlimited 5G data plan on my mom's phone.
* **The Physical Problem:** My mom needed to use her phone normally, while I needed her hotspot to study. Due to the physical distance between where she needed to be and my workspace, relying on a direct phone-to-device hotspot created highly unstable signal degradation. This left me with a constant background anxiety about sudden disconnects during study sessions.
* **The Objective:** To eliminate this anxiety and create an isolated, high-range wireless environment, I decided to repurpose an idle Jio Home Gateway router left over from a previous post-exam period. The goal was to force the router to ingest my mom's mobile 5G link and broadcast it cleanly across the house, stabilizing the range for my learning setup.
