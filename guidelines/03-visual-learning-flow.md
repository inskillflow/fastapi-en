> [!TIP]
> **Figure 1 — Global Learning Flow**  
> Shows the complete progression from FastAPI fundamentals to the final project transition.

```mermaid
flowchart TD
    A["Understand FastAPI"] --> B["Study a Simple Example"]
    B --> C["Read the Main Document"]
    C --> D["Learn API Testing"]
    D --> E["Practice with Quiz"]
    E --> F["Understand main.py"]
    F --> G["Build Your Own API"]
    G --> H["Build the Front-End"]
    H --> I["Continue to Iris AI Platform"]
````

> [!TIP]
> **Figure 2 — Recommended Mindset**
> Summarizes the ideal working approach: read, understand, analyze, adapt, build, test, and deliver.

```mermaid id="028z78"
flowchart TD
    A["Read"] --> B["Understand"]
    B --> C["Analyze"]
    C --> D["Reuse Patterns"]
    D --> E["Adapt"]
    E --> F["Build"]
    F --> G["Test"]
    G --> H["Deliver"]
```

> [!TIP]
> **Figure 3 — Core Idea of FastAPI**
> Illustrates how FastAPI receives a request, validates data, executes logic, and returns a JSON response while generating Swagger documentation.

```mermaid id="gxbs8u"
flowchart TD
    A["Client Request"] --> B["FastAPI Endpoint"]
    B --> C["Validation with Pydantic"]
    C --> D["Business Logic"]
    D --> E["JSON Response"]
    B --> F["Swagger UI Documentation"]
```

> [!TIP]
> **Figure 4 — Simple Example Architecture**
> Presents the structure of the calculator example and the relationship between the client, Swagger UI, endpoints, and responses.

```mermaid id="aqrfdm"
flowchart TD
    A["Browser / Client"] --> B["Swagger UI"]
    B --> C["FastAPI Application"]
    C --> D["GET /add"]
    C --> E["GET /subtract"]
    C --> F["GET /multiply"]
    C --> G["GET /divide"]
    D --> H["JSON Response"]
    E --> H
    F --> H
    G --> H
```

> [!TIP]
> **Figure 5 — From Theory to Practice**
> Shows the progression from conceptual understanding to implementation and hands-on project work.

```mermaid id="xfmy2v"
flowchart TD
    A["Concepts"] --> B["FastAPI Structure"]
    B --> C["Endpoints"]
    C --> D["Validation"]
    D --> E["Testing"]
    E --> F["Hands-on Project"]
```

> [!TIP]
> **Figure 6 — Swagger UI Testing Flow**
> Describes the step-by-step process for testing an endpoint directly from the Swagger interface.

```mermaid id="pd6isn"
flowchart TD
    A["Open /docs"] --> B["Select an Endpoint"]
    B --> C["Click Try it out"]
    C --> D["Enter Parameters"]
    D --> E["Execute Request"]
    E --> F["Inspect JSON Response"]
    F --> G["Validate Behavior"]
```

> [!TIP]
> **Figure 7 — API Testing Ecosystem**
> Compares the main testing options available for interacting with a FastAPI application.

```mermaid id="s6c77l"
flowchart TD
    A["FastAPI API"] --> B["Swagger UI"]
    A --> C["REST Client"]
    A --> D["curl"]
    A --> E["Postman"]
    B --> F["Manual Testing"]
    C --> F
    D --> F
    E --> F
```

> [!TIP]
> **Figure 8 — Internal Structure of a FastAPI App**
> Highlights the main building blocks of a FastAPI project, including routes, models, validation, and business logic.

```mermaid id="pqi2tj"
flowchart TD
    A["main.py"] --> B["FastAPI App Instance"]
    A --> C["Routes / Endpoints"]
    A --> D["Pydantic Models"]
    A --> E["Business Logic"]
    C --> F["Incoming Requests"]
    D --> G["Validation"]
    E --> H["Processed Response"]
```

> [!TIP]
> **Figure 9 — Build Strategy**
> Explains a practical strategy for creating a personal API by adapting the demo project instead of starting from zero.

```mermaid id="6fyxky"
flowchart TD
    A["Study Demo Project"] --> B["Choose New Domain"]
    B --> C["Rename Resources"]
    C --> D["Adjust Endpoints"]
    D --> E["Implement Logic"]
    E --> F["Test Your API"]
```

> [!TIP]
> **Figure 10 — Front-End / Back-End Interaction**
> Shows how the user, front-end, and FastAPI backend communicate during a typical request-response cycle.

```mermaid id="ml8j2l"
sequenceDiagram
    participant U as User
    participant F as Front-End
    participant A as FastAPI API

    U->>F: Enter data / click action
    F->>A: Send HTTP request
    A->>A: Validate and process
    A-->>F: Return JSON response
    F-->>U: Display result
```

> [!TIP]
> **Figure 11 — Full Stack Progression**
> Summarizes the path from a completed backend to a connected, tested, and refined front-end.

```mermaid id="9jl5tv"
flowchart TD
    A["Backend Ready"] --> B["Analyze Demo Front-End"]
    B --> C["Design Your Front-End"]
    C --> D["Connect to API"]
    D --> E["Test End-to-End"]
    E --> F["Refine and Deliver"]
```

> [!TIP]
> **Figure 12 — Evaluation Flow**
> Presents the order of the three evaluations and the transition to the next project.

```mermaid id="h7j0o0"
flowchart TD
    A["Evaluation 1<br/>Quiz on API Testing"] --> B["Evaluation 2<br/>Build Your Own API"]
    B --> C["Evaluation 3<br/>Build the Front-End"]
    C --> D["Next Project<br/>Iris AI Platform"]
```

> [!TIP]
> **Figure 13 — Evaluation Logic**
> Explains how the evaluations move from knowledge verification to backend implementation and then to full project readiness.

```mermaid id="knv3qv"
flowchart TD
    A["Knowledge Check"] --> B["Backend Implementation"]
    B --> C["Front-End Development"]
    C --> D["Larger Project Readiness"]
```

> [!TIP]
> **Figure 14 — FastAPI Learning Journey**
> Visualizes the learner’s progression across foundations, testing, development, and next-stage practice.

```mermaid id="y45ngf"
journey
    title FastAPI Learning Journey
    section Foundations
      Understand FastAPI: 5: Learner
      Review Calculator API: 5: Learner
      Read Main Document: 5: Learner
    section Testing
      Learn Swagger UI Testing: 5: Learner
      Practice with Quiz: 4: Learner
      Review Complete Testing Guide: 5: Learner
    section Development
      Understand main.py: 5: Learner
      Build Own API: 5: Learner
      Build Front-End: 5: Learner
    section Progression
      Move to Iris AI Platform: 5: Learner
```

> [!TIP]
> **Figure 15 — Project Delivery Map**
> Provides a compact summary of the path from foundation to the next complete project.

```mermaid id="m4qe80"
flowchart TD
    A["Foundation"] --> B["Testing Skills"]
    B --> C["Code Understanding"]
    C --> D["Backend Project"]
    D --> E["Front-End Project"]
    E --> F["Next Full Project"]
```
