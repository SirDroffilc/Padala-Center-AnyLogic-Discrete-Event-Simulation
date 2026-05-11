# Statistics View

## **I. Histograms: The Efficiency Suite**

Histograms show the **distribution** of data. They answer not just "what was the average?" but "how often did we hit our targets?" and "how consistent is our operation?"

| Chart Name | What it Represents (Logic) | Reality Equivalent |
| --- | --- | --- |
| **1. Customer Turn Around Time** | Time from `sourceCustomers` entry to `sinkCustomer` exit. | **Customer Service Experience:** The total time a customer spends in the store, including walking and waiting. |
| **2. Packaging Process Time** | Time from `splitToPackages` until `releaseMLForPackaging`. | **Value-Added Time:** The physical efficiency of your labeling, boxing, and preparation stage. |
| **3. Package Storage Time** | Time from `releaseMLForPackaging` until `releaseMLForStorage`. | **Placement Speed:** How quickly your workers clear the prep area and move items to the floor. |
| **4. Package Loading Time** | Time from `releaseMLForStorage` until `releaseMLForLoading`. | **Staging/Wait Efficiency:** High values here usually represent the time inventory spends "dead" on the floor waiting for a truck. |
| **5. Package Turn Around Time** | Total time from "birth" at the split to entering `sinkPackages`. | **Internal Lead Time:** The total lifecycle of an item inside the warehouse. |
| **6. Truck Turn Around Time** | Time from parking at `waitAtDock` until departure at `sink`. | **Logistics Performance:** The total time a truck spends inside the warehouse. |

### **How to Interpret Histograms**
Using the provided chart as a reference, here is what each visual element represents:

#### **1. The Green Vertical Bars (Frequency Bins)**

* **What they are:** Each bar represents a "bin" or a specific time interval (e.g., 0.5 to 1.0 minutes).
* **The Y-Axis (Height):** Shows the percentage of total agents that fell into that specific time range.
* **Interpretation:** The tallest bar represents the **Mode**—the most frequent experience for a customer or package. 

#### **2. The Pink Vertical Line (The Mean)**
* **What it is:** This represents the mathematical average ($\mu$) of all recorded data points.


#### **3. The Teal Curved Line (The CDF)**

* **What it is:** This is the **Cumulative Distribution Function**. It is the running total of all bars from left to right.
* **Interpretation:** The line always starts at $0\%$ and ends at $100\%$ ($1.0$). The steeper the line, the more "consistent" your warehouse is.
* **Reality Check:** If the line is very flat, it means your turnaround times are all over the place (high unpredictability).


#### **4. PDF: Probability Density Function (The Bars)**

* **Definition:** Represents the likelihood of an outcome falling within a **specific** interval.
* **Utility:** Use this to answer: *"What is the chance a customer finishes in exactly 1 minute?"*
* **Visual Interpretation:** If the bars are tightly bunched around the mean, your warehouse is "Stable." If the bars are spread wide, your warehouse is "Volatile."

#### **5. CDF: Cumulative Distribution Function (The Line)**

* **Definition:** Represents the probability that an outcome will be **less than or equal to** a specific value.
* **Utility:** This is the most important metric for **Service Level Agreements (SLAs)**.
* **Example from Image:** Find where the teal line crosses the $30\%$ mark on the Y-axis. Look down to the X-axis (approx. $1.1$).
* **Report Statement:** "We are $30\%$ certain that the turnaround time will be $1.1$ minutes or less."


---

## **II. Bar Chart: The Resource Utilization Suite**

The Bar Chart provides a snapshot of **Resource Efficiency**. It measures how much of your total capacity is being used over the entire simulation run.

### **1. Customer Service Employees**

* **What it means:** The percentage of the shift that service desk workers spend processing customer orders.
* **Interpretation:** * **Above 85%:** You likely have a customer queue. Wait times will be high.
* **Below 40%:** You are overstaffed at the front desk; workers are idle too often.

### **2. Manual Labor Employees**

* **What it means:** The percentage of time your warehouse staff spends moving, packaging, and loading.
* **Interpretation:**
* **High Utilization (80–95%):** Your workers are productive, but the system is "brittle." If a truck arrives unexpectedly, there may be no one free to load it immediately.
* **Low Utilization (<50%):** You have excess labor capacity. You could likely handle a higher customer arrival rate without needing more staff.


