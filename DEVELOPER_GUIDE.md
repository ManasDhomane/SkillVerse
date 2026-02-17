# SkillVerse - Developer Guide

## 🏗️ Project Structure

```
/src
├── /app
│   ├── App.tsx                    # Main app with RouterProvider
│   ├── routes.tsx                 # Route configuration
│   ├── /pages                     # All page components
│   │   ├── Home.tsx              # Landing page
│   │   ├── AIInterview.tsx       # Interview chamber
│   │   ├── SkillReport.tsx       # Fail flow report
│   │   ├── VirtualWorkplace.tsx  # Pass flow simulation
│   │   └── SkillProfile.tsx      # Final profile page
│   ├── /components               # Reusable components
│   │   ├── CountdownTimer.tsx    # Timer with progress ring
│   │   ├── FeatureCard.tsx       # Feature showcase card
│   │   ├── LoadingScreen.tsx     # Loading state
│   │   ├── ParticleBackground.tsx # Animated background
│   │   ├── SkillBadge.tsx        # Skill tag component
│   │   ├── StatCard.tsx          # Stat display card
│   │   ├── XPNotification.tsx    # Gamification toast
│   │   └── /ui                   # Radix UI components
│   └── /utils                    # Utility functions
│       ├── data.ts               # Common data utilities
│       └── mockData.ts           # Mock data for demos
└── /styles
    ├── fonts.css                 # Font imports
    ├── index.css                 # Custom styles
    ├── tailwind.css              # Tailwind imports
    └── theme.css                 # Theme tokens
```

## 🎨 Component Usage

### StatCard
```tsx
<StatCard
  label="Skill Score"
  value={85}
  icon={TrendingUp}
  color="blue"
  trend="up"
  trendValue="+5%"
  delay={0.2}
/>
```

### SkillBadge
```tsx
<SkillBadge
  skill="Problem Solving"
  level={91}
  animated={true}
/>
```

### CountdownTimer
```tsx
<CountdownTimer
  timeLeft={3600}
  totalTime={7200}
  size="md"
  showProgress={true}
/>
```

### ParticleBackground
```tsx
<ParticleBackground variant="blue" />
```

### XPNotification
```tsx
<XPNotification
  show={true}
  type="xp"
  title="+250 XP"
  description="Task completed!"
/>
```

## 🎯 Key Pages

### 1. Home Page (`/`)
- Landing page with hero section
- Feature cards showcase
- Quick stats display
- CTA to start interview

### 2. AI Interview (`/interview`)
- 5-question adaptive interview
- Voice/text input toggle
- Real-time AI feedback
- Progress tracking
- Skill evaluation display

**Navigation Logic:**
- After completion, randomly routes to either:
  - `/workplace` (pass flow)
  - `/skill-report` (fail flow)

### 3. Skill Report (`/skill-report`)
- Overall performance score
- Skill breakdown with charts
- Radar chart visualization
- Performance timeline
- AI-generated insights
- Actions: Retry, Learning Path, Download

### 4. Virtual Workplace (`/workplace`)
- Task panel with constraints
- Monaco-style code editor
- AI team members panel
- Live chat functionality
- Test execution
- Time pressure with countdown

**AI Team Members:**
- Sarah Chen - Senior Developer
- Marcus Rodriguez - Product Manager
- Priya Sharma - QA Engineer
- Alex Kim - DevOps Engineer

### 5. Skill Profile (`/profile`)
- Profile card with avatar
- XP and level display
- Skill radar chart
- Completed simulations list
- Achievement badges
- Share functionality (LinkedIn, Twitter, Email)
- Downloadable badge

## 🔄 Data Flow

```
User starts → Interview begins
            → 5 questions answered
            → AI evaluation
            ↓
       Pass/Fail decision
       ↙          ↘
   Pass            Fail
   ↓               ↓
Workplace      Skill Report
Simulation        ↓
   ↓          Option to retry
Profile Page       ↓
                Profile Page
```

## 🎨 Styling Guide

### Color Usage
- **Blue**: Primary actions, trust, professionalism
- **Violet**: Secondary actions, creativity
- **Amber**: Warnings, medium priority
- **Green**: Success, achievements
- **Red**: Errors, critical items

### Component Patterns

**Glassmorphism Card:**
```tsx
<div className="p-6 rounded-2xl border border-gray-800/50 bg-gray-900/30 backdrop-blur-sm">
  {/* Content */}
</div>
```

**Gradient Button:**
```tsx
<Button className="bg-gradient-to-r from-blue-600 to-violet-600 hover:from-blue-700 hover:to-violet-700">
  Action
</Button>
```

**Animated Container:**
```tsx
<motion.div
  initial={{ opacity: 0, y: 20 }}
  animate={{ opacity: 1, y: 0 }}
  transition={{ delay: 0.2 }}
>
  {/* Content */}
</motion.div>
```

## 🎮 Gamification System

### XP Calculation
```typescript
const calculateXP = (action: string) => {
  const xpValues = {
    interview: 100,
    simulation: 250,
    achievement: 150,
    streak: 50,
  };
  return xpValues[action] || 0;
};
```

### Level System
- Level = floor(totalXP / 1000) + 1
- Progress to next level = (currentXP % 1000) / 1000

### Achievement Triggers
- First Interview: Complete first AI interview
- Workplace Master: Complete simulation
- Fast Thinker: Complete task in < 30 mins
- Team Player: Chat with 3+ AI members
- Perfectionist: Score 90+ on any task

## 🔧 Utility Functions

### Time Formatting
```typescript
import { formatTime } from './utils/data';
formatTime(3600); // "1:00:00"
```

### Skill Level Detection
```typescript
import { getSkillLevel } from './utils/data';
getSkillLevel(85); // Returns ADVANCED level object
```

### XP Progress
```typescript
import { getXPProgress } from './utils/data';
getXPProgress(2840); // { currentLevelXP: 840, percentage: 84, remaining: 160 }
```

## 🎯 Best Practices

1. **Animations**: Use Motion for all animations, keep delays subtle (0.1-0.3s)
2. **Colors**: Stick to the defined color palette for consistency
3. **Loading States**: Always show loading feedback for async operations
4. **Error Handling**: Provide clear, actionable error messages
5. **Accessibility**: Maintain proper ARIA labels and keyboard navigation
6. **Mobile**: Ensure responsive design for all screen sizes
7. **Performance**: Lazy load heavy components, optimize images

## 🐛 Common Issues & Solutions

### Issue: Routes not working
**Solution:** Ensure RouterProvider is in App.tsx with proper router import

### Issue: Animations not smooth
**Solution:** Check Motion import: `import { motion } from "motion/react"`

### Issue: Charts not rendering
**Solution:** Ensure ResponsiveContainer wraps chart component

### Issue: Colors not showing
**Solution:** Verify Tailwind classes are not purged, check theme.css

## 📦 Dependencies

**Core:**
- react: ^18.3.1
- react-router: ^7.13.0
- motion: ^12.23.24

**UI:**
- @radix-ui/*: Various versions
- lucide-react: ^0.487.0
- recharts: ^2.15.2

**Styling:**
- tailwindcss: ^4.1.12
- @tailwindcss/vite: ^4.1.12

## 🚀 Development Tips

1. Start with the Home page to understand the flow
2. Use browser DevTools to inspect animations
3. Test all routes and navigation paths
4. Verify responsive design at different breakpoints
5. Check dark mode compatibility (default theme)
6. Test interactions with keyboard and mouse
7. Validate form inputs and error states

## 📝 Code Style

- Use TypeScript interfaces for props
- Prefer functional components with hooks
- Keep components focused and single-purpose
- Extract reusable logic into custom hooks
- Use meaningful variable names
- Comment complex logic
- Follow the existing naming conventions

## 🎓 Learning Resources

- Motion (Framer Motion): https://motion.dev
- Radix UI: https://www.radix-ui.com
- Recharts: https://recharts.org
- Tailwind CSS v4: https://tailwindcss.com
- React Router: https://reactrouter.com

---

Happy coding! 🚀
