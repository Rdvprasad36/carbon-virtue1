# CarbonVirtue — Carbon Footprint Awareness Platform

CarbonVirtue (also styled as CarbonSense) is a full-stack, lightweight Carbon Footprint Tracker and AI Conversational Assistant. It helps individuals understand, track over time, and systematically reduce their greenhouse gas output with real-time feedback and engaging, gamified weekly challenges.

## 🌟 Key Features
- **Conversational Expert AI**: Ask the integrated Gemini assistant contextual questions about utilities, diet choices, or travel commutes. Instant rough estimate ranges with confidence scales returned.
- **Accurate Mathematical Footprints**: Leverages real climate-science conversion factor constants to turn kWh, gas therms, diet types, and petrol km into real-time $CO_2e$ counts.
- **Visual Progress Dashboards**: Clean, reactive, hardware-accelerated inline SVG Trend chart mapping user registration history.
- **Actionable Gamification**: Motivational environmental challenges with completed checkboxes and celebratory milestone badges.
- **Privacy First & Copy-Exportable**: Anonymous local operational mode prevents public data exposure. One-click text-clipboard exporter extracts summaries instantly without messy file generations.

---

## 🛠 Prerequisites & Requirements
- **Node.js**: Ready for v20+
- **Database**: PostgreSQL / Supabase Migration schema provided inside `/db/schema.sql` (or Firebase Firestore dynamic fallback)
- **Gemini API Key**: (Optional but recommended) Access key available from Google AI Studio.

---

## 📁 Repository Structure
```
├── .github/workflows/ci.yml # Continuous Integration Action pipeline
├── db/
│   └── schema.sql           # PostgreSQL Database Schema Blueprint
├── prompts/
│   └── assistant_prompts.md # Engineered AI System instructions & prompt sheets
├── src/
│   ├── lib/
│   │   ├── calc.ts          # Core calculation math unit
│   │   └── firebase.ts      # Cloud dynamic store interface
│   ├── App.tsx              # Beautiful Tailwind UX Dashboard
│   ├── main.tsx             # React SPA mounting point
│   ├── types.ts             # Static Types definitions
│   └── index.css            # Global Tailwind imports
├── tests/
│   └── calc.test.ts         # Math calculation unit tests
├── server.ts                # Express backend routing & asset server code
├── README.md                # General introduction guidance
├── deploy.md                # External cloud deployment map
├── package.json             # NPM dependencies config
└── vite.config.ts           # Bundler config
```

---

## 🚀 Setup & Running Locally

1. **Clone the Repository** (ensure single branch, safe under 10MB limit):
   ```bash
   git clone <repo_url>
   cd carbon-virtue
   ```

2. **Configure Environment Variables**:
   Create a `.env` file in the root directory (never commit actual secret keys):
   ```env
   GEMINI_API_KEY="your_actual_gemini_api_key_from_ai_studio"
   APP_URL="http://localhost:3000"
   ```

3. **Install Dependencies**:
   ```bash
   npm install
   ```

4. **Boot Development Environment / Full-Stack Server**:
   ```bash
   npm run dev
   ```
   Open [http://localhost:3000](http://localhost:3000) to examine the live CarbonSense engine.

---

## 🧪 Verification via Unit Tests
We compile our test suite using `vitest` which supports extremely fast, block-free continuous testing:
```bash
# Run tests synchronously
npm run test
```

Our tests rigorously verify calculation rules, including edge cases (zero inputs, vegans baseline diet, standard omnivore travel outputs).

---

## 📡 Core Carbon Calculation Rules
Our calculations are built directly upon verified, clean conversion factors:
- **Electricity Grid Factor**: $0.475 \text{ kg } CO_2e / \text{kWh}$
- **Natural Gas Factor**: $5.30 \text{ kg } CO_2e / \text{therm}$
- **Petrol Passenger vehicle**: $0.192 \text{ kg } CO_2e / \text{km}$ (weekly parameters automatically scaled to monthly using a factor of $4.333$)
- **Diet Monthly Baseline (Vegan)**: $100 \text{ kg } CO_2e / \text{month}$ multiplied by relative multipliers:
  - **Vegan**: $\times 1.0$ (Baseline: $100 \text{ kg}$)
  - **Vegetarian**: $\times 1.2$ (Baseline: $120 \text{ kg}$)
  - **Omnivore**: $\times 1.6$ (Baseline: $160 \text{ kg}$)

---

## 💭 Climate Assumptions & Math Scaling
- **Utility Conversions**: Thermal factors assume direct standard residential Natural Gas efficiency factors. Electricity calculations approximate grid-average baselines.
- **Weekly to Monthly scale**: Car commutes are expressed weekly for ease of user tracking. The software translates this to monthly using $4.333$ weeks/month.
- **Action plan prioritizing**: High-impact actions are mathematically sorted, bubbling higher-impact items (e.g. residential solar installation) to the top while matching user levels.

---

## 🔮 Future Enhancements
- **Dynamic Grid Integration**: Integration with third-party real-time carbon grid factor trackers (such as electricityMap) for region-specific real-time adjustments.
- **Relational Sync**: Activating deep automatic Supabase REST sync queries for collaborative team challenges.
- **Interactive Multi-User Boards**: Shared dashboard views for friendly group carbon reduction milestones.
# carbon-virtue1
