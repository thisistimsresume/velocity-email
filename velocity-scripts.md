# Velocity Scripting Logic

Documentation of the Velocity scripting used in the productivity benchmark email template.

## Token Structure

### Basic Personalization Tokens

```velocity
{{my.replacefirstname}}      ## Recipient first name (default: "there")
{{my.replacecompany}}         ## Company name (default: "Your organization")
{{my.CurrentYear}}            ## Current year (default: "2025")
{{my.currentaddress}}         ## Company address
```

### Metric Data Tokens

Current year metrics (2025):
```velocity
{{lead.Workday Span 2025}}
{{lead.Total Time 2025}}
{{lead.Productive Time 2025}}
{{lead.Focus Time 2025}}
{{lead.Collaboration Time 2025}}
```

Previous year metrics with defaults (2024):
```velocity
{{lead.Workday Span 2024:default=--}}
{{lead.Total Time 2024:default=--}}
{{lead.Productive Time 2024:default=--}}
{{lead.Focus Time 2024:default=--}}
{{lead.Collaboration Time 2024:default=--}}
```

### Dynamic Content Tokens

These tokens generate conditional content based on metric values:
```velocity
{{my.Collaboration Time Content}}
{{my.Focus Time Content}}
{{my.Productive Time Content}}
{{my.Total Time Content}}
{{my.Workday Span Content}}
```

## Content Generation Logic

### Collaboration Time

**Format:** Minutes (e.g., "44m", "1h 30m")

**Thresholds:**

| Range | Status | Message Type | Color |
|-------|--------|--------------|-------|
| 30-60m | ✅ Healthy | Congrats! | Green (#2ED4B5) |
| 20-30m | ⚠️ Low | Keep an eye on this | Yellow (#FBD13E) |
| 60-90m | ⚠️ High | Keep an eye on this | Yellow (#FBD13E) |
| <20m | 🔴 Very Low | This may call for action | Orange (#FF864B) |
| >90m | 🔴 Very High | This may call for action | Orange (#FF864B) |

**Benchmark:** 44 minutes

---

### Focus Time

**Format:** Hours (e.g., "4h 12m")

**Thresholds:**

| Range | Status | Message Type | Color |
|-------|--------|--------------|-------|
| 3.5-5h | ✅ Healthy | Congrats! | Green (#2ED4B5) |
| 3-3.5h | ⚠️ Low | Keep an eye on this | Yellow (#FBD13E) |
| 5-5.5h | ⚠️ High | Keep an eye on this | Yellow (#FBD13E) |
| <3h | 🔴 Very Low | This may call for action | Orange (#FF864B) |
| >5.5h | 🔴 Very High | This may call for action | Orange (#FF864B) |

**Benchmark:** 4 hours 12 minutes

---

### Productive Time

**Format:** Hours (e.g., "6h 33m")

**Thresholds:**

| Range | Status | Message Type | Color |
|-------|--------|--------------|-------|
| 5.5-7.5h | ✅ Healthy | Congrats! | Green (#2ED4B5) |
| 4.5-5.5h | ⚠️ Low | Keep an eye on this | Yellow (#FBD13E) |
| 7.5-8.5h | ⚠️ High | Keep an eye on this | Yellow (#FBD13E) |
| <4.5h | 🔴 Very Low | This may call for action | Orange (#FF864B) |
| >8.5h | 🔴 Very High | This may call for action | Orange (#FF864B) |

**Benchmark:** 6 hours 33 minutes

---

### Screen Time (Total Time)

**Format:** Hours (e.g., "7h 6m")

**Thresholds:**

| Range | Status | Message Type | Color |
|-------|--------|--------------|-------|
| 6-8h | ✅ Healthy | Well done! | Green (#2ED4B5) |
| 5-6h | ⚠️ Low | Keep an eye on this | Yellow (#FBD13E) |
| 8-9h | ⚠️ High | Keep an eye on this | Yellow (#FBD13E) |
| <5h | 🔴 Very Low | This may call for action | Orange (#FF864B) |
| >9h | 🔴 Very High | This may call for action | Orange (#FF864B) |

**Benchmark:** 7 hours 6 minutes

---

### Workday Span

**Format:** Hours (e.g., "8h 18m")

**Thresholds:**

| Range | Status | Message Type | Color |
|-------|--------|--------------|-------|
| 7.5-9h | ✅ Healthy | Congrats! | Green (#2ED4B5) |
| 9-10h | ⚠️ High | Keep an eye on this | Yellow (#FBD13E) |
| <7.5h | 🔴 Very Low | This may call for action | Orange (#FF864B) |
| >10h | 🔴 Very High | This may call for action | Orange (#FF864B) |

**Benchmark:** 8 hours 18 minutes

---

## Implementation Example

### Email Template Usage

```html
<p>Hi {{my.replacefirstname}},</p>

<p>{{my.replacecompany}}'s {{my.CurrentYear}} productivity data is ready.</p>

<!-- Dynamic content based on collaboration time -->
{{my.Collaboration Time Content}}

<!-- Current year metric -->
<td>{{lead.Collaboration Time 2025}}</td>

<!-- Previous year metric with default -->
<td>{{lead.Collaboration Time 2024:default=--}}</td>
```

### Content Generation Process

1. **Parse Time String** - Extract hours and minutes from format like "4h 12m"
2. **Convert to Comparable Unit** - Minutes for collaboration, hours for others
3. **Compare to Thresholds** - Determine which range the value falls into
4. **Generate Message** - Return appropriate HTML with color coding and status

### Example Generated Content

**Input:** Collaboration Time = "44m"

**Output:**
```html
<p>
  <strong style="color: #2ED4B5;">Congrats!</strong> 
  Your average of 44m of daily collaboration time closely matches the 
  benchmark (44 minutes) and falls within healthy parameters (30-60 minutes).
</p>
```

---

## Processing Logic (Conceptual)

```javascript
function generateCollaborationContent(timeString) {
  const minutes = parseTimeToMinutes(timeString);
  
  if (minutes >= 30 && minutes <= 60) {
    return "Congrats! message...";
  } else if (minutes > 60 && minutes <= 90) {
    return "Keep an eye on this message...";
  } else if (minutes < 20) {
    return "This may call for action message...";
  }
  // ... etc
}
```

## Benefits

- **Single Template:** One email serves all segments
- **Automatic Personalization:** Content adapts to recipient data
- **Scalable:** Easy to add new metrics or adjust thresholds
- **Maintainable:** Logic changes don't require new email builds
- **Testable:** Can preview with different data values
