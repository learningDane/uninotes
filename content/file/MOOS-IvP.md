"*Mission Oriented Operating Suite*"-"*Interval Programming*" is a open source [[C++]] autonomy framework for marine autonomous vehicles.

**MOOS** is a lightweight middleware: independent programs exchange data through a centrale message server (**MOOSDB**).

**IvP Helm** is the autonomy engine, which combines multiple objectives (BHV: behaviors).

Architecture philosophy used:
1. **backseat driver paradigm**: vehicle control and vehicle autonomy are separated: the autonomy module runs on a separate payload computer (also called mission controller - vehicle controller paradigm). Exactly how the vehicle navigates and implements control is largely unspecified to the autonomy system running in the payload.
2. **publish and subscribe** autonomy middleware: MOOS applications communicate with each other through the MOOSDB in a star topology.
3. **behavior based autonomy**: the IvP Helm is a single MOOS application with distinct software modules called BHV (behaviors) that can be described as self-contained mini expert systems dedicated to a particular aspect of overall vehicle autonomy. When multiple BHV compete for influence over the vehicle the IvP solver is used to reconcile the behaviors.