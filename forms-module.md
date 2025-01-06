---
layout: page
title: Forms for Procurement
---

> At [Airflip](https://www.airflip.com){:target="_blank"} in September 2024, I spearheaded the development of a specialized forms module tailored for procurement teams. This simplified PRD showcases my ability to transform business requirements into an intuitive, user-centric solution.
>

<div style="display: flex; justify-content: left; gap: 150px;">
    <div style="text-align: left; width: 1100px;">
        <img src="/public/images/forms.gif" alt="Forms Module Demo" width="100%"/>
        <p style="margin-bottom: 20px;"></p>
    </div>
</div>

## Problem Statement  

Procurement teams struggled with fragmented data collection and stakeholder management processes for two main workflows: performance reviews and renewals. 

**Performance Reviews:**
A structured process where procurement teams gather multi-stakeholder feedback on supplier performance. Stakeholders independently evaluate suppliers across key metrics like quality, responsiveness, and SLA compliance. This consolidated feedback creates a comprehensive assessment of supplier relationships and helps identify areas for improvement.

**Renewals:**
A dynamic workflow for managing supplier contract renewals that centralizes critical information from multiple sources. This includes tracking contract terms, maintaining updated contact information, and collecting stakeholder inputs throughout the contract lifecycle. The process ensures all relevant data is readily available when making renewal decisions.

## Pain Points

Traditional tools failed to address these workflows in a few ways:

**Fragmented Processes & Manual Work:** Teams relied heavily on spreadsheets and disconnected systems to manage vendor submissions and feedback. This resulted in:

- Constant data transfer between systems
- Increased risk of errors
- Time wasted on repetitive tasks
- Inconsistent data across platforms

**Limited Customization:** Generic form builders couldn't accommodate procurement-specific needs, lacking:

- Specialized field types for procurement data
- Dynamic calculations for contract terms
- Real-time integration with deal profiles (Airflip entities that track deal progress)
- Complex conditional logic for filling, hiding, requiring certain fields.

## Key Features  

### 1. Flexible Workflows for Creating and Assigning Forms   

<a href="/public/images/formsSpec.png" target="_blank">
  <img src="/public/images/formsSpec.png" alt="Forms Module Spec" style="max-width: 100%; cursor: pointer;">
</a> 
 
- **Bi-directional Record Linking**:
Forms feature bi-directional data connections with Deal and Supplier entities - Deals represent individual negotiations (Salesforce may have 3 active deals ongoing), while Suppliers represent consolidated vendor information (all associated supplier information for active and past vendors).
>Example: When creating a supplier performance review form, imagine a "Supplier Contact Information" field. Instead of manually typing in the supplier's email and phone number, the field automatically populates with current contact details from the linked Supplier record (e.g., pulling in "sarah.jones@abc.com" and "555-0123" from ABC Corp's supplier profile). If the user updates this contact information while filling out the form, the submission will also update the master supplier record, ensuring all future forms have the correct contact details.
>

- **Single & Multi-Submission Forms:**   

  **Multi-Submission Forms:** Used for collecting independent feedback, such as supplier performance reviews.  
  > Example: Users in operations, legal, and finance each provide a numeric rating and justification for DocuSign. Procurement reviews each of these submissions to understand DocuSign's performance.  
  >

  **Single-Submission Forms:** Collaborative workflows where inputs from various stakeholders are consolidated into one submission, such as for contract renewals.  
  > Example: A renewal form gathers contract updates and approval justifications into a single document for procurement to review the DocuSign renewal.  
  >

### 2. Customizable Data Model

<a href="/public/images/formsUI.png" target="_blank">
  <img src="/public/images/formsUI.png" alt="Forms Module UI" style="max-width: 50%; cursor: pointer;">
</a>

- **Dynamic Layouts:**  
  Customizable form sections and field types (e.g., text, dropdowns, dates, people) to match procurement needs.  
  > Example: Fields like 'People' and 'Suppliers' can sync with Airflip’s supplier directory and existing HRIS integration to provide autocomplete suggestions. 

- **Integrated Data:**  
  Each field can be configured to either pull live data from an Airflip entity (e.g., a supplier or deal) or update an entity with new information provided by the user upon form submission.  
  > Example: A renewal form can display the current contact information for a supplier, allow the user to update it, and automatically save the changes to the supplier's record. The updated contact information will then appear correctly in future forms.


### 3. Rules Engine for Automation  

<a href="/public/images/rules.png" target="_blank">
  <img src="/public/images/rules.png" alt="Forms Module UI" style="max-width: 80%; cursor: pointer;">
</a>

- **No-Code Rule Builder:** Easily define conditional logic and drag and drop rules to define rule hierarchies. Have the ability to preview rules in real-time.

- **Automation Features:**  
  - Show or hide fields based on user input.  
  - Require fields to be filled.  
  - Perform calculations automatically.  
  - Enforce validation to prevent errors.  
> Example: In a supplier evaluation form, if the user selects "Poor Performance" as a rating, additional fields appear to provide details on specific issues. If "Excellent Performance" is selected, those fields remain hidden to keep the form concise.
>




