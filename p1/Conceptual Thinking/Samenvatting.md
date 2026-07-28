
# Summary of Conceptual Thinking & OOAD PowerPoints

## **Introduction to Conceptual Thinking & OOAD (Week 1)**
**File:** `CT_W01_02a_Inleiding in concepten.pptx`

* **Conceptual Thinking:** Focuses on understanding user needs and solving problems before coding. It involves identifying the "What," "Who," and "Why" of a product.
* **SDLC (Software Development Life Cycle):** The structured process of software creation.
    * **Phases:** Analysis (Requirements), Design (UML/Architecture), Implementation (Coding), Testing, Deployment, and Maintenance.
    * **Models:** Waterfall (Sequential), Agile (Iterative/Flexible), V-Model, Spiral.
* **OOAD (Object-Oriented Analysis & Design):**
    * **Analysis:** Modeling the problem domain (real-world entities).
    * **Design:** Modeling the technical solution.
    * **Objects:** Entities with **Identity**, **State** (Attributes), and **Behavior** (Methods/Operations).
* **UML (Unified Modeling Language):** A standard visual language for documenting software systems.

---

## **Functional Analysis (Weeks 2 & 3)**
**Files:** `CT - W02.1 - Slides - Functional Analysis (deel 1).pptx`, `CT - W03.1 - Slides - Functional Analysis (deel 2).pptx`

### **Requirements Engineering**
* **Functional Requirements:** What the system must *do* (behavior/features).
* **Non-functional Requirements:** How the system performs (quality standards). Structured using the **FURPS** model:
    * **F**unctionality (Capabilities)
    * **U**sability (UX, consistency)
    * **R**eliability (Availability, uptime)
    * **P**erformance (Speed, response time)
    * **S**upportability (Maintainability, testability).

### **User Stories & Mapping**
* **User Story:** "As a <role>, I want <goal> so that <benefit>".
* **Story Mapping:** Organizes stories into a narrative flow (backbone) to prioritize releases and visualize the big picture.
* **Wireframes:** Low-fidelity sketches of the user interface to plan layout and interaction.

### **Diagrams**
* **Use Case Diagram:** Visualizes interactions between **Actors** (users/systems) and **Use Cases** (system functions). Includes relationships like `<<include>>` (mandatory) and `<<extend>>` (optional).
* **Activity Diagram:** Models workflows or logic flow. Key elements include Actions, Decisions (branches), Forks/Joins (parallelism), and Swimlanes (responsibility).

---

## **Data Analysis & Domain Modeling (Weeks 4 & 5)**
**Files:** `CT - W04.1 - Slides - Data Analysis (deel 1).pptx`, `CT - W05.1 - Slides - Data Analysis (deel 2).pptx`

### **Domain Modeling**
* **Conceptual Class Diagram (CCD):** Represents real-world concepts (not software classes yet).
* **Process:**
    1.  Identify concepts (nouns) in the problem description.
    2.  Filter out vague terms or simple attributes.
    3.  Define **Attributes** (properties) and **Associations** (relationships between concepts).
* **Multiplicity:** Defines how many instances relate to each other (e.g., 1..*, 0..1).

### **Advanced Modeling**
* **History:** Modeling past data often requires changing multiplicities or adding associations to track historical states.
* **Many-to-Many Associations:** Must be resolved by introducing an **Association Class** or intermediate class to hold specific relationship data.
* **Enumerations:** Classes with a fixed set of constant values.
* **Constraints:** Rules defined in `{braces}` (e.g., `{xor}` for exclusive relationships).

---

## **From Analysis to Design (Week 7)**
**File:** `CT - W07.1 - Slides - From analysis to design.pptx`

* **Transition:** Moving from "What" (Analysis) to "How" (Design).
* **System Sequence Diagram (SSD):**
    * Treats the system as a **Black Box**.
    * Shows interaction between an **Actor** and the **System** for a specific Use Case scenario.
    * Defines **System Events** (input messages) and responses.
* **Operation Contracts (OC):**
    * Describes the detailed effect of a system operation on the Domain Model.
    * Defines **Pre-conditions** (state before operation) and **Post-conditions** (created instances, associations formed, attribute changes).

---

## **Interaction Design: Sequence Diagrams (Week 8)**
**File:** `CT - W08.1 - Slides - Sequence Diagram.pptx`

* **Sequence Diagram (SD):** A white-box view detailing how objects interact internally to fulfill a system operation.
* **Key Elements:**
    * **Lifelines:** Represent object instances.
    * **Messages:** Synchronous (solid arrow), Asynchronous (open arrow), Reply (dashed).
    * **Activation Bars:** Show when an object is active/processing.
    * **Creation/Destruction:** `<<create>>` and `<<destroy>>` messages.
* **Fragments:** Structured logic within the diagram:
    * `loop` (iteration), `alt` (if/else), `opt` (optional/if), `ref` (reference to another SD).

---

## **Structure Design: Class Diagrams & Principles (Weeks 9, 10, 11)**
**Files:** `CT - W09.1`, `CT - W10.1`, `CT - W11.1`

### **Design Class Diagram (DCD)**
* Evolves the Domain Model into a software specification.
* **Additions:** Visibility (private `-`, public `+`), Method signatures, Data types, Navigability (arrows on associations).
* **Encapsulation:** Using getters/setters and private attributes to protect data.

### **GRASP Patterns (General Responsibility Assignment Software Patterns)**
Guidelines for assigning responsibilities to classes:
1.  **Controller:** Handles system events (e.g., Facade or Session controller).
2.  **Creator:** Who should create object A? (Ideally, the container or recorder of A).
3.  **Information Expert:** Assign responsibility to the class that has the necessary information.
4.  **Low Coupling:** Minimize dependencies between classes to increase maintainability.
5.  **High Cohesion:** Ensure a class has focused, related responsibilities.

### **Advanced Design Concepts**
* **Visibility:** Attribute, Parameter, Local, and Global visibility.
* **Interfaces:** Define contracts without implementation. Classes `implement` interfaces; interfaces `extend` interfaces.
* **Polymorphism**: Handling different types via a common interface or superclass.
* **Liskov Substitution Principle (LSP):** Subclasses must be substitutable for their superclasses. Preconditions cannot be stricter; postconditions cannot be weaker.