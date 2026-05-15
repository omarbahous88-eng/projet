# AGENTS.md – Toraty (Rabat Smart Book 2026)

You are an expert React Native and Expo engineer helping me build **Toraty**.

Write clean, simple, maintainable code. Prioritize clarity over unnecessary abstraction.

Think like a senior mobile developer.
---
## Project Overview

We are building **Toraty**, a mobile app that turns the city of Rabat into an interactive literary library using AR, geolocation, and gamification.

The app includes:

- Scan monuments to unlock literary excerpts
- Augmented reality display of book extracts
- Earn XP and convert to Dirhams Culturels (DC)
- Redeem DC discounts at local shops
- Complete thematic quests and level up
- Premium subscription (29 MAD/month)

Keep the implementation simple and readable.
---
## Tech Stack

- Expo
- React Native
- TypeScript   
- Expo Router
- NativeWind
- Zustand
- AsyncStorage
- Clerk for authentication

Do not introduce new major libraries unless there is a strong reason. Ask before installing anything new.
---
## Development philosophy

1. Read this file first.
2. Keep the implementation simple.
3. Avoid overengineering.
4. Prefer readable code over clever code.
5. Build the smallest useful version first.
6. Refactor only when repetition appears.
---
## Decision Making

If something is unclear or could be improved, suggest a better approach. If a new library would significantly help, recommend it, explain why, and ask before adding it.

Do not install new libraries without approval.
---
## Architecture

Use this folder structure:

```text
app/
  (auth)/
  (tabs)/
components/
constants/
  images.ts
  quests.ts
data/
  monuments.json
  merchants.json
hooks/
lib/
  clerk.ts
  api.ts
  cn.ts
store/
  xpStore.ts
  dcStore.ts
  questStore.ts
types/
assets/
  images/
```
  
**app/** is for routes and screens only. Screens compose components and call hooks or stores. They should not contain large reusable UI blocks or business logic.

**components/** is for reusable UI. Create a component when it is reused in multiple places, when it makes a screen easier to read, or when it represents a clear UI concept. Examples for this app: `MonumentCard`, `QuestProgressBar`, `QRScannerView`, `DCRewardButton`. Do not create components too early.

**data/** holds hardcoded content. Keep it typed.

**store/** holds Zustand stores. Examples of state to keep here: `currentXP`, `currentDC`, `completedQuests`, `scannedMonuments`. Persist with AsyncStorage when needed.

**lib/** holds external service helpers (`clerk.ts`, `api.ts`, `cn.ts`). Never expose secret keys here.

---
## UI Rules

For any UI task:

- Replicate the provided design exactly.
- Match layout, spacing, padding, font sizes, font hierarchy, colors, border radius, shadows, alignment, and proportions.
- Do not approximate. Do not simplify unless explicitly asked.
---
## Styling Rules
Use NativeWind classes. Do not use StyleSheet unless it is not possible to style with className.

Use the NativeWind version installed in this project. Check package.json. Do not upgrade without approval.

Reuse class patterns through utilities in global.css.
---
## Style Exception List
Use StyleSheet or inline styles for:

- SafeAreaView (className not supported)
- KeyboardAvoidingView (behavior props)
- Modal (visible, transparent props)
- Animated.View (animated style values)
- Dynamic styles calculated at runtime
- Platform specific styles
- Pressable or TouchableOpacity pressed states
- Shadows (different per platform)

Everywhere else, use NativeWind.
---
## Image Rule

Use centralized image imports.

1. Check if constants/images.ts exists.
2. If not, create it.
3. Import all app images there.
4. Use them through the centralized object.

```ts
import monumentPlaceholder from "@/assets/images/monument-placeholder.png";
import badgeErudit from "@/assets/images/badge-erudit.png";

export const images = {
  monumentPlaceholder,
  badgeErudit,
};
```
```tsx

<Image source={images.mascot} />
```

Do not import image assets directly inside screens or components.
---
## State Management
- Zustand for global client state.
- Local state for temporary UI state.
- AsyncStorage for persistence.

---
## TypeScript
- Strict mode.
- No 'any'.
- Keep types simple and readable.
---
## Feature Implementation
1. Read this file first.
2. Identify the files to change.
3. Keep changes focused.
4. Do not rewrite unrelated code.
5. Follow existing patterns.
6. Make sure the feature works end to end.
7. Fix lint and type errors before finishing.
---
## Secrets
- Never expose secret keys in client code.
- Use server routes for tokens, AI calls, and any external API access.
---
## Authentication
Use Clerk. Do not build custom auth.
---
## Communication
Be concise. Explain what changed and how to test it.
---
## Final Reminder
Before every feature:

- Read this file.
- Follow it strictly.
- Build clean, simple code.
- Replicate UI exactly when designs are provided.
