# Requirements Document: SwasthyaSetu

## Introduction

SwasthyaSetu is an AI-powered Occupational Health Intelligence and Care Continuity platform designed to address the critical healthcare challenges faced by India's 450+ million internal migrant workers. The platform provides migration-aware health risk prediction, portable health identity, and seamless care continuity across state borders while ensuring ethical AI practices, regulatory compliance, and accessibility for low-literacy, multilingual users.

The system does NOT provide medical diagnosis but offers risk indicators, alerts, and care recommendations to enable early intervention and continuous care coordination.

## Problem Statement

Internal migrant workers in India face severe healthcare discontinuity:
- Medical history is lost when crossing state borders
- Insurance schemes are non-portable across states
- Language barriers prevent effective healthcare communication
- Occupational health risks (silicosis, TB, musculoskeletal disorders, anemia) go untracked
- No care continuity when workers return to source locations
- Occupational diseases develop silently and are detected too late

SwasthyaSetu addresses these challenges through portable health identity, AI-powered health intelligence, and migration-aware care coordination.

## Glossary

- **System**: The SwasthyaSetu platform
- **Worker**: An internal migrant worker who is the primary beneficiary
- **ABHA**: Ayushman Bharat Health Account - India's national health ID
- **ASHA_Worker**: Accredited Social Health Activist - community health worker
- **PHC**: Primary Health Center
- **Source_Location**: The worker's home location before migration
- **Destination_Location**: The location where the worker migrates for work
- **Health_Record**: Digital representation of medical documents (prescriptions, lab reports, diagnoses)
- **Risk_Score**: A numerical indicator of occupational health risk (NOT a diagnosis)
- **Care_Continuity**: Seamless transfer of health information and care coordination across locations
- **Consent_Manager**: Component managing user consent for data access and sharing
- **OCR_Engine**: Optical Character Recognition system for digitizing medical documents
- **Risk_Prediction_Engine**: ML-based system correlating occupation, migration, and health data
- **Voice_Interface**: Speech-to-text and text-to-speech system supporting Indian languages
- **Offline_Mode**: System capability to function without internet connectivity
- **Anonymized_Insights**: Aggregated health data with all personal identifiers removed

## User Personas

### Persona 1: Ramesh - Construction Worker
- Age: 32, from rural Bihar, migrated to Mumbai for construction work
- Low literacy, speaks Hindi and Bhojpuri
- Has smartphone but limited data connectivity
- Suffers from chronic cough (potential silicosis risk)
- Lost all medical records during migration
- Needs: Portable health identity, voice-based interaction, offline access

### Persona 2: Lakshmi - Domestic Worker
- Age: 28, from Odisha, working in Delhi
- Moderate literacy, speaks Odia and basic Hindi
- Pregnant, needs continuous prenatal care
- Insurance from home state not valid in Delhi
- Needs: Care continuity, multilingual support, ASHA coordination

### Persona 3: Dr. Priya - PHC Doctor
- Works at destination PHC treating migrant workers
- Needs complete medical history to provide effective care
- Faces language barriers with patients
- Needs: Quick access to health records, risk indicators, translation support

### Persona 4: Meera - ASHA Worker
- Community health worker at source location
- Coordinates care for returning migrants
- Limited technical skills
- Needs: Simple interface, care handoff information, follow-up alerts

### Persona 5: Public Health Official
- State health department analyst
- Needs aggregated data for policy planning
- Requires privacy-compliant insights
- Needs: Anonymized trends, occupational risk patterns, migration health data

## Requirements

### Requirement 1: Portable Health Identity

**User Story:** As a migrant worker, I want a portable health identity that works across state borders, so that my medical history follows me wherever I go.

#### Acceptance Criteria

1. WHEN a worker registers, THE System SHALL create a unique health identity linked with ABHA
2. WHEN a worker presents their health identity, THE System SHALL retrieve their complete health record within 3 seconds
3. THE System SHALL generate a QR code for offline identity verification
4. WHEN scanning a QR code in offline mode, THE System SHALL display cached health summary
5. WHEN a worker updates their location, THE System SHALL record the migration event with timestamp and location
6. THE System SHALL support identity verification without internet connectivity using QR code validation

### Requirement 2: AI-Powered Document Digitization

**User Story:** As a migrant worker with paper prescriptions and lab reports, I want the system to automatically convert them to digital format, so that I don't lose my medical history.

#### Acceptance Criteria

1. WHEN a worker uploads a photo of a prescription, THE OCR_Engine SHALL extract text with minimum 85% accuracy
2. WHEN a document is in Hindi, Tamil, Telugu, Bengali, Marathi, Gujarati, Kannada, Malayalam, Punjabi, or Odia, THE OCR_Engine SHALL process it correctly
3. WHEN text extraction is complete, THE System SHALL structure the data into standardized health record format
4. WHEN OCR confidence is below 70%, THE System SHALL flag the record for manual review
5. THE System SHALL extract key medical entities (medications, dosages, diagnoses, lab values, dates)
6. WHEN a lab report is digitized, THE System SHALL validate numerical values against normal ranges
7. THE System SHALL preserve the original document image alongside extracted data

### Requirement 3: Migration-Aware Occupational Risk Prediction

**User Story:** As a migrant worker, I want the system to alert me about potential health risks based on my occupation and migration pattern, so that I can seek early medical attention.

#### Acceptance Criteria

1. WHEN a worker registers their occupation type, THE Risk_Prediction_Engine SHALL identify associated occupational hazards
2. WHEN a worker's migration duration exceeds 6 months in high-risk occupation, THE System SHALL generate elevated risk alerts
3. WHEN correlating occupation (construction), destination (urban), and symptoms (chronic cough), THE Risk_Prediction_Engine SHALL calculate silicosis risk score
4. WHEN a risk score exceeds threshold, THE System SHALL generate an alert with recommended actions (NOT a diagnosis)
5. THE Risk_Prediction_Engine SHALL consider occupation type, migration source and destination, duration of migration, environmental exposure, workplace conditions, and health record patterns
6. WHEN generating risk predictions, THE System SHALL provide explainable reasoning for the risk score
7. THE System SHALL update risk scores when new health records are added
8. WHEN a worker has no recent health records for 90 days in high-risk occupation, THE System SHALL generate a health check reminder

### Requirement 4: Voice-First Multilingual Interaction

**User Story:** As a low-literacy migrant worker, I want to interact with the system using voice in my native language, so that I can access healthcare information without reading barriers.

#### Acceptance Criteria

1. THE Voice_Interface SHALL support Hindi, Tamil, Telugu, Bengali, Marathi, Gujarati, Kannada, Malayalam, Punjabi, and Odia
2. WHEN a worker speaks a query, THE System SHALL transcribe it with minimum 80% accuracy
3. WHEN the system responds, THE Voice_Interface SHALL convert text to speech in the worker's selected language
4. WHEN a worker switches language preference, THE System SHALL update all subsequent interactions
5. THE System SHALL provide voice-based navigation for all core features
6. WHEN voice input fails, THE System SHALL provide simple visual fallback options
7. THE Voice_Interface SHALL function in noisy environments with noise cancellation

### Requirement 5: Source-to-Destination Care Continuity

**User Story:** As a migrant worker, I want my healthcare providers at destination to coordinate with providers at my home location, so that my treatment continues seamlessly.

#### Acceptance Criteria

1. WHEN a worker visits a destination PHC, THE System SHALL notify the source ASHA_Worker of the consultation
2. WHEN a worker returns to source location, THE System SHALL provide the source PHC with complete destination health records
3. WHEN a care plan is created at destination, THE System SHALL make it accessible to source healthcare providers with worker consent
4. WHEN a worker requires follow-up care, THE System SHALL generate alerts for the appropriate ASHA_Worker based on current location
5. THE System SHALL maintain a chronological care timeline across all locations
6. WHEN a worker migrates to a new destination, THE System SHALL identify nearby PHCs and ASHA workers
7. THE System SHALL support care handoff notes from one provider to another

### Requirement 6: Privacy-Preserving Consent Management

**User Story:** As a migrant worker, I want complete control over who can access my health data, so that my privacy is protected.

#### Acceptance Criteria

1. WHEN a healthcare provider requests access to health records, THE Consent_Manager SHALL prompt the worker for explicit consent
2. WHEN granting consent, THE System SHALL allow the worker to specify data scope (specific records or time period)
3. WHEN granting consent, THE System SHALL allow the worker to specify duration (one-time, 7 days, 30 days, or ongoing)
4. THE System SHALL log all data access events with timestamp, accessor identity, and data accessed
5. WHEN a worker revokes consent, THE System SHALL immediately block further access by that provider
6. THE System SHALL provide voice-based consent workflows for low-literacy users
7. WHEN consent expires, THE System SHALL automatically revoke access
8. THE System SHALL encrypt all health records at rest and in transit
9. WHEN generating anonymized insights, THE System SHALL ensure no individual can be re-identified

### Requirement 7: Offline-First Capability

**User Story:** As a migrant worker in areas with poor connectivity, I want to access my health information offline, so that I can show it to doctors even without internet.

#### Acceptance Criteria

1. WHEN the device is offline, THE System SHALL display cached health summary and recent records
2. WHEN offline, THE System SHALL allow QR code generation for identity verification
3. WHEN offline, THE System SHALL queue health record uploads for synchronization when connectivity returns
4. WHEN connectivity is restored, THE System SHALL automatically sync queued data within 60 seconds
5. THE System SHALL cache the most recent 50 health records for offline access
6. WHEN offline, THE System SHALL display the last sync timestamp
7. THE System SHALL function in offline mode for core features (view records, generate QR, record symptoms)

### Requirement 8: Aggregated Public Health Insights

**User Story:** As a public health official, I want anonymized aggregated health data about migrant workers, so that I can plan interventions and policies.

#### Acceptance Criteria

1. WHEN generating public health reports, THE System SHALL aggregate data with all personal identifiers removed
2. THE System SHALL provide occupational disease prevalence by occupation type and migration corridor
3. THE System SHALL identify emerging health trends in migrant populations
4. WHEN displaying geographic health patterns, THE System SHALL use district-level or higher aggregation (never individual location)
5. THE System SHALL ensure aggregated datasets contain minimum 100 individuals to prevent re-identification
6. THE System SHALL provide insights on care continuity gaps and healthcare access patterns
7. WHEN exporting anonymized data, THE System SHALL apply differential privacy techniques

### Requirement 9: ABHA Integration and Interoperability

**User Story:** As a system architect, I want SwasthyaSetu to integrate with India's ABHA ecosystem, so that it works seamlessly with national health infrastructure.

#### Acceptance Criteria

1. WHEN a worker has an existing ABHA ID, THE System SHALL link it to their SwasthyaSetu profile
2. WHEN a worker doesn't have ABHA, THE System SHALL facilitate ABHA creation through the registration flow
3. THE System SHALL use ABHA as the primary health identifier for all records
4. THE System SHALL comply with ABDM (Ayushman Bharat Digital Mission) data standards
5. WHEN sharing health records, THE System SHALL use FHIR-compliant formats
6. THE System SHALL support integration with Health Information Exchanges (HIE)
7. THE System SHALL validate ABHA credentials using official ABDM APIs

### Requirement 10: Ethical AI and Explainability

**User Story:** As a migrant worker receiving risk alerts, I want to understand why the system flagged a risk, so that I can make informed decisions about my health.

#### Acceptance Criteria

1. WHEN displaying a risk score, THE System SHALL provide plain-language explanation of contributing factors
2. THE System SHALL clearly label all outputs as "risk indicators" and NOT medical diagnoses
3. WHEN showing risk predictions, THE System SHALL include disclaimer that medical consultation is required
4. THE Risk_Prediction_Engine SHALL avoid bias based on caste, religion, gender, or regional origin
5. THE System SHALL undergo regular bias audits on protected demographic attributes
6. WHEN a risk prediction is made, THE System SHALL log the model version and input features for auditability
7. THE System SHALL provide workers with option to report incorrect or concerning predictions

### Requirement 11: Scalability and Performance

**User Story:** As a system architect, I want the platform to scale to tens of millions of users, so that it can serve India's entire migrant worker population.

#### Acceptance Criteria

1. THE System SHALL support 50 million registered users
2. WHEN concurrent users reach 500,000, THE System SHALL maintain response times under 3 seconds
3. THE System SHALL process 10,000 document digitization requests per hour
4. THE System SHALL handle 1 million risk score calculations per day
5. WHEN system load increases by 50%, THE System SHALL auto-scale compute resources within 5 minutes
6. THE System SHALL maintain 99.5% uptime for core services
7. THE System SHALL support geographic distribution across multiple Indian regions for low latency

### Requirement 12: Security and Compliance

**User Story:** As a compliance officer, I want the system to meet Indian healthcare data regulations, so that we operate legally and protect user privacy.

#### Acceptance Criteria

1. THE System SHALL comply with Digital Personal Data Protection Act (DPDP) 2023
2. THE System SHALL comply with Information Technology Act 2000 and amendments
3. THE System SHALL implement role-based access control for all user types
4. WHEN a security breach is detected, THE System SHALL alert administrators within 60 seconds
5. THE System SHALL conduct automated security scans daily
6. THE System SHALL encrypt all data at rest using AES-256
7. THE System SHALL encrypt all data in transit using TLS 1.3
8. THE System SHALL implement multi-factor authentication for healthcare provider accounts
9. THE System SHALL maintain audit logs for minimum 7 years
10. WHEN a worker requests data deletion, THE System SHALL complete deletion within 30 days while preserving anonymized aggregates

## Non-Functional Requirements

### Performance
- Health record retrieval: < 3 seconds
- OCR processing: < 10 seconds per document
- Risk score calculation: < 5 seconds
- Voice transcription: < 2 seconds for 10-second audio
- Mobile app launch: < 2 seconds

### Availability
- Core services: 99.5% uptime
- Planned maintenance windows: < 4 hours per month
- Disaster recovery: < 4 hours RTO, < 1 hour RPO

### Usability
- Mobile-first design optimized for low-end Android devices
- Support for screen sizes from 4.5" to 6.5"
- Maximum 3 taps to reach any core feature
- Voice commands for all critical workflows
- Works on devices with 2GB RAM and Android 8.0+

### Scalability
- Horizontal scaling for all microservices
- Database sharding by geographic region
- CDN for static assets and cached data
- Auto-scaling based on load metrics

### Maintainability
- Microservices architecture with clear service boundaries
- Comprehensive API documentation
- Automated testing with 80%+ code coverage
- Infrastructure as Code for all deployments
- Centralized logging and monitoring

## Success Metrics

### User Adoption
- 1 million registered workers in first year
- 60% monthly active user rate
- 40% of users complete health profile within first week

### Health Impact
- 30% reduction in time to occupational disease detection
- 50% of high-risk workers receive timely health check reminders
- 70% care continuity rate for workers migrating back to source

### System Performance
- 85%+ OCR accuracy across all supported languages
- 80%+ voice recognition accuracy in noisy environments
- < 3 second average response time for health record retrieval

### Engagement
- Average 4 health records uploaded per active user per year
- 50% of consent requests approved by workers
- 25% of workers use voice interface as primary interaction mode

### Public Health Value
- Anonymized insights used by minimum 5 state health departments
- Identification of 3+ emerging occupational health trends per year
- 80% data completeness for migration health corridors

