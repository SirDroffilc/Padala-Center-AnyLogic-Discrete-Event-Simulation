## **I. Logic View: Customers and Packages**

This flow represents the "Inbound and Processing" phase. It simulates the physical movement of people and the creation of physical inventory from digital orders.

### **Phase A: The Customer Journey**

| Block | Type | Reality Equivalent | Logic Function |
| --- | --- | --- | --- |
| **1. sourceCustomers** | Source | Store Entrance | Generates customer entities based on a defined arrival rate. |
| **2. toCusServ** | MoveTo | Walking to Counter | Simulates the time/space taken for a customer to reach the service area. |
| **3. queueCusServ** | Queue | Physical Waiting Line | Holds customers if the service counter is currently occupied. |
| **4. serviceCusServ** | Service | Transaction/Order | Represents the time taken to process a customer's request. |
| **5. splitToPackages** | Split | Order Fulfillment | **Communication Hub:** Converts 1 Customer into $N$ Packages. The customer proceeds to exit, while the packages enter the warehouse logic. |
| **6. toCustomerExit** | MoveTo | Walking to Exit | Customer moves toward the exit after their order is "placed." |
| **7. sinkCustomer** | Sink | Customer Departure | Removes the customer entity from the simulation. |

### **Phase B: Internal Handling & Packaging**

| Block | Type | Reality Equivalent | Logic Function |
| --- | --- | --- | --- |
| **8. seizeMLForMove** | Seize | Calling a Worker | Requests an available Manual Laborer to handle the new packages. |
| **9. moveToPackagingArea** | MoveTo | Transport to Prep Area | Worker carries the raw items to the packaging station. |
| **10. releaseMLForMove** | Release | Task Completion | The worker is freed to perform other tasks while packaging happens. |
| **11. seizMLForPackaging** | Seize | Assigning Packager | Assigns a worker to stay with the package during the boxing process. |
| **12. packagingProcess** | Delay | Boxing/Labeling | A time delay representing the physical task of preparing the box. |
| **13. releaseMLForPackaging** | Release | Task Completion | Worker is released after the package is ready for storage. |

### **Phase C: Storage and Outbound Loading**

| Block | Type | Reality Equivalent | Logic Function |
| --- | --- | --- | --- |
| **14. seizeMLForStorage** | Seize | Calling a Stocker | Worker picks up the finished box for floor storage. |
| **15. moveToStorage** | MoveTo | Walking to Zones | Moves the package to one of the 6 designated storage zones. |
| **16. storageCongestionDelay** | Delay | Disorganization Factor | Simulates the time spent finding a spot in a "disorganized" floor layout. |
| **17. releaseMLForStorage** | Release | Task Completion | Worker returns to the pool; package is now "inventory." |
| **18. waitReadyForLoading** | **Wait** | **Inventory Wait** | **Communication Hub:** Packages sit here until a Truck signals it is ready to receive them (The Handshake). |
| **19. seizeMLForLoading** | Seize | Calling a Loader | Worker picks up a "reserved" package from the storage zone. |
| **20. storageCongestionDelay2** | Delay | Retrieval Time | Simulates the difficulty of finding/reaching a specific box in a full zone. |
| **21. moveToTruck** | MoveTo | Walking to Dock | Worker carries the package from the zone to the parked truck. |
| **22. releaseMLForLoading** | Release | Task Completion | Worker is freed; the package is now physically "loaded." |
| **23. sinkPackages** | Sink | Shipment | Updates the Truck's `physicalLoadVolume` and removes the package from simulation. |

---

## **II. Logic View: Trucks**

This flow represents the "Outbound Logistics" phase. It is a "Pull" system that reacts to the total volume stored in the warehouse.

| Block | Type | Reality Equivalent | Logic Function |
| --- | --- | --- | --- |
| **1. sourceTrucks** | Source | Truck Arrival | Triggered only when warehouse volume hits **75%**. |
| **2. seizeDock** | Seize | Parking Reservation | Reserves one of the 2 available dock slots (Resources). |
| **3. moveToDock** | MoveTo | Driving to Slot | The truck maneuvers into the specific reserved dock node. |
| **4. waitAtDock** | **Wait** | **Loading Bay Wait** | **Communication Hub:** The truck stays here until it is physically full (signaled by `loadAndSink`). |
| **5. releaseDock** | Release | Vacating Slot | Frees the dock resource for the next potential truck. |
| **6. moveToExit** | MoveTo | Driving Away | The full truck drives to the `truckEntryExit` point. |
| **7. sink** | Sink | Delivery Departure | Removes the truck and logs the final shipment data. |

---

## **III. Communication and Synchronization**

The most sophisticated part of your model is how these two independent flows "talk" to each other without physical connections:

1. **The Trigger (Packages $\rightarrow$ Trucks):** As packages enter storage (Step 17), the code checks `getTotalStoredVolume()`. If it hits 75%, it calls `sourceTrucks.inject(1)`.
2. **The Handshake (Trucks $\rightarrow$ Packages):** When a truck arrives at `waitAtDock` (Truck Step 4), it triggers the `checkAndTriggerLoading()` function. This function scans `waitReadyForLoading` (Package Step 18) and "frees" the packages that fit the truck's capacity.
3. **The Completion (Packages $\rightarrow$ Trucks):** As each package hits `sinkPackages` (Package Step 23), it increments the truck's `physicalLoadVolume`. Once the truck is full, the package logic calls `waitAtDock.free(truck)`, allowing the truck to finally leave.

This guide is designed for the **Experimentation Phase** of your MPCR project. By adjusting these parameters, you are performing **Sensitivity Analysis**—determining which "knob" has the most significant impact on your warehouse's performance.

---

## **IV. Parameters for Simulating Different Scenarios**

### **1. customerArrivalSchedule (Arrival Rate)**

* **How to Change it:** * **Baseline:** Open the `customerArrivalSchedule` object and edit the **Value** column in the table.

* **Simulated Effect:** This controls the **System Load**.
* **Impact:** Increasing this value will increase the rate of sustomer arrival, and in turn, the number of packages.

### **2. cusSerWorkSchedule (CS Employee Count)**

* **How to Change it:** * **Baseline:** Open the `cusSerWorkSchedule` object and edit the **Value** column in the table.
* **Impact:** This is the number of customer service employees.

### **3. manLabWorkSchedule (Manual Labor Count)**

* **How to Change it:** * **Baseline:** Open the `cusSerWorkSchedule` object and edit the **Value** column in the table.
* **Impact:** This is the most critical parameter. It's the number of Manual Labor Employees. Increasing this makes all the Statistical Times much faster.

### **4. storageDelayTime (Disorganization Multiplier)**

* **How to Change it:** * Edit the Default Value. This is in minutes.
* **Impact:** This simulates a disorganized floor. Higher values increase the time workers spend searching for items, effectively lowering their productivity even if the labor count remains the same. 

### **5. maxTrucks (Daily Dispatch Limit)**

* **How to Change it:** * Edit the default value.
* **Impact:** This controls how many trucks can arrive in one day. If this value is low, then packages will pile up more inside the warehouse.