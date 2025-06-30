

# KNOWLEDGE BASED SYSTEMS (KNBS) COURSE
- Ontology Project by **John Amissah**
- Student number: **22205995**

# Road Traffic Injury Ontology (RTIO)

A semantic knowledge model for road traffic injuries in Ghana, built using the Epidemiological Person–Place–Time (PPT) concept. 
The ontology captures real-world accident data, injury types, weather conditions, emergency responses, and treatment outcomes for public health and policy research.

Built with:
- OWL 2 (Web Ontology Language)
- Web Ontology Language (.owl) syntax for readability
- Fully compatible with Protégé and SPARQL endpoints

---

#  Project Foundation – The PPT Triad

This ontology is modeled around the **epidemiological triad** of disease causation, adapted for analyzing road traffic injuries:



This ontology models road traffic injuries as a combination of:


### 1. Person
Represents individuals involved in road traffic incidents:
- Driver
- Passenger
- Pedestrian

Each person has properties:
- Name (`rtio:hasName`)
- Age (`rtio:hasAge`)
- Gender (`rtio:hasGender`)
- Occupation (`rtio:hasOccupation`)
- Sustained injury (`rtio:sustainedInjury`)
- Treatment facility (`rtio:treatedAt`)
- Immediate care required (`rtio:requiresImmediateCare`)

### 2. Place
Describes where an incident occurred:
- Urban
- Rural
- Junction
- Roundabout
- Highway

Properties include:
- Location name (`rtio:hasLocationName`)
- High-risk area status (`rtio:isHighRiskArea`)

Real-world locations are modeled:
- Circle
- Ejisu
- Nkawkaw
- TechJunction
- Tema Motorway

### 3. Time
Captures when the accident happened:
- MorningRush
- Midday
- NightDriving

Includes actual time values:
- `rtio:hasActualTime` using `xsd:time` (e.g., `"07:30:00"^^xsd:time`)

### 4. Weather Conditions
Environmental factors influencing road safety:
- DustHaze
- PoorVisibility
- PotholeAfterRain

Grouped under:
- DrySeason
- RainySeason

Linked to injuries via:
- `rtio:associatedInjuryType` → e.g., `DustHaze` → `Fracture_Severe`


---

This ontology project on road traffic injuries was modeled to answer these questions

- Who : Drivers, passengers, pedestrians
- Where : Urban areas, rural zones, highways, junctions
- When : Morning rush, midday, night driving
- Why : Speeding, drunk driving, brake failure, poor visibility
- Under what conditions : Dust haze, pothole after rain, poor visibility
- What injuries occurred : Fracture, head injury, internal injury, laceration (with severity levels)
- How were they treated : Government hospitals, private clinics, faith-based facilities
- Which units responded : MTTD, Ghana Ambulance Services, Fire Department




## Example Use Cases

You can use this ontology to answer questions like:

- Which injuries are most common during DustHaze conditions?
- What time of day sees the most critical injuries?
- Do rainy season potholes increase internal injuries?
- Which hospitals treat severe head injuries most frequently?
- Are urban roads more prone to specific injury types?
-Which emergency units respond to critical injuries?
-Are lacerations more common under poor visibility?
-Which locations are linked to fractures?
-How does time of day affect accident outcomes?
-What is the gender distribution among injured individuals?


All entities are linked to allow meaningful exploration using:
- SPARQL queries
- Visualization tools (Protégé, WebVOWL)

---


## 🛠️ Tools & Standards Used

- OWL 2 (Web Ontology Language)
