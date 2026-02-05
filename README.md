# NYAYA MITRA 🏛️
## Voice-First AI Legal Intelligence System


[![AWS](https://img.shields.io/badge/AWS-Cloud%20Native-orange)](https://aws.amazon.com/)
[![AI/ML](https://img.shields.io/badge/AI%2FML-Bedrock%20%2B%20SageMaker-blue)](https://aws.amazon.com/bedrock/)
[![Voice-First](https://img.shields.io/badge/Interface-Voice%20First-green)](https://aws.amazon.com/connect/)
[![Languages](https://img.shields.io/badge/Languages-22%2B%20Indian-red)](https://aws.amazon.com/transcribe/)

---

## 🚨 The Problem We're Solving

**67% of Indians who fight legal battles end up poorer than before filing - even when they WIN.**

- **73%** of rural Indians never access legal aid despite legitimate grievances
- **₹50,000+ crore** lost annually in wages, land rights, and benefits
- Families spend **60-80%** of claim value just fighting cases
- **Language barriers**: Courts use English/Hindi, villages speak 700+ dialects
- **Hidden costs**: No way to calculate true cost-to-justice before filing

### Real Story
*"When I was 15, my family entered a land dispute. Half the land had patta, half was poramboke our ancestors used for 40 years. A neighbor claimed it based on an oral promise. We didn't know our rights. We spent ₹1.2 lakhs over 2 years. We're still fighting."*

---

## 💡 Our Solution

**NYAYA MITRA** is a voice-first AI legal intelligence system that **prevents justice debt traps** by:

### 🎯 Core Innovation: Justice Debt Trap Prevention
```
Before: Family fights ₹4.5L land case → Spends ₹3.2L → Wins but goes bankrupt
After: AI calculates costs → Recommends mediation → Saves ₹2.9L → Family keeps land + money
```

### 🔥 Key Features

#### 1. **Cost-to-Justice Calculator**
- Predicts total litigation costs before filing
- Compares mediation vs court expenses
- Shows expected value: *"You'll likely lose ₹2L even if you win"*

#### 2. **Voice-First Interface**
- Works on feature phones with 2G networks
- Supports 22+ Indian languages and dialects
- Natural conversation: *"Mere paas zameen ka jhagda hai..."*

#### 3. **Land Dispute Diagnostics**
- Analyzes evidence strength (1-10 score)
- Counters oral promise claims with legal precedents
- Guides poramboke land rights claims

#### 4. **Smart Path Recommendations**
- AI recommends: Mediation → Administrative → Court (in order of cost-effectiveness)
- Shows district-wise success rates
- Generates timeline estimates

#### 5. **Offline-First Architecture**
- Works at gram panchayats without internet
- Edge computing with local legal knowledge cache
- Syncs when connectivity available

---

## 🏗️ Architecture Overview

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

### 🛠️ Tech Stack
- **AI/ML**: Amazon Bedrock (Claude 3.5), SageMaker (XGBoost, Random Forest)
- **Voice**: Amazon Connect, Transcribe, Polly
- **Data**: DynamoDB, RDS PostgreSQL, S3
- **Compute**: Lambda (serverless), IoT Greengrass (edge)
- **Region**: Primary ap-south-1 (Mumbai), Backup ap-southeast-1 (Singapore)

---

## 📊 Impact & Metrics

### 🎯 Target Impact
- **₹10+ crore** saved in legal costs annually
- **70%+** cases resolved through mediation
- **100,000+** families helped in first year
- **4.5+ stars** user satisfaction

### 💰 Cost Efficiency
- **₹1.80 per user** interaction cost
- **₹90,000/month** for 50,000 users
- **91% cost savings** vs traditional litigation

### 📈 Success Metrics
- Voice processing: **<3 seconds** response time
- System availability: **99.5%** uptime
- Legal accuracy: **95%+** precedent matching
- User retention: **70%+** monthly active users

---

## 🚀 Getting Started

### Prerequisites
- AWS Account with appropriate permissions
- Node.js 18+ and Python 3.9+
- AWS CLI configured
- AWS CDK installed

### Quick Setup (Hackathon Demo)
```bash
# Clone the repository
git clone https://github.com/your-org/nyaya-mitra.git
cd nyaya-mitra

# Install dependencies
npm install
pip install -r requirements.txt

# Deploy infrastructure
cdk deploy --all

# Configure Connect instance
aws connect create-instance --identity-management-type CONNECT_MANAGED

# Test voice interface
curl -X POST https://api-gateway-url/voice/test
```

### Environment Variables
```bash
export AWS_REGION=ap-south-1
export BEDROCK_MODEL_ID=anthropic.claude-3-5-sonnet-20241022-v2:0
export CONNECT_INSTANCE_ID=your-connect-instance-id
export DYNAMODB_TABLE_NAME=nyaya-mitra-cases
```

---

## 📁 Project Structure

```
nyaya-mitra/
├── README.md                           # This file
├── requirements.md                     # Detailed requirements (100 lines)
├── design.md                          # System design (200 lines)
├── functional-requirements-aws-mapping.md  # FR to AWS services mapping
├── src/
│   ├── lambda/                        # Lambda functions
│   │   ├── voice-processor/           # Voice input/output handler
│   │   ├── cost-calculator/           # ML cost prediction
│   │   └── document-generator/        # Legal document creation
│   ├── ml-models/                     # SageMaker model code
│   │   ├── cost-prediction/           # XGBoost cost model
│   │   └── success-probability/       # Random Forest classifier
│   ├── connect/                       # Amazon Connect flows
│   └── greengrass/                    # Edge computing components
├── infrastructure/                    # AWS CDK code
├── data/                             # Sample legal data
├── docs/                             # Additional documentation
└── tests/                            # Unit and integration tests
```

---

## 🎯 Use Cases

### 1. **Land Dispute Resolution**
```
User: "Mere paas 2 acre zameen hai, neighbor claim kar raha hai"
AI: "Evidence strength: 6/10. Court cost: ₹2.5L. Mediation cost: ₹15K. 
     Recommendation: Try mediation first - 74% success rate in your district."
```

### 2. **Wage Recovery**
```
User: "MGNREGA payment nahi mila 6 months se"
AI: "File complaint with Block Development Officer first. Cost: ₹500. 
     Success rate: 89%. Court filing will cost ₹45K+ and take 2+ years."
```

### 3. **Property Documentation**
```
User: "Grandfather's property, no will, 4 brothers fighting"
AI: "Succession certificate needed. Cost: ₹25K via revenue court. 
     Family settlement deed alternative: ₹5K, 3 months vs 2+ years."
```

---

## 🌍 Deployment Regions

| Region | Purpose | Services |
|--------|---------|----------|
| **ap-south-1 (Mumbai)** | Primary | All services, lowest latency for India |
| **ap-southeast-1 (Singapore)** | Backup | Disaster recovery, cross-region replication |
| **Edge Locations** | Offline Access | 500+ gram panchayats with Greengrass |

---

## 🔒 Security & Compliance

- **End-to-end encryption** for all user data
- **Phone-based OTP** authentication via Cognito
- **Bar Council compliance** - guidance only, no direct legal advice
- **Data localization** - sensitive data stays in India
- **PII protection** - tokenization and automatic deletion

---

## 🤝 Contributing

We welcome contributions! Please see our [Contributing Guidelines](CONTRIBUTING.md).

### Development Workflow
1. Fork the repository
2. Create feature branch: `git checkout -b feature/amazing-feature`
3. Commit changes: `git commit -m 'Add amazing feature'`
4. Push to branch: `git push origin feature/amazing-feature`
5. Open Pull Request

### Code Standards
- Follow AWS Well-Architected Framework principles
- Write unit tests for all Lambda functions
- Use TypeScript for infrastructure code
- Document all API endpoints

---
