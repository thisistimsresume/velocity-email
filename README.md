# Email Marketing & Automation Work

Source files demonstrating email development and Velocity scripting for dynamic content personalization in Marketo.

## Productivity Benchmark Email

A data-driven email campaign using Velocity scripting to personalize content based on workforce productivity metrics.

### Overview

This email template uses Velocity scripting to generate dynamic, personalized content based on five productivity metrics. Content adapts automatically based on how recipient metrics compare to benchmarks and healthy ranges, providing congratulatory, cautionary, or action-required messaging.

### Key Features

- **Dynamic Content Generation** - Email content changes based on metric thresholds
- **Velocity Token Processing** - Uses Marketo Velocity scripting for personalization
- **Conditional Logic** - 15+ content variations across 5 metrics
- **Color-Coded Messaging** - Green (healthy), Yellow (watch), Red (action needed)
- **Responsive Design** - Mobile-optimized email template

### Metrics & Personalization

The email personalizes content for:
1. **Collaboration Time** - Daily meeting/communication time
2. **Focus Time** - Uninterrupted work periods  
3. **Productive Time** - Total active work time
4. **Screen Time** - Daily computer usage
5. **Workday Span** - Total time between first/last activity

Each metric includes:
- Benchmark comparison
- Healthy range assessment
- Context-appropriate messaging
- Status indicator (Congrats! / Keep an eye on this / This may call for action)

### Technical Implementation

**Velocity Tokens Used:**
- `{{my.replacefirstname}}` - First name personalization
- `{{my.replacecompany}}` - Company name
- `{{lead.Workday Span 2025}}` - Current year metrics
- `{{lead.Workday Span 2024:default=--}}` - Previous year with default
- `{{my.Collaboration Time Content}}` - Dynamic content blocks

**Content Logic:**
- Parses time values (e.g., "4h 12m")
- Compares against benchmark thresholds
- Generates appropriate messaging
- Returns color-coded status

### Files

- `plab-email.html` - Production email template with Velocity tokens
- `velocity-scripts.md` - Detailed Velocity scripting logic and thresholds

### Business Impact

This approach:
- Eliminates need for 15+ separate email versions per segment
- Provides relevant, personalized insights to each recipient
- Reduces email build time from hours to minutes
- Improves engagement through context-aware messaging

### Live Demo

View an interactive demo at: [thisistimsresume.com/projects/velocity-email](https://thisistimsresume.com/projects/velocity-email)

---

**Connect:** [linkedin.com/in/timothymcurtis](https://linkedin.com/in/timothymcurtis) | [thisistimsresume.com](https://thisistimsresume.com)
