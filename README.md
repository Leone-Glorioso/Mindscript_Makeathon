# Insurance Company AI Assistant

## Table of Contents
- [Introduction](#introduction)
- [Team](#team)
- [Problem Statement](#problem-statement)
- [Requirements](#requirements)
- [Implementation Overview](#implementation-overview)
- [Operation Modes](#operation-modes)
  - [Analyst Mode](#analyst-mode)
  - [Prosecutor Mode](#prosecutor-mode)
  - [Secretary Mode](#secretary-mode)
- [Data Format](#data-format)
- [Chatbot Behavior Guidelines](#chatbot-behavior-guidelines)
- [Special Conditions](#special-conditions)
- [Technical Details](#technical-details)
- [Evaluation Metrics](#evaluation-metrics)

## Introduction
Insurance Company AI Assistant is a Gradio-based chatbot prototype developed during the Makeathon Hackathon. Hosted in a Kaggle Notebook and powered by the Llama 3.1 model, it automates and streamlines customer interactions for emergency situations related to Accident Care (AC) and Road Assistance (RA).

## Team
- Konstantinos Leontiadis
- Aikaterina Minadaki
- Maria Evangelia Mara
- Stella Soundia

## Problem Statement
The chatbot must collect and process critical information via dialogue with the customer, including:
- License plate number
- Customer full name
- Detailed description of the incident
- Exact incident location
- Final destination for the vehicle if immobile

### Challenge Levels
- **Level 1**: Focus on extracting essential information.
- **Level 2**: Handle explicit conditional logic (e.g., out-of-county processes).

## Requirements
1. Extract core details:
   - Full Name
   - Category of request (AC or RA)
   - Customer intent (e.g., call road assistance, report accident)
   - Precise geo-location of the incident
2. Maintain a respectful, clear, and customer-centric tone.
3. Return only the chatbot’s message to the client—no extra metadata.
4. Avoid repeating already-provided information; ask clarifying questions only if data conflicts.
5. Limit dialogue turns to 5–7 messages unless critical information is missing.
6. Diagnose vehicle issues using common automotive knowledge when customers describe symptoms.

## Implementation Overview
- **Vehicle Issue Detection**: Recognize potential malfunctions.
- **Troubleshooting Suggestions**: Offer quick fixes when possible.
- **Recommended Workshops**: Suggest a nearby garage, and respect customer choices.
- **Geographic Logic**: Trigger alternate workflows for out-of-county destinations.

## Operation Modes

### Analyst Mode
- Classify incoming requests as AC (Accident Care), RA (Road Assistance), or Other.
- Extract and validate essential fields:
  - License plate
  - Name
  - Description
  - Location
  - Final destination

### Prosecutor Mode
- Detect special cases:
  - **Delay compensation**: Issue a coupon if wait time > 1 hour.
  - **Geolocation links**: Provide map links for unclear addresses.
  - **Automated declarations**: Generate forms for exceptional scenarios.
- **Fraud detection**: Flag inconsistent or suspicious cases (e.g., claim soon after policy start) and escalate to human agents.

### Secretary Mode
- Summarize each case in 50–120 words, including:
  - Quality of communication
  - Key extracted details
  - Concise summary of the incident

## Data Format
Inputs are parsed from JSON:
```json
{
  "name": "Alice Chen",
  "category": "car_broke_down",
  "description": "Car stopped on Main Street due to engine overheating.",
  "location": "Main Street 123, Cityville",
  "final_destination": "Nearest Service Center"
}
```

## Chatbot Behavior Guidelines
- **Respect & Clarity**: Always be polite and concise.
- **Single Responsibility**: Only send the crafted message to the customer.
- **No Redundancy**: Do not echo previous inputs unless clarifying conflicts.
- **Precision over Probing**: Ask minimal follow-up questions needed for decision-making.
- **Safety First**: Prioritize customer safety in all suggestions.
- **Dialogue Length**: Keep conversations within 5–7 exchanges.

## Special Conditions
- **Delay Coupons**: Automatically tag requests exceeding 1 hr wait for a €50 e-Mood discount code.
- **Fraud Tags**: Label cases with potential fraud signs and notify the customer that a human agent will follow up.

## Technical Details
- **Core Model**: Llama 3.1, fine-tuned on domain-specific dialogues.
- **Secondary Classifier**: DistilBERT for offline case categorization (20 epochs).
- **Frontend**: Gradio interface in a Kaggle Notebook.
- **Mapping Services**: OpenStreetMap for geocoding; Mapbox for proximity searches.
- **Real-time Refresh**: Live chat updates without manual reloads.

## Evaluation Metrics
- **Information Extraction Accuracy**: % of correctly extracted fields.
- **Response Latency**: Average time to respond (< 2 seconds).
- **User Satisfaction**: Qualitative feedback scores.
- **Conversation Efficiency**: Avg. dialogue turns per resolved case.
