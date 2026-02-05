# NYAYA MITRA - System Design
## Voice-First AI Legal Intelligence System

## System Architecture

### High-Level Architecture
```
┌─────────────────────────────────────────────────────────────┐
│           USER INTERFACES                                   │
│  IVR System (Connect) | WhatsApp Bot | Gram Panchayat Kiosks│
└─────────────────────────────────────────────────────────────┘
                              │
┌─────────────────────────────────────────────────────────────┐
│           CORE AI SERVICES                                  │
│  Legal AI (Bedrock) | Cost Calculator (SageMaker) | Voice   │
└─────────────────────────────────────────────────────────────┘
                              │
┌─────────────────────────────────────────────────────────────┐
│           DATA & STORAGE                                    │
│  User Data (DynamoDB) | Legal DB (RDS) | Documents (S3)    │
└─────────────────────────────────────────────────────────────┘
```

**Design Principles:** Voice-first, offline-capable, cost-focused, multi-language, serverless

---

## Essential AWS Services

### Voice & Communication
**Amazon Connect:** Cloud contact center for IVR system
- Handles 1000+ concurrent calls, pay-per-minute pricing (₹2-5/call)
- Built-in Transcribe/Polly integration

**Amazon Transcribe & Polly:** Speech processing
- Indian accent support, 5000+ legal terms vocabulary, 2G-optimized audio

### AI/ML Core
**Amazon Bedrock (Claude 3.5):** Legal reasoning and conversation
- No infrastructure management, pay-per-token, safety guardrails
- Use cases: Evidence analysis, legal document generation, cost prevention

**Amazon SageMaker:** Custom ML models
- Cost Prediction: XGBoost, 85%+ accuracy on 50K cases
- Success Probability: Random Forest, trained on 100K+ outcomes

### Data Storage
**Amazon DynamoDB:** User data and case tracking
- Serverless auto-scaling, millisecond latency, pay-per-request
- Tables: UserCases, CostBenchmarks

**Amazon S3:** Document storage
- Unlimited scale, lifecycle policies, CloudFront integration
- Generated documents, evidence uploads, templates

**Amazon RDS (PostgreSQL):** Legal precedents
- ACID compliance, full-text search, automated backups
- Tables: legal_precedents, cost_benchmarks

### Supporting Services
**AWS Lambda:** Serverless compute (voice-processor, cost-calculator, document-generator)
**Amazon SNS:** SMS notifications for document delivery
**Amazon Cognito:** Phone-based OTP authentication

---

## Data Flow

### User Journey
```
User calls → Connect IVR → Language selection → Voice input → 
Transcribe → Lambda → Bedrock analysis → SageMaker cost calc → 
DynamoDB storage → Polly response → SMS delivery
```

### Cost Calculation Example
```yaml
Input: "Land dispute, Tamil Nadu, oral promise"
Processing:
  - Case type: Land boundary
  - Evidence strength: 3/10 (oral invalid)
  - Claim value: ₹4.5L
Prediction:
  - Total cost: ₹2.47L (lawyer ₹85K + court ₹12K + misc ₹1.5L)
  - Success probability: 35%
  - Expected value: -₹1.9L (likely loss)
Recommendation: MEDIATION (₹15K cost, 70% success rate)
```

---

## Security Design

### Authentication & Data Protection
```yaml
Authentication:
  - Cognito: Phone OTP, role-based access
  - IAM: Service permissions, least privilege

Encryption:
  - At Rest: KMS for all databases
  - In Transit: TLS 1.3 for communications
  - Voice: End-to-end via Connect

Privacy:
  - PII tokenization, 7-year auto-deletion
  - Data masking in non-prod environments
```

### Network Security
- Multi-AZ VPC deployment (ap-south-1a, ap-south-1b)
- Private subnets for databases, security groups with least privilege

---

## Scalability & Performance

### Auto-Scaling
```yaml
Lambda: 1000 concurrent (voice), 500 (cost-calc), 200 (docs)
SageMaker: 1-10 instances, ml.t3.medium
DynamoDB: On-demand billing, DAX caching
```

### Performance Targets
- Voice processing: <3 seconds
- Cost calculation: <2 seconds
- Concurrent users: 10,000+
- System availability: 99.5%

---

## Cost Optimization

### Monthly Estimates (50K users, 200K calls)
```yaml
AWS Services:
  - Lambda: ₹15,000 (10M requests)
  - Connect: ₹25,000 (200K minutes)
  - Bedrock: ₹20,000 (5M tokens)
  - SageMaker: ₹8,000 (endpoints)
  - DynamoDB: ₹12,000 (operations)
  - S3: ₹3,000 (storage)
  - RDS: ₹5,000 (db.t3.medium)
  - SNS: ₹2,000 (SMS)
Total: ₹90,000/month (~₹1.80 per user)
```

### Optimization Strategies
- S3 Intelligent Tiering, lifecycle policies
- Lambda provisioned concurrency only for critical functions
- CloudFront caching, API Gateway 5-minute TTL

---

## Offline Capabilities

### AWS IoT Greengrass at Gram Panchayats
```yaml
Edge Devices: Raspberry Pi 4 (₹8,000 each), 64GB cache
Local Features:
  - Basic cost calculation (cached models)
  - Document templates in local languages
  - Voice processing for common queries
Sync: Daily updates when online, conflict resolution
```

---

## Failure Handling

### High Availability
```yaml
Multi-AZ: RDS primary + 2 replicas, Lambda auto-failover
Error Handling: Circuit breaker, exponential backoff, dead letter queues
Monitoring: CloudWatch (<3s response, <1% errors), SMS/email alerts
```

### Disaster Recovery
- RDS: Daily backups, 7-day retention
- DynamoDB: Point-in-time recovery
- S3: Cross-region replication to Singapore
- RTO: 4 hours, RPO: 1 hour

---

## Deployment Strategy

### CI/CD Pipeline
```yaml
Stages: CodeCommit → CodeBuild → Test → Deploy Dev → Deploy Prod
Tools: AWS CDK (TypeScript), CloudFormation, Parameter Store
Deployment: Blue/Green for zero downtime
```

### Regional Strategy
- **Primary:** ap-south-1 (Mumbai) - lowest latency for India
- **Backup:** ap-southeast-1 (Singapore) - disaster recovery
- **Edge:** CloudFront in Mumbai, Chennai, Delhi, Bangalore
---


*This architecture prevents justice debt traps through AI-powered cost analysis, balancing hackathon constraints with production scalability for India-scale deployment.*