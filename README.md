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

---


### 2. The Journey (The How)

### Phase 0: Concept Validation
Before spending money on any extra hardware or adapters, I wanted to see if it was even possible to share internet traffic this way. 
* **The Setup:** I connected my PC to the internet and used AI for guidance to figure out the local routing mechanics. I managed to successfully set up a software bridge to broadcast the link from the PC.
* **The Catch:** While it worked and validated that the routing logic was sound, the internet only stayed live if the host PC itself remained powered on and actively tethered. 
* **The Conclusion:** This is obviously not practical for a daily study setup, but it proved the idea works. Now I need to figure out a way to move the connection through a dedicated hardware bridge instead of keeping the PC running 24/7.

### Phase 1: Physical Layer Testing & The Hardware Wall (Dec 12 – Dec 26, 2025)
Once the Amkette 8-in-1 multi-port hub finally arrived, I spent days testing it with my mom's Samsung Galaxy A35 to establish a direct hardware bridge via a CAT 5e UTP cable plugged into the router's WAN port. 

#### 1. Learning the Physical LED Interface
Before looking at software settings, I had to learn what the physical port lights actually meant so I could see how the hardware was handshaking:
* **Yellow Light:** Indicates active data packet transmission. If it stays completely solid/static and doesn't flicker, no data is moving.
* **Green vs. Red/Orange Light:** Indicates the link speed capability. I discovered the green light isn't fixed. When testing a link directly between the hub and my PC's port, the LED turned **Red/Orange**, showing a degraded connection profile or a total failure to negotiate proper speeds.

#### 2. Core Obstacles with the A35
I hit massive, unexpected hardware lockouts during my attempts:
* **The Power Delivery (PD) Conflict:** The moment I plugged a fast charger into the hub's PD port to keep my mom's phone charged during study sessions, the phone completely refused to tether. The "Ethernet Tethering" toggle instantly greyed out and became unavailable.
* **The "No Internet" Trap:** Even on battery power when I successfully toggled Ethernet Tethering ON, the PC connected to the router's Wi-Fi still showed "No Internet," and the physical LEDs remained completely static without flickering.

#### 3. Troubleshooting Steps & Sequences I Attempted
I realized quickly that in networking, you can't just randomly connect components; sequences matter heavily. I tested multiple distinct approaches:

* **The "Wake Up" Sequence:** I tried a timed reboot order: Unplug ethernet -> Turn OFF tethering -> Unplug the Jio Router's power for 10 seconds -> Wait for the router's Wi-Fi light to blink -> Re-plug everything -> Toggle tethering back ON. *Result: Still no internet status.*
* **Killing DHCP:** I logged into the router's admin dashboard and turned DHCP completely OFF. *Result:* Total communication breakdown. The phone stopped recognizing the router entirely, forcing me to toggle DHCP back ON just to restore basic interface visibility.
* **The Low-Battery Security Lockout:** During these heavy testing cycles, the Ethernet option suddenly refused to turn ON altogether. I noticed the phone's battery had dropped down to 12%. I deduced that Android systems silently lock out power-heavy external network drivers at low battery percentages as a core safety feature.
* **Developer Settings Tweaks:** I went deep into Android Developer Options and manually enabled *USB Tethering in Default USB Configurations* and *Tethering Hardware Acceleration*, while ensuring *Data Saver* was completely OFF. *Result: Still stuck on a solid Red/Orange light with zero yellow activity.*

#### 4. Final Phase 1 Conclusion & Hypothesis
After executing every loop sequence possible, the Ethernet Tethering on the A35 simply would not route data. 
* **My Hypothesis:** Since this is a massive multi-port hub and not a simple single-purpose Ethernet-to-Type-C adapter, the Samsung A35's basic software build likely lacks the necessary kernel drivers to talk to the hub's internal network controller chip.
* **Next Step:** My brand new personal phone—a Samsung Galaxy M36 5G—is scheduled to arrive in 2 days (Dec 28th). I finally got it because I am entering Class 12 and genuinely need my own device for my studies. Before giving up and returning the hub, I will hold onto it to run an isolated chipset test using my new phone to see if it's a driver barrier or a dead hub.

