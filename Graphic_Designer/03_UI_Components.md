---
title: "CARIVIX AI — UI Components & Theme Design System"
document_id: "GD-03"
version: "1.0"
status: "Final"
last_updated: "2026-09-18"
author: "Shivanath Samudrala"
role: "Technical Writer"
---

# CARIVIX AI — UI Components & Theme Design System

## 1. Overview

The CARIVIX AI UI Design System was developed to create a **consistent and reusable interface structure** for the CARIVIX AI platform.

The system defines the visual treatment and behavior of major interface elements used throughout the application, including:

- Navigation
- KPI cards
- Data cards
- Charts
- Tables
- Buttons
- Forms
- Filters
- Alerts
- Dashboards
- Other information-based components

### Two Visual Themes

| Theme | Description |
|---|---|
| **Light Theme** | Primary clean and professional interface style |
| **Dark Theme** | Same structure, adapted to a darker visual environment |

Both themes follow the **same underlying component structure and information hierarchy**, while adapting backgrounds, surfaces, text, borders, and accent colors according to the selected theme.

> This approach allows CARIVIX AI to maintain the **same product experience** while providing different visual modes.

---

## 2. Light Theme

The Light Theme was designed as the **primary clean and professional interface style** for CARIVIX AI.

### Visual Direction

| # | Element |
|---|---|
| 1 | Light backgrounds |
| 2 | White content surfaces |
| 3 | Dark navy / gray typography |
| 4 | Blue as the primary accent |
| 5 | Subtle borders |
| 6 | Controlled status colors |
| 7 | Clean card layouts |
| 8 | Clear data visualization |

The light theme is particularly suitable for **information-heavy screens** because it provides strong contrast between the page background, cards, text, charts, and interactive elements.

> The design direction emphasizes a **professional enterprise dashboard appearance** rather than excessive gradients, glow effects, or decorative elements.

---

## 3. Dark Theme

The Dark Theme uses the **same component structure** as the Light Theme but changes the visual treatment to darker backgrounds and surfaces.

### Visual Direction

| # | Element |
|---|---|
| 1 | Dark navy backgrounds |
| 2 | Dark content surfaces |
| 3 | Light typography |
| 4 | Blue / cyan accents |
| 5 | Controlled status colors |
| 6 | Subtle borders |
| 7 | High-contrast charts and indicators |

> The purpose of the Dark Theme is **not** to create a completely different interface. Instead, the same components are adapted to the darker visual environment so that users can switch themes **without having to learn a different interface structure**.

This makes the theme system **more scalable** and maintains consistency between Light and Dark modes.

---

## 4. Dashboard Layout

The dashboard acts as the **primary container** for CARIVIX AI's information and intelligence components.

### 4.1 Sidebar Navigation

The sidebar provides access to major application modules and maintains a consistent navigation structure.

**Includes:**

- Navigation items
- Active page state
- Icons
- Labels
- Section organization
- Collapsed / expanded behavior

### 4.2 Top Navigation

The top area provides access to global functions such as:

- Search
- AI-related actions
- Notifications
- Risk / status information
- User / system controls

### 4.3 Main Content Area

The main content area contains the actual intelligence and analytics components, including:

- KPI cards
- Charts
- Tables
- Alerts
- Other information blocks

> The layout uses a **structured grid** so that components can be arranged according to their importance and information density.

---

## 5. KPI Cards

KPI cards are one of the **major components** of the CARIVIX AI dashboard. They present important metrics in a quick, easily scannable format.

### Typical KPI Card Contents

| # | Element |
|---|---|
| 1 | Metric title |
| 2 | Main numerical value |
| 3 | Supporting information |
| 4 | Trend / change indicator |
| 5 | Status or contextual indicator |
| 6 | Optional visual indicator / chart |

**Example:**

```
Total Alerts
1,284
↑ 12% from previous period
```

> The card structure gives the user the **most important number first**, followed by supporting information.

### KPI Card Design

KPI cards were designed with:

- Consistent dimensions
- Structured internal spacing
- Clear metric hierarchy
- Prominent numerical values
- Secondary supporting text
- Consistent borders / surfaces
- Theme-specific backgrounds
- Functional status colors

> This makes it possible to place multiple KPI cards together while maintaining a **consistent dashboard structure**.

---

## 6. Analytics Cards

Analytics cards provide **larger areas** for visualizing trends and relationships within data. Unlike KPI cards, which focus primarily on one metric, analytics cards provide **context** around the metric.

### Typical Analytics Card Contents

| # | Element |
|---|---|
| 1 | Chart title |
| 2 | Primary metric |
| 3 | Supporting value |
| 4 | Chart visualization |
| 5 | Time period |
| 6 | Comparison information |
| 7 | Filters or actions |

> These cards allow complex information to be grouped into **clearly defined sections**.

---

## 7. Line Charts

Line charts are used to represent **changes and trends over time**.

### Design Elements

| # | Element |
|---|---|
| 1 | Chart title |
| 2 | Metric / value |
| 3 | Horizontal time axis |
| 4 | Data points or line |
| 5 | Supporting labels |
| 6 | Optional comparison information |

### CARIVIX Use Cases

- Risk trends
- Alert activity
- Threat activity
- System activity
- Prediction trends
- Performance changes

> The chart is placed inside a **standardized card container** so that its spacing and hierarchy remain consistent with other analytics components.

---

## 8. Bar Charts

Bar charts are used when **different values need to be compared**.

### CARIVIX Use Cases

- Regional comparisons
- Category comparisons
- Alert counts
- Risk levels
- Performance metrics
- Resource distribution

> The bar chart component follows the **same card structure** as other analytics components, ensuring that charts from different sections of the platform look consistent.

---

## 9. Area Charts

Area charts provide another way to display trends while **visually emphasizing the magnitude of change**.

### CARIVIX Use Cases

- Activity trends
- Risk progression
- System usage
- Prediction patterns
- Monitoring data

> The area is kept visually controlled so that the chart remains **readable** and does not overpower the surrounding information.

---

## 10. Pie / Donut Charts

Pie and donut charts are used to communicate **proportional or categorical information**.

### CARIVIX Use Cases

- Risk distribution
- Alert categories
- Threat types
- Data categories
- System status
- Regional distribution

> The center of a donut chart can also be used to display an important **total or percentage**, making the visualization both informative and compact.

---

## 11. Progress & Status Components

Progress indicators communicate the **completion or current state** of a process.

### CARIVIX Use Cases

- System readiness
- Task completion
- Data processing
- Risk levels
- Monitoring status
- Prediction confidence

> The progress component uses **controlled colors and percentages** to make the status immediately understandable.

---

## 12. Data Tables

Tables are used when users need to examine **detailed information** rather than only high-level metrics.

### Table Structure

| # | Element |
|---|---|
| 1 | Column headers |
| 2 | Data rows |
| 3 | Status indicators |
| 4 | Numerical values |
| 5 | Sorting |
| 6 | Filtering |
| 7 | Pagination where required |
| 8 | Actions |

> Tables are designed with **clear row spacing and typography** so that large amounts of information remain readable.

For an enterprise intelligence platform like CARIVIX AI, tables provide the **detailed layer** beneath the summarized dashboard metrics.

---

## 13. Status Indicators & Badges

Status indicators are used to communicate **system conditions** quickly.

### Functional Colors

| Color | Meaning |
|---|---|
| 🟢 Green | Safe / Success |
| 🟠 Orange / Yellow | Warning |
| 🔴 Red | Critical / Error |
| 🔵 Blue | Information / Active state |
| 🟣 Violet | AI / Prediction-related information |

### Indicator Forms

- Badges
- Labels
- Dots
- Status text
- Card indicators
- Alert markers

> The purpose is to communicate meaning **consistently** instead of using colors purely for decoration.

---

## 14. Buttons & Action Components

Buttons provide the **main interaction points** within the interface.

### Button Patterns

| Type | Purpose |
|---|---|
| **Primary Button** | Most important action on a screen |
| **Secondary Button** | Supporting actions |
| **Outline Button** | Actions that should remain visually lighter |
| **Icon Button** | Compact actions (Search, Refresh, Filter, More options, Close) |

### Consistent Properties

- Height
- Padding
- Typography
- Border radius
- Color
- Hover state
- Active state
- Disabled state

> This ensures that actions **behave and look consistent** throughout the application.

---

## 15. Search & Filter Components

Because CARIVIX AI works with large amounts of intelligence and data, **search and filtering** are important UI components.

### Search Component

Provides a consistent area for users to find relevant information.

### Filter Capabilities

| # | Filter |
|---|---|
| 1 | Date |
| 2 | Location |
| 3 | Risk level |
| 4 | Category |
| 5 | Status |
| 6 | Data source |
| 7 | Other relevant parameters |

> These controls are designed to work **consistently across dashboard, analytics, reports, and monitoring screens**.

---

## 16. Input & Form Components

The UI system also establishes **reusable patterns** for user input.

### Input Components

| # | Component |
|---|---|
| 1 | Text fields |
| 2 | Search fields |
| 3 | Dropdowns |
| 4 | Select controls |
| 5 | Checkboxes |
| 6 | Toggles |
| 7 | Date selection |
| 8 | Filter controls |

> The components use consistent **labels, spacing, borders, states, and feedback**.

---

## 17. Alert & Notification Components

Alerts and notifications are particularly important for an intelligence platform.

### Alert Types

| Type | Purpose |
|---|---|
| **Informational** | Provides general system information |
| **Warning** | Highlights something requiring attention |
| **Critical** | Communicates an urgent or high-priority condition |
| **Success** | Confirms that an action or process has completed successfully |

> These states use consistent **colors, typography, icons, and container styles**.

---

## 18. AI Interaction Components

CARIVIX AI also requires components specifically designed around **AI interaction**.

### AI Components

| # | Component |
|---|---|
| 1 | AI search / query interface |
| 2 | AI response area |
| 3 | AI-generated insights |
| 4 | Voice input |
| 5 | Query results |
| 6 | AI recommendations |
| 7 | Insight cards |
| 8 | Loading / processing states |

> The AI components are designed to visually distinguish **user input, system processing, and AI-generated information**.
>
> This is important because CARIVIX is designed around converting **questions into data-driven visual insights** — users can ask questions by voice or text and receive automatically generated visualizations and AI summaries.

---

## 19. GIS & Map Components

For CARIVIX AI's geospatial functionality, the UI system also supports **map-based components**.

### Map Components

| # | Component |
|---|---|
| 1 | Map containers |
| 2 | Location indicators |
| 3 | Risk markers |
| 4 | Map controls |
| 5 | Zoom controls |
| 6 | Legends |
| 7 | Geographic information |
| 8 | Location-based cards |

> The GIS components follow the **same card, spacing, typography, and color standards** as the rest of the application so that the map interface feels like part of the same product.

---

## 20. Loading, Empty, Success & Error States

The UI system also considers **different system states**.

| State | Purpose |
|---|---|
| **Loading State** | Used while data or AI results are being processed |
| **Empty State** | Used when no data or results are available |
| **Success State** | Used after a successful operation |
| **Error State** | Used when an operation fails or requires attention |

> These states provide users with **feedback** rather than leaving the interface visually inactive.

---

## 21. Theme Consistency

One of the important aspects of the CARIVIX UI system is that the **Light and Dark Themes use the same component architecture**.

### Example: KPI Card

| Theme | Visual Treatment |
|---|---|
| **Light Theme** | White / light surface + dark text + blue accent |
| **Dark Theme** | Dark surface + light text + blue / cyan accent |

> The component itself **does not change** its purpose or structure. Only its **visual tokens** change.

### The Same Principle Applies To

- Charts
- Tables
- Buttons
- Forms
- Navigation
- Alerts
- Cards
- Status indicators
- AI components

> This makes the system **easier to maintain and scale**.

---

## 22. Component Standardization

The overall UI work focuses on **converting individual design elements into reusable components**.

Instead of designing:

```
Dashboard Card A → Dashboard Card B → Dashboard Card C
```

…independently, a **common card structure** is established and then adapted according to the content.

### Standardization Chain

```
Buttons → Cards → KPI Cards → Charts → Tables → Forms → Alerts → Navigation
```

### Each Component Has Defined Rules

| # | Rule |
|---|---|
| 1 | Size |
| 2 | Spacing |
| 3 | Typography |
| 4 | Color |
| 5 | Border |
| 6 | Radius |
| 7 | Content hierarchy |
| 8 | Interaction states |
| 9 | Light / Dark behavior |

> This creates a **scalable design system** rather than a collection of unrelated screens.

---

## 23. Overall Component Structure

The CARIVIX AI UI component system can be summarized as:

### Foundation

```
Colors → Typography → Spacing → Layout → Surfaces → Borders
```

### Navigation

```
Sidebar → Header → Search → Navigation states
```

### Metrics

```
KPI Cards → Metric Cards → Status indicators → Progress indicators
```

### Data Visualization

```
Line Charts → Bar Charts → Area Charts → Pie / Donut Charts → Analytics Cards
```

### Data Management

```
Tables → Filters → Search → Dropdowns → Pagination → Sorting
```

### Interaction

```
Buttons → Inputs → Forms → Toggles → Actions
```

### Intelligence

```
AI Query → AI Responses → AI Insights → Voice Interaction → Recommendation Cards
```

### Geospatial

```
Maps → Location markers → Map controls → Legends → Risk indicators
```

### System Feedback

```
Alerts → Notifications → Loading → Success → Error → Empty states
```

### Themes

```
Light Theme → Dark Theme
```

---

## 24. Conclusion

The CARIVIX AI UI Component & Theme Design System establishes a **reusable foundation** for designing the platform's interface. The major focus was on creating standardized:

- KPI cards
- Metric cards
- Analytics cards
- Charts
- Tables
- Navigation
- Buttons
- Forms
- Filters
- Alerts
- AI interaction components
- GIS components
- System states

…while maintaining the **same structure across both Light and Dark Themes**.

### Design Approach

The components were designed with a common approach to:

| # | Approach Area |
|---|---|
| 1 | Visual hierarchy |
| 2 | Spacing |
| 3 | Typography |
| 4 | Color |
| 5 | Surfaces |
| 6 | Interaction states |
| 7 | Responsive behavior |

> This allows different CARIVIX AI modules to use the **same UI language** while presenting different types of information.

Overall, the system provides CARIVIX AI with a **consistent, scalable, and reusable UI framework** that can support:

- Future dashboard modules
- Analytics features
- AI capabilities
- GIS functionality
- Enterprise workflows

---

## Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-09-18 | Shivanath Samudrala | Initial version — UI components & theme design system documentation |
