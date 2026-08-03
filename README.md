# supply-distribution

Village Water Distribution SCADA System

System Overview

This project simulates a complete, automated Supervisory Control and Data Acquisition system designed for agricultural water management. The primary goal of the system is to efficiently draw water from a municipal source, store it in a central reservoir, and distribute it to four distinct agricultural fields while prioritizing water conservation during emergency outages.

The architecture is divided into two primary subsystems:

The Pump House (Supply)

The Village Center (Distribution)

Physical Flow Dynamics

The system operates on a realistic mass balance model where the total water in the reservoir is constantly calculated based on the difference between active supply and active demand.

Supply Capacity: The intake utilizes four parallel pumps. When active, each pump provides exactly 6 cubic meters per hour. At maximum capacity with all four pumps running, the system can intake 24 cubic meters per hour.

Demand Draw: The village contains four agricultural fields. Under normal operating conditions, a single active field demands exactly 7 cubic meters per hour. If all four fields are watering simultaneously, the total system demand is 28 cubic meters per hour.

Intentional Deficit: Because the absolute maximum demand exceeds the absolute maximum supply, the system operates in a deliberate deficit when running at full capacity, requiring the automated logic to carefully manage the stored reservoir water.

Automated Deficit Control

To maintain efficiency, reduce hardware wear, and prevent overflows, the system does not run all pumps constantly. Instead, it utilizes an automated staging sequence based on the current water level in the reservoir. The system targets a maximum fill level of 90 percent.

High Deficit (Below 66 percent): All 4 pumps operate to maximize intake.

Moderate Deficit (66 to 71 percent): 3 pumps operate; 1 shuts down.

Low Deficit (72 to 77 percent): 2 pumps operate; 2 shut down.

Near Capacity (78 to 89 percent): 1 pump operates to slowly top off the tank.

Full Capacity (90 percent and above): All pumps automatically shut down to prevent overflow.

Emergency Rationing Protocol

The core conservation feature of this system is its automated response to a municipal water source outage. If the main intake supply is cut off, the system shifts from standard distribution to strict preservation.

Rationing Phase: If an outage occurs while the reservoir holds more than 30 percent of its capacity, the system automatically restricts agricultural water usage. The flow rate to any active field is immediately choked down from the standard 7 cubic meters per hour to a survival rate of 2 cubic meters per hour.

Critical Halt: If the reservoir level drops to exactly 30 percent during an ongoing outage, the system initiates a hard stop. All distribution to the fields is cut off entirely to preserve the remaining water for critical village infrastructure, and a master emergency alarm is broadcasted to the operators.

Safety Mechanisms and Interlocks

Safety protocols are hardcoded into the system to override the standard automation in the event of hardware failure or necessary maintenance.

Maintenance Overrides: Each individual pump is equipped with a manual isolation valve. If an operator physically closes one of these valves for maintenance, the system immediately forces the corresponding pump to shut down, overriding the automation cycle.

Inlet Emergency Stop: A master kill switch is available at the pump house. Activating this instantly closes all intake lines and shuts down all pumps, regardless of how low the reservoir gets.

Overpressure Burst Protection: The system monitors pipe pressure to prevent catastrophic bursts. If a pump attempts to run against a closed valve, or if it runs while the source is dry, the system trips a high-pressure interlock that immediately mimics the emergency stop protocol to protect the infrastructure.
