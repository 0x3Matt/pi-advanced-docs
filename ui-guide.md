# UI Development Guide - Piverse

## Table of Contents
1. [Technology Stack](#technology-stack)
2. [Design System](#design-system)
3. [Component Standards](#component-standards)
4. [Page Layouts](#page-layouts)
5. [Theme Configuration](#theme-configuration)
6. [Accessibility Standards](#accessibility-standards)
7. [Performance Guidelines](#performance-guidelines)
8. [Best Practices](#best-practices)

## Technology Stack

### Core Technologies
- **React 18.3.1** - UI Framework
  - Functional Components
  - React Hooks
  - TypeScript Integration
- **TypeScript** - Type Safety
- **Vite 5.4.1** - Build Tool
  - Hot Module Replacement (HMR)
  - Fast Development Server
  - Optimized Production Builds

### UI Framework
- **Tailwind CSS 3.4.11**
  - Utility-First Approach
  - JIT (Just-In-Time) Compilation
  - Custom Plugin Support
- **shadcn/ui**
  - Radix UI Primitives
  - Accessible Components
  - Customizable Themes

### Component Libraries
- **Radix UI Primitives**
  ```typescript
  // Example usage
  import * as Dialog from '@radix-ui/react-dialog';
  import * as Select from '@radix-ui/react-select';
  ```
- **Supporting Libraries**
  - `lucide-react` - Icons
  - `class-variance-authority` - Component Variants
  - `tailwind-merge` - Class Merging
  - `clsx` - Conditional Classes

## Design System

### Colors
```css
/* Brand Colors */
--primary: #4527A0;      /* Primary Purple */
--primary-dark: #311B92;  /* Dark Purple */
--accent: #F97316;       /* Accent Orange */
--success: #22C55E;      /* Success Green */
--warning: #F97316;      /* Warning Orange */
--error: #EF4444;        /* Error Red */

/* Gradients */
--gradient-primary: linear-gradient(to bottom right, #9C27B0, #673AB7, #3F51B5);
--gradient-card: linear-gradient(to bottom right, rgba(69, 39, 160, 0.8), rgba(103, 58, 183, 0.8));

/* Background & Surfaces */
--background: var(--gradient-primary);
--card-bg: rgba(255, 255, 255, 0.05);
--card-hover: rgba(255, 255, 255, 0.1);
--overlay: rgba(0, 0, 0, 0.5);

/* Text Colors */
--text-primary: #FFFFFF;
--text-secondary: rgba(255, 255, 255, 0.6);
--text-muted: rgba(255, 255, 255, 0.4);
```

### Typography
```css
/* Headings */
h1: 2.25rem (36px) - font-bold
h2: 1.875rem (30px) - font-semibold
h3: 1.5rem (24px) - font-semibold
h4: 1.25rem (20px) - font-medium

/* Body Text */
body: 1rem (16px) - font-normal
small: 0.875rem (14px) - font-normal
xs: 0.75rem (12px) - font-normal

/* Font Weights */
regular: 400
medium: 500
semibold: 600
bold: 700
```

### Component Patterns

#### Dashboard Cards
```tsx
// Standard Dashboard Card
<div className={cn(cardStyle, "p-6")}>
  <h2 className="text-lg font-semibold text-white mb-4">Card Title</h2>
  {/* Card content */}
</div>

// Glass Effect Card
<div className={cn(cardWithPadding, "relative bg-gradient-to-br from-[#4527A0]/80 to-[#673AB7]/80 overflow-hidden")}>
  {/* Decorative Circles */}
  <div className="absolute -top-20 -left-20 w-40 h-40 rounded-full bg-[#9C27B0] opacity-40 blur-2xl"></div>
  <div className="absolute -bottom-20 -right-20 w-40 h-40 rounded-full bg-[#3F51B5] opacity-40 blur-2xl"></div>
  {/* Card content */}
</div>

// Data Card
<div className={cn(cardStyle, "p-4 bg-white/5 relative")}>
  <div className="flex items-start gap-4">
    <div className="shrink-0 mt-1">
      <Icon className="text-icon-base" />
    </div>
    <div className="flex-1 min-w-0">
      <h3 className="text-lg font-semibold text-white mb-1">Title</h3>
      <p className="text-sm text-white/60">Description</p>
    </div>
  </div>
</div>
```

#### Dropdowns and Select Inputs
```tsx
// Basic Dropdown
<select
  className="w-full px-3 py-2 rounded-lg bg-[#4527A0] hover:bg-[#4527A0]/80 transition-colors text-white border border-white/20"
>
  <option value="all">All Types</option>
  {/* Options */}
</select>

// Search Input with Dropdown
<div className="relative">
  <Search className="absolute left-3 top-1/2 -translate-y-1/2 w-4 h-4 text-white/40" />
  <input
    type="text"
    placeholder="Search..."
    className="w-full pl-9 pr-4 rounded-lg bg-black/30 border border-white/20 text-white placeholder:text-white/40 focus:outline-none focus:border-white/20"
  />
</div>

// Filter Dropdown
<button
  className="px-4 py-2 rounded-lg bg-[#4527A0] hover:bg-[#4527A0]/80 transition-colors text-white flex items-center gap-2"
>
  <Filter className="w-5 h-5" />
  Filters
  <ChevronDown className={cn("w-4 h-4 transition-transform", showFilters && "rotate-180")} />
</button>
```

#### Status Indicators
```tsx
// Success Status
<span className="px-2 py-1 rounded-full bg-green-400/10 text-green-400 text-xs">
  Completed
</span>

// Warning/Pending Status
<span className="px-2 py-1 rounded-full bg-yellow-400/10 text-yellow-400 text-xs">
  Pending
</span>

// Error Status
<span className="px-2 py-1 rounded-full bg-red-400/10 text-red-400 text-xs">
  Failed
</span>
```

### Public Pages Layout

#### Landing Page
```tsx
// Hero Section
<div className="min-h-screen bg-gradient-to-br from-[#9C27B0] via-[#673AB7] to-[#3F51B5] px-4">
  <div className="max-w-7xl mx-auto pt-24 pb-20">
    {/* Content */}
  </div>
</div>

// Feature Card
<div className="glass-card p-6 backdrop-blur-xl bg-white bg-opacity-10 border border-white/10">
  <div className="flex flex-col items-center text-center">
    <div className="w-12 h-12 rounded-full bg-[#4527A0] flex items-center justify-center mb-4">
      <Icon className="w-6 h-6 text-white" />
    </div>
    <h3 className="text-lg font-semibold text-white mb-2">Title</h3>
    <p className="text-white/90">Description</p>
  </div>
</div>
```

#### Transaction Pages
```tsx
// Transaction Form
<form className="space-y-6">
  <div className="grid grid-cols-2 gap-4">
    <div>
      <label className="block text-sm font-medium text-white/60 mb-2">
        Label
      </label>
      <input
        type="number"
        className="w-full p-3 rounded-lg bg-black/30 border border-white/10 text-white placeholder:text-white/40 focus:outline-none focus:border-white/20 text-lg font-medium"
        placeholder="0.00"
      />
    </div>
  </div>
</form>

// Action Button
<button 
  type="submit"
  className="w-full p-3 sm:p-4 rounded-lg bg-[#4527A0] hover:bg-opacity-90 text-white font-medium transition-colors flex items-center justify-center gap-2"
>
  <Icon className="w-5 h-5" />
  Button Text
</button>
```

### Layout Patterns

#### Dashboard Layout
```tsx
// Main Layout
<div className="min-h-screen bg-gradient-to-br from-[#9C27B0] via-[#673AB7] to-[#3F51B5]">
  <Sidebar />
  <main className={cn("min-h-screen transition-all duration-300", sidebarClasses)}>
    {/* Content */}
  </main>
</div>

// Content Container
<div className="container mx-auto px-3 sm:px-4 lg:px-6 py-4 sm:py-6 lg:py-8">
  {/* Page content */}
</div>
```

#### Grid Layouts
```tsx
// Two Column Grid
<div className="grid grid-cols-1 lg:grid-cols-2 gap-6">
  {/* Grid items */}
</div>

// Three Column Grid
<div className="grid grid-cols-1 md:grid-cols-3 gap-6">
  {/* Grid items */}
</div>

// Responsive Table
<div className={cn(cardStyle, "overflow-hidden")}>
  <div className="overflow-x-auto">
    <table className="w-full">
      {/* Table content */}
    </table>
  </div>
</div>
```

### Icons and Assets
```tsx
// Icon Sizes
<Icon className="w-4 h-4" />  // Small (16px)
<Icon className="w-5 h-5" />  // Medium (20px)
<Icon className="w-6 h-6" />  // Large (24px)

// Logo Usage
<img 
  src="/assets/images/pi-network-logo.png" 
  alt="Pi Network" 
  className="w-10 h-10 rounded-lg"
/>
```

### Responsive Design
```css
/* Breakpoints */
sm: 640px   /* Small devices */
md: 768px   /* Medium devices */
lg: 1024px  /* Large devices */
xl: 1280px  /* Extra large devices */
2xl: 1536px /* 2X large devices */

/* Responsive Patterns */
.responsive-container {
  @apply px-4 sm:px-6 lg:px-8;
  @apply py-4 sm:py-6 lg:py-8;
  @apply max-w-7xl mx-auto;
}

.responsive-text {
  @apply text-base sm:text-lg lg:text-xl;
}

.responsive-grid {
  @apply grid-cols-1 sm:grid-cols-2 lg:grid-cols-3;
}
```

## Best Practices

### Component Organization
```
src/
├── components/
│   ├── ui/               # Base UI components
│   ├── dashboard/        # Dashboard components
│   │   ├── layout/      # Layout components
│   │   └── widgets/     # Dashboard widgets
│   ├── forms/           # Form components
│   └── shared/          # Shared components
```

### Styling Guidelines
1. Use `cn()` utility for class merging
2. Follow consistent spacing patterns
3. Maintain color scheme consistency
4. Use semantic class naming
5. Implement responsive design patterns
6. Maintain accessibility standards

### Performance Considerations
1. Lazy load components when possible
2. Optimize images and assets
3. Minimize re-renders
4. Use proper caching strategies
5. Implement code splitting

### Charts and Data Visualization

#### Area Chart
```tsx
// Area Chart Component
<div className="h-[200px] w-full">
  <ResponsiveContainer width="100%" height="100%">
    <AreaChart
      data={data}
      margin={{ top: 5, right: 10, left: 10, bottom: 0 }}
    >
      <defs>
        <linearGradient id="gradientArea" x1="0" y1="0" x2="0" y2="1">
          <stop offset="0%" stopColor="#4527A0" stopOpacity={0.5} />
          <stop offset="100%" stopColor="#4527A0" stopOpacity={0} />
        </linearGradient>
      </defs>
      <Area
        type="monotone"
        dataKey="value"
        stroke="#4527A0"
        fill="url(#gradientArea)"
        strokeWidth={2}
      />
      <XAxis
        dataKey="date"
        stroke="#FFFFFF40"
        fontSize={12}
        tickLine={false}
        axisLine={false}
      />
      <YAxis
        stroke="#FFFFFF40"
        fontSize={12}
        tickLine={false}
        axisLine={false}
        tickFormatter={(value) => `${value}`}
      />
      <Tooltip
        content={({ active, payload }) => {
          if (active && payload && payload.length) {
            return (
              <div className="rounded-lg border border-white/10 bg-black/60 backdrop-blur-md p-2 shadow-xl">
                <p className="text-white text-sm font-medium">
                  {payload[0].value}
                </p>
              </div>
            );
          }
          return null;
        }}
      />
    </AreaChart>
  </ResponsiveContainer>
</div>
```

#### Bar Chart
```tsx
// Bar Chart Component
<div className="h-[200px] w-full">
  <ResponsiveContainer width="100%" height="100%">
    <BarChart
      data={data}
      margin={{ top: 5, right: 10, left: 10, bottom: 0 }}
    >
      <Bar dataKey="value" radius={[4, 4, 0, 0]}>
        {data.map((entry, index) => (
          <Cell
            key={`cell-${index}`}
            fill={entry.value > 0 ? "#22C55E" : "#EF4444"}
            fillOpacity={0.7}
          />
        ))}
      </Bar>
      <XAxis
        dataKey="date"
        stroke="#FFFFFF40"
        fontSize={12}
        tickLine={false}
        axisLine={false}
      />
      <YAxis
        stroke="#FFFFFF40"
        fontSize={12}
        tickLine={false}
        axisLine={false}
        tickFormatter={(value) => `${value}`}
      />
      <Tooltip
        cursor={{ fill: "#FFFFFF10" }}
        content={({ active, payload }) => {
          if (active && payload && payload.length) {
            return (
              <div className="rounded-lg border border-white/10 bg-black/60 backdrop-blur-md p-2 shadow-xl">
                <p className="text-white text-sm font-medium">
                  {payload[0].value}
                </p>
              </div>
            );
          }
          return null;
        }}
      />
    </BarChart>
  </ResponsiveContainer>
</div>
```

#### Line Chart with Multiple Series
```tsx
// Multi-Series Line Chart
<div className="h-[300px] w-full">
  <ResponsiveContainer width="100%" height="100%">
    <LineChart
      data={data}
      margin={{ top: 5, right: 10, left: 10, bottom: 0 }}
    >
      <CartesianGrid strokeDasharray="3 3" stroke="#FFFFFF10" />
      <XAxis
        dataKey="date"
        stroke="#FFFFFF40"
        fontSize={12}
        tickLine={false}
        axisLine={false}
      />
      <YAxis
        stroke="#FFFFFF40"
        fontSize={12}
        tickLine={false}
        axisLine={false}
        tickFormatter={(value) => `${value}`}
      />
      <Tooltip
        content={({ active, payload }) => {
          if (active && payload && payload.length) {
            return (
              <div className="rounded-lg border border-white/10 bg-black/60 backdrop-blur-md p-3 shadow-xl">
                {payload.map((entry, index) => (
                  <div key={`tooltip-${index}`} className="flex items-center gap-2">
                    <div
                      className="w-3 h-3 rounded-full"
                      style={{ backgroundColor: entry.color }}
                    />
                    <p className="text-white text-sm">
                      {entry.name}: {entry.value}
                    </p>
                  </div>
                ))}
              </div>
            );
          }
          return null;
        }}
      />
      <Line
        type="monotone"
        dataKey="buy"
        stroke="#22C55E"
        strokeWidth={2}
        dot={false}
      />
      <Line
        type="monotone"
        dataKey="sell"
        stroke="#F97316"
        strokeWidth={2}
        dot={false}
      />
    </LineChart>
  </ResponsiveContainer>
</div>
```

#### Pie Chart
```tsx
// Pie Chart Component
<div className="h-[200px] w-full">
  <ResponsiveContainer width="100%" height="100%">
    <PieChart>
      <Pie
        data={data}
        cx="50%"
        cy="50%"
        innerRadius={60}
        outerRadius={80}
        paddingAngle={2}
        dataKey="value"
      >
        {data.map((entry, index) => (
          <Cell
            key={`cell-${index}`}
            fill={colors[index % colors.length]}
            fillOpacity={0.8}
          />
        ))}
      </Pie>
      <Tooltip
        content={({ active, payload }) => {
          if (active && payload && payload.length) {
            const data = payload[0].payload;
            return (
              <div className="rounded-lg border border-white/10 bg-black/60 backdrop-blur-md p-2 shadow-xl">
                <p className="text-white text-sm font-medium">
                  {data.name}: {data.value}
                </p>
                <p className="text-white/60 text-xs">
                  {((data.value / total) * 100).toFixed(1)}%
                </p>
              </div>
            );
          }
          return null;
        }}
      />
    </PieChart>
  </ResponsiveContainer>
</div>
```

#### Chart Card Container
```tsx
// Chart Card Wrapper
<div className={cn(cardStyle, "p-6")}>
  <div className="flex items-center justify-between mb-6">
    <div>
      <h3 className="text-lg font-semibold text-white">{title}</h3>
      <p className="text-sm text-white/60">{subtitle}</p>
    </div>
    {/* Optional Chart Controls */}
    <div className="flex items-center gap-2">
      <select
        className="px-2 py-1 rounded-lg bg-white/10 border border-white/20 text-white text-sm"
        value={timeRange}
        onChange={(e) => setTimeRange(e.target.value)}
      >
        <option value="day">24h</option>
        <option value="week">7d</option>
        <option value="month">30d</option>
      </select>
    </div>
  </div>
  
  {/* Chart Component */}
  <div className="w-full aspect-[16/9]">
    {/* Chart goes here */}
  </div>
  
  {/* Optional Legend */}
  <div className="mt-4 flex items-center gap-4">
    {legendItems.map((item, index) => (
      <div key={index} className="flex items-center gap-2">
        <div
          className="w-3 h-3 rounded-full"
          style={{ backgroundColor: item.color }}
        />
        <span className="text-sm text-white/60">{item.label}</span>
      </div>
    ))}
  </div>
</div>
```

#### Chart Loading States
```tsx
// Loading Skeleton
<div className="animate-pulse">
  <div className="h-6 w-32 bg-white/10 rounded mb-2" />
  <div className="h-4 w-24 bg-white/10 rounded mb-6" />
  <div className="h-[200px] bg-white/10 rounded" />
</div>

// Error State
<div className="h-[200px] flex items-center justify-center">
  <div className="text-center">
    <AlertTriangle className="w-8 h-8 text-red-400 mx-auto mb-2" />
    <p className="text-white/60">Failed to load chart data</p>
    <button
      onClick={retryLoad}
      className="mt-2 px-3 py-1 rounded-lg bg-white/10 hover:bg-white/20 text-white text-sm"
    >
      Retry
    </button>
  </div>
</div>
```

#### Chart Utilities
```typescript
// Data Formatting
const formatChartData = (data: any[]) => {
  return data.map(item => ({
    date: format(new Date(item.timestamp), 'MMM dd'),
    value: Number(item.value)
  }));
};

// Value Formatting
const formatValue = (value: number) => {
  if (value >= 1000000) return `${(value / 1000000).toFixed(1)}M`;
  if (value >= 1000) return `${(value / 1000).toFixed(1)}K`;
  return value.toString();
};

// Color Utilities
const chartColors = {
  primary: '#4527A0',
  success: '#22C55E',
  warning: '#F97316',
  error: '#EF4444',
  gray: '#FFFFFF40'
};

// Gradient Definitions
const gradients = {
  area: {
    id: 'gradientArea',
    color: '#4527A0',
    opacity: [0.5, 0]
  },
  bar: {
    id: 'gradientBar',
    color: '#22C55E',
    opacity: [0.8, 0.4]
  }
};
```

---
Last Updated: 2024-03-20
Version: 1.2.0 