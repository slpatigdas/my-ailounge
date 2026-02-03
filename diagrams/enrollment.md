# Enrollment Process / Onboarding

```mermaid
graph TD
    %% Phase 1: Entry Options
    Start([Start: Enrollment Phase]) --> Choice{Enrollment Method}
    
    Choice -->|Option A| Codes[POC provides list of Unique Codes<br/>e.g., Employee IDs]
    Choice -->|Option B| Emails[POC provides list of<br/>Names & Emails]

    %% Phase 2: System Processing
    Codes --> Upload[Admin uploads data to System]
    Emails --> Upload
    
    Upload --> WelcomeEmail[System sends Welcome Email<br/>with Onboarding Link]

    %% Phase 3: User Action
    WelcomeEmail --> UserClick[User clicks link &<br/>redirected to Portal]
    UserClick --> SetPassword[User activates account &<br/>sets Password]
    
    %% Phase 4: Onboarding & Completion
    SetPassword --> Screening[User undergoes Initial<br/>Screening Process]
    Screening --> Dashboard[User gains Dashboard Access<br/>& all features]
    
    Dashboard --> End([Process Complete])

    %% Styling
    style Start fill:#f9f,stroke:#333,stroke-width:2px
    style End fill:#f9f,stroke:#333,stroke-width:2px
    style Choice fill:#fff4dd,stroke:#d4a017,stroke-width:2px
```

## 🌟 Key Highlights of This Enrollment Flow

- **Flexibility at the Start:**  
  Whether the company provides pre-existing IDs or a fresh email list, the **Upload** step unifies the process—making onboarding easy regardless of source data.

- **Security by Design:**  
  Users are prompted to set their own password upon first login, ensuring that unique identifiers (like Employee IDs) aren't the sole means of account protection.

- **Gatekeeping & Controlled Access:**  
  The **Initial Screening** step acts as a safeguard. Even after activating their account, users gain full dashboard access only after completing your specific onboarding requirements.

