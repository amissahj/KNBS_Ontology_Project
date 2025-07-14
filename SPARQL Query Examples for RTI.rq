# SPARQL Query Examples for Road Traffic Injury Ontology (RTIO)

This file contains 5 sample SPARQL queries designed to demonstrate the analytical capabilities of the Road Traffic Injury Ontology. These queries showcase different aspects of traffic accident analysis within the Ghana context.

## Prerequisites

Before running these queries, ensure you have:
- Loaded the `RTI_exam_updated10.owl` file into your SPARQL endpoint
- Configured the namespace prefix: `PREFIX rtio: <http://www.example.org/rtio#>`

---

## Query 1: Complete Accident Analysis with All Details

**Purpose**: Get comprehensive information about all traffic accidents including participants, locations, timing, causes, and emergency responses.

```sparql
PREFIX rtio: <http://www.example.org/rtio#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT ?accident ?participant ?participantType ?location ?timing ?cause ?emergencyService ?injury
WHERE {
    ?accident rdf:type rtio:TrafficAccident .
    ?accident rtio:involvesPerson ?participant .
    ?participant rdf:type ?participantType .
    ?accident rtio:occurredAt ?location .
    ?accident rtio:happenedOn ?timing .
    
    OPTIONAL { ?accident rtio:hasCause ?cause }
    OPTIONAL { ?accident rtio:respondedBy ?emergencyService }
    OPTIONAL { ?participant rtio:sustainedInjury ?injury }
    
    FILTER(?participantType = rtio:Driver || ?participantType = rtio:Passenger || ?participantType = rtio:Pedestrian)
}
ORDER BY ?accident ?participant
```

**Expected Results**: Shows all 5 accidents with their participants (Kwame, Yaw, AkuffoAddo, Akosua, Ama, Kojo), locations (Circle, TechJunction, etc.), and timing patterns.

---

## Query 2: High-Risk Location Analysis

**Purpose**: Identify high-risk locations and analyze accident patterns, including urban vs rural distribution and timing correlations.

```sparql
PREFIX rtio: <http://www.example.org/rtio#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>

SELECT ?location ?locationType ?accident ?timing ?participantCount
WHERE {
    ?accident rdf:type rtio:TrafficAccident .
    ?accident rtio:occurredAt ?location .
    ?location rdf:type ?locationType .
    ?accident rtio:happenedOn ?timing .
    
    # Count participants in each accident
    {
        SELECT ?accident (COUNT(?participant) AS ?participantCount) WHERE {
            ?accident rtio:involvesPerson ?participant .
        }
        GROUP BY ?accident
    }
    
    # Filter for high-risk locations or specific location types
    FILTER(?locationType = rtio:HighRiskLocation || 
           ?locationType = rtio:UrbanArea || 
           ?locationType = rtio:RuralArea ||
           ?locationType = rtio:Highway ||
           ?locationType = rtio:Junction)
}
ORDER BY ?locationType ?timing
```

**Expected Results**: Shows distribution between urban areas (Circle, Nkawkaw, TechJunction), rural areas (Ejisu), and highways (TemaMotorway).

---

## Query 3: Emergency Response and Healthcare Analysis

**Purpose**: Analyze emergency response patterns and healthcare facility utilization, including NHIS acceptance and response times.

```sparql
PREFIX rtio: <http://www.example.org/rtio#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>

SELECT ?accident ?emergencyService ?patient ?healthFacility ?facilityType ?acceptsNHIS ?responseTime
WHERE {
    ?accident rdf:type rtio:TrafficAccident .
    ?accident rtio:involvesPerson ?patient .
    
    OPTIONAL { 
        ?accident rtio:respondedBy ?emergencyService .
        ?emergencyService rdf:type ?serviceType .
        FILTER(?serviceType = rtio:GhanaAmbulanceServices || 
               ?serviceType = rtio:MTTD || 
               ?serviceType = rtio:Fire_Department)
    }
    
    OPTIONAL { 
        ?patient rtio:treatedAt ?healthFacility .
        ?healthFacility rdf:type ?facilityType .
        FILTER(?facilityType = rtio:GovernmentHospital || 
               ?facilityType = rtio:PrivateHospital || 
               ?facilityType = rtio:FaithBasedHospital)
    }
    
    OPTIONAL { ?healthFacility rtio:acceptsNHIS ?acceptsNHIS }
    OPTIONAL { ?emergencyService rtio:responseTimeMinutes ?responseTime }
}
ORDER BY ?accident
```

**Expected Results**: Shows emergency services (Ghana Ambulance, MTTD, Fire Department) and healthcare facilities (KATH, Nyaho, HolyFamily, StDominic) with NHIS acceptance status.

---

## Query 4: Injury Severity and Treatment Priority Analysis

**Purpose**: Classify injuries by severity and identify patients requiring immediate care, correlating with vehicle types and participant roles.

```sparql
PREFIX rtio: <http://www.example.org/rtio#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>

SELECT ?patient ?participantType ?injury ?injuryType ?severity ?requiresImmediate ?vehicle ?vehicleType ?accident
WHERE {
    ?patient rtio:sustainedInjury ?injury .
    ?injury rdf:type ?injuryType .
    ?patient rdf:type ?participantType .
    ?accident rtio:involvesPerson ?patient .
    
    # Get injury severity information
    OPTIONAL { ?injury rtio:hasSeverity ?severity }
    OPTIONAL { ?injury rtio:requiresImmediateCare ?requiresImmediate }
    
    # Get vehicle information for drivers
    OPTIONAL { 
        ?patient rtio:operatesVehicle ?vehicle .
        ?vehicle rdf:type ?vehicleType .
    }
    
    # Filter for specific injury types
    FILTER(?injuryType = rtio:HeadInjury_Severe || 
           ?injuryType = rtio:Fracture_Severe || 
           ?injuryType = rtio:InternalInjury_Critical ||
           ?injuryType = rtio:InternalInjury_Moderate ||
           ?injuryType = rtio:Laceration_Deep ||
           ?injuryType = rtio:Laceration_Shallow)
}
ORDER BY DESC(?requiresImmediate) ?severity
```

**Expected Results**: Prioritizes severe injuries requiring immediate care and correlates with vehicle types (CarA, Bus1, Truck1, Bike1, Bicycle1).

---

## Query 5: Seasonal and Environmental Context Analysis

**Purpose**: Analyze accident patterns in relation to seasonal factors, visibility conditions, and environmental contexts specific to Ghana.

```sparql
PREFIX rtio: <http://www.example.org/rtio#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>

SELECT ?accident ?timing ?timingType ?context ?contextType ?location ?cause ?visibility
WHERE {
    ?accident rdf:type rtio:TrafficAccident .
    ?accident rtio:happenedOn ?timing .
    ?timing rdf:type ?timingType .
    ?accident rtio:occurredAt ?location .
    
    # Seasonal and environmental context
    OPTIONAL { 
        ?accident rtio:hasContext ?context .
        ?context rdf:type ?contextType .
        FILTER(?contextType = rtio:Mdry_DustHaze_Context || 
               ?contextType = rtio:Mdry_PoorVisibility_Context ||
               ?contextType = rtio:Rainy_Pothole_Context)
    }
    
    # Causal factors
    OPTIONAL { 
        ?accident rtio:hasCause ?cause .
        ?cause rdf:type ?causeType .
        FILTER(?causeType = rtio:DrunkDriving || 
               ?causeType = rtio:Speeding || 
               ?causeType = rtio:RecklessDriving ||
               ?causeType = rtio:BrakeFailure)
    }
    
    # Visibility conditions
    OPTIONAL { 
        ?accident rtio:hasVisibilityCondition ?visibility .
        ?visibility rdf:type ?visibilityType .
        FILTER(?visibilityType = rtio:PoorVisibility || 
               ?visibilityType = rtio:DustHaze)
    }
    
    # Filter for specific timing patterns
    FILTER(?timingType = rtio:MorningRush || 
           ?timingType = rtio:Midday || 
           ?timingType = rtio:NightDriving)
}
ORDER BY ?timingType ?contextType
```

**Expected Results**: Shows correlation between timing (MorningRush, Midday, NightDriving), seasonal contexts (dry season dust haze, rainy season potholes), and accident causes.

---
## Expected Data Coverage

These queries work with the sample data in the ontology:
- **5 accidents** at different locations and times
- **6 people** with different roles (drivers, passengers, pedestrian)
- **5 vehicles** of different types
- **Multiple healthcare facilities** and emergency services
- **Seasonal contexts** for Ghana's climate patterns

---

*For more complex analysis or custom queries, refer to the ontology structure in Protégé or contact the maintainers.*