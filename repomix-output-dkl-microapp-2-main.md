This file is a merged representation of the entire codebase, combined into a single document by Repomix.
The content has been processed where security check has been disabled.

# File Summary

## Purpose
This file contains a packed representation of the entire repository's contents.
It is designed to be easily consumable by AI systems for analysis, code review,
or other automated processes.

## File Format
The content is organized as follows:
1. This summary section
2. Repository information
3. Directory structure
4. Repository files (if enabled)
5. Multiple file entries, each consisting of:
  a. A header with the file path (## File: path/to/file)
  b. The full contents of the file in a code block

## Usage Guidelines
- This file should be treated as read-only. Any changes should be made to the
  original repository files, not this packed version.
- When processing this file, use the file path to distinguish
  between different files in the repository.
- Be aware that this file may contain sensitive information. Handle it with
  the same level of security as you would the original repository.

## Notes
- Some files may have been excluded based on .gitignore rules and Repomix's configuration
- Binary files are not included in this packed representation. Please refer to the Repository Structure section for a complete list of file paths, including binary files
- Files matching patterns in .gitignore are excluded
- Files matching default ignore patterns are excluded
- Security check has been disabled - content may contain sensitive information
- Files are sorted by Git change count (files with more changes are at the bottom)

# Directory Structure
```
dkl-microapp-2-main/
  app/
    (auth)/
      login/
        page.tsx
      register/
        page.tsx
      signup/
        page.tsx
      layout.tsx
    (dashboard)/
      analytics/
        page.tsx
      builders/
        [id]/
          edit/
            page.tsx
          page.tsx
        loading.tsx
        page.tsx
      dashboard/
        page.tsx
      import/
        page.tsx
      insights/
        page.tsx
      listings/
        [id]/
          edit/
            page.tsx
          page.tsx
        page.tsx
      reports/
        page.tsx
      settings/
        page.tsx
      social/
        [postId]/
          page.tsx
        loading.tsx
        page.tsx
      layout.tsx
    actions/
      ai-actions.ts
    globals.css
    layout.tsx
    page.tsx
  components/
    layout/
      header.tsx
      sidebar.tsx
    ui/
      alert-dialog.tsx
      alert.tsx
      badge.tsx
      button.tsx
      card.tsx
      chart.tsx
      checkbox.tsx
      command.tsx
      data-table-column-header.tsx
      data-table-pagination.tsx
      data-table-toolbar.tsx
      data-table.tsx
      dialog.tsx
      dropdown-menu.tsx
      input.tsx
      label.tsx
      popover.tsx
      progress.tsx
      radio-group.tsx
      scroll-area.tsx
      select.tsx
      separator.tsx
      sheet.tsx
      switch.tsx
      table.tsx
      tabs.tsx
      textarea.tsx
      toast.tsx
      toaster.tsx
      toggle.tsx
    builder-assignment-dialog.tsx
    builder-form-dialog.tsx
    editable-field.tsx
    field-mapping-sheet.tsx
    header.tsx
    listing-form-dialog.tsx
    main-nav.tsx
    mapbox-map.tsx
    pill-input.tsx
    sidebar.tsx
    social-post-property-item.tsx
    theme-provider.tsx
    user-nav.tsx
  contexts/
    auth-context.tsx
  hooks/
    use-toast.ts
  lib/
    supabase/
      client.ts
      server.ts
    builder-fields.ts
    color-utils.ts
    listing-fields.ts
    supabase.ts
    utils.ts
  public/
    placeholder-logo.svg
    placeholder.svg
  styles/
    globals.css
  supabase/
    functions/
      geocode-properties/
        index.ts
    migrations/
      001_add_user_field_mappings.sql
      002_add_mapbox_key_to_user_settings.sql
      003_update_existing_mappings.sql
    schema.sql
    seed-social-posts.sql
    social-schema.sql
    update-schema.sql
  types/
    supabase.ts
  .gitignore
  components.json
  next.config.mjs
  package.json
  postcss.config.mjs
  README.md
  tailwind.config.ts
  tsconfig.json
```

# Files

## File: dkl-microapp-2-main/app/(auth)/login/page.tsx
```typescript
"use client"

import type React from "react"

import { useState } from "react"
import { useAuth } from "@/contexts/auth-context"
import { Button } from "@/components/ui/button"
import { Input } from "@/components/ui/input"
import { Label } from "@/components/ui/label"
import { Card, CardContent, CardDescription, CardHeader, CardTitle } from "@/components/ui/card"
import { Alert, AlertDescription } from "@/components/ui/alert"
import { Loader2 } from "lucide-react"
import Link from "next/link"

export default function LoginPage() {
  const { signIn } = useAuth()
  const [email, setEmail] = useState("")
  const [password, setPassword] = useState("")
  const [error, setError] = useState("")
  const [loading, setLoading] = useState(false)

  const handleSubmit = async (e: React.FormEvent) => {
    e.preventDefault()
    setError("")
    setLoading(true)

    try {
      await signIn(email, password)
    } catch (err: any) {
      setError(err.message || "Failed to sign in")
    } finally {
      setLoading(false)
    }
  }

  return (
    <div className="flex min-h-screen items-center justify-center bg-gray-50">
      <Card className="w-full max-w-sm">
        <CardHeader className="space-y-1">
          <CardTitle className="text-xl">Sign in</CardTitle>
          <CardDescription className="text-xs">Enter your email and password to access the platform</CardDescription>
        </CardHeader>
        <CardContent>
          <form onSubmit={handleSubmit} className="space-y-3">
            {error && (
              <Alert variant="destructive">
                <AlertDescription className="text-xs">{error}</AlertDescription>
              </Alert>
            )}

            <div className="space-y-1">
              <Label htmlFor="email" className="text-xs">
                Email
              </Label>
              <Input
                id="email"
                type="email"
                placeholder="name@example.com"
                value={email}
                onChange={(e) => setEmail(e.target.value)}
                required
                className="h-8 text-xs"
              />
            </div>

            <div className="space-y-1">
              <Label htmlFor="password" className="text-xs">
                Password
              </Label>
              <Input
                id="password"
                type="password"
                value={password}
                onChange={(e) => setPassword(e.target.value)}
                required
                className="h-8 text-xs"
              />
            </div>

            <Button type="submit" className="h-8 w-full text-xs" disabled={loading}>
              {loading ? (
                <>
                  <Loader2 className="mr-2 h-3 w-3 animate-spin" />
                  Signing in...
                </>
              ) : (
                "Sign in"
              )}
            </Button>
          </form>

          <div className="mt-4 text-center text-xs text-gray-600">
            Don't have an account?{" "}
            <Link href="/signup" className="text-blue-600 hover:underline">
              Sign up
            </Link>
          </div>
        </CardContent>
      </Card>
    </div>
  )
}
```

## File: dkl-microapp-2-main/app/(auth)/register/page.tsx
```typescript
"use client"

import type React from "react"

import { useState } from "react"
import { useRouter } from "next/navigation"
import Link from "next/link"
import { useAuth } from "@/contexts/auth-context"
import { Button } from "@/components/ui/button"
import { Input } from "@/components/ui/input"
import { Label } from "@/components/ui/label"
import { AlertCircle } from "lucide-react"
import { Alert, AlertDescription } from "@/components/ui/alert"

export default function RegisterPage() {
  const router = useRouter()
  const { signUp } = useAuth()
  const [email, setEmail] = useState("")
  const [password, setPassword] = useState("")
  const [error, setError] = useState<string | null>(null)
  const [isLoading, setIsLoading] = useState(false)
  const [isSuccess, setIsSuccess] = useState(false)

  const handleSubmit = async (e: React.FormEvent) => {
    e.preventDefault()
    setError(null)
    setIsLoading(true)

    try {
      await signUp(email, password)
      setIsSuccess(true)
    } catch (error: any) {
      setError(error.message || "Failed to sign up")
    } finally {
      setIsLoading(false)
    }
  }

  if (isSuccess) {
    return (
      <div className="flex min-h-screen flex-col items-center justify-center">
        <div className="mx-auto flex w-full flex-col justify-center space-y-6 sm:w-[350px]">
          <div className="flex flex-col space-y-2 text-center">
            <h1 className="text-2xl font-semibold tracking-tight">Check your email</h1>
            <p className="text-sm text-muted-foreground">We&apos;ve sent you a confirmation link to {email}</p>
          </div>
          <Button asChild>
            <Link href="/login">Return to login</Link>
          </Button>
        </div>
      </div>
    )
  }

  return (
    <div className="flex min-h-screen flex-col items-center justify-center">
      <div className="mx-auto flex w-full flex-col justify-center space-y-6 sm:w-[350px]">
        <div className="flex flex-col space-y-2 text-center">
          <h1 className="text-2xl font-semibold tracking-tight">Create an account</h1>
          <p className="text-sm text-muted-foreground">Enter your email below to create your account</p>
        </div>
        <div className="grid gap-6">
          {error && (
            <Alert variant="destructive">
              <AlertCircle className="h-4 w-4" />
              <AlertDescription>{error}</AlertDescription>
            </Alert>
          )}
          <form onSubmit={handleSubmit}>
            <div className="grid gap-4">
              <div className="grid gap-2">
                <Label htmlFor="email">Email</Label>
                <Input
                  id="email"
                  placeholder="name@example.com"
                  type="email"
                  value={email}
                  onChange={(e) => setEmail(e.target.value)}
                  autoCapitalize="none"
                  autoComplete="email"
                  autoCorrect="off"
                  disabled={isLoading}
                  required
                />
              </div>
              <div className="grid gap-2">
                <Label htmlFor="password">Password</Label>
                <Input
                  id="password"
                  type="password"
                  value={password}
                  onChange={(e) => setPassword(e.target.value)}
                  autoCapitalize="none"
                  autoComplete="new-password"
                  autoCorrect="off"
                  disabled={isLoading}
                  required
                />
              </div>
              <Button type="submit" disabled={isLoading}>
                {isLoading ? "Creating account..." : "Create account"}
              </Button>
            </div>
          </form>
          <div className="text-center text-sm">
            Already have an account?{" "}
            <Link href="/login" className="text-primary underline-offset-4 hover:underline">
              Sign in
            </Link>
          </div>
        </div>
      </div>
    </div>
  )
}
```

## File: dkl-microapp-2-main/app/(auth)/signup/page.tsx
```typescript
"use client"

import type React from "react"

import { useState } from "react"
import { useAuth } from "@/contexts/auth-context"
import { Button } from "@/components/ui/button"
import { Input } from "@/components/ui/input"
import { Label } from "@/components/ui/label"
import { Card, CardContent, CardDescription, CardHeader, CardTitle } from "@/components/ui/card"
import { Alert, AlertDescription } from "@/components/ui/alert"
import { Loader2 } from "lucide-react"
import Link from "next/link"

export default function SignupPage() {
  const { signUp } = useAuth()
  const [email, setEmail] = useState("")
  const [password, setPassword] = useState("")
  const [confirmPassword, setConfirmPassword] = useState("")
  const [error, setError] = useState("")
  const [loading, setLoading] = useState(false)
  const [success, setSuccess] = useState(false)

  const handleSubmit = async (e: React.FormEvent) => {
    e.preventDefault()
    setError("")

    if (password !== confirmPassword) {
      setError("Passwords do not match")
      return
    }

    setLoading(true)

    try {
      await signUp(email, password)
      setSuccess(true)
    } catch (err: any) {
      setError(err.message || "Failed to sign up")
    } finally {
      setLoading(false)
    }
  }

  if (success) {
    return (
      <div className="flex min-h-screen items-center justify-center bg-gray-50">
        <Card className="w-full max-w-sm">
          <CardHeader>
            <CardTitle className="text-xl">Check your email</CardTitle>
            <CardDescription className="text-xs">We've sent a confirmation link to {email}</CardDescription>
          </CardHeader>
          <CardContent>
            <Link href="/login">
              <Button className="h-8 w-full text-xs">Back to login</Button>
            </Link>
          </CardContent>
        </Card>
      </div>
    )
  }

  return (
    <div className="flex min-h-screen items-center justify-center bg-gray-50">
      <Card className="w-full max-w-sm">
        <CardHeader className="space-y-1">
          <CardTitle className="text-xl">Create an account</CardTitle>
          <CardDescription className="text-xs">Enter your details to create your account</CardDescription>
        </CardHeader>
        <CardContent>
          <form onSubmit={handleSubmit} className="space-y-3">
            {error && (
              <Alert variant="destructive">
                <AlertDescription className="text-xs">{error}</AlertDescription>
              </Alert>
            )}

            <div className="space-y-1">
              <Label htmlFor="email" className="text-xs">
                Email
              </Label>
              <Input
                id="email"
                type="email"
                placeholder="name@example.com"
                value={email}
                onChange={(e) => setEmail(e.target.value)}
                required
                className="h-8 text-xs"
              />
            </div>

            <div className="space-y-1">
              <Label htmlFor="password" className="text-xs">
                Password
              </Label>
              <Input
                id="password"
                type="password"
                value={password}
                onChange={(e) => setPassword(e.target.value)}
                required
                className="h-8 text-xs"
              />
            </div>

            <div className="space-y-1">
              <Label htmlFor="confirmPassword" className="text-xs">
                Confirm Password
              </Label>
              <Input
                id="confirmPassword"
                type="password"
                value={confirmPassword}
                onChange={(e) => setConfirmPassword(e.target.value)}
                required
                className="h-8 text-xs"
              />
            </div>

            <Button type="submit" className="h-8 w-full text-xs" disabled={loading}>
              {loading ? (
                <>
                  <Loader2 className="mr-2 h-3 w-3 animate-spin" />
                  Creating account...
                </>
              ) : (
                "Sign up"
              )}
            </Button>
          </form>

          <div className="mt-4 text-center text-xs text-gray-600">
            Already have an account?{" "}
            <Link href="/login" className="text-blue-600 hover:underline">
              Sign in
            </Link>
          </div>
        </CardContent>
      </Card>
    </div>
  )
}
```

## File: dkl-microapp-2-main/app/(auth)/layout.tsx
```typescript
import type React from "react"
export default function AuthLayout({
  children,
}: {
  children: React.ReactNode
}) {
  return <>{children}</>
}
```

## File: dkl-microapp-2-main/app/(dashboard)/analytics/page.tsx
```typescript
"use client"

import { useEffect, useState } from "react"
import { supabase } from "@/lib/supabase/client"
import { Card, CardContent, CardHeader, CardTitle, CardDescription } from "@/components/ui/card"
import { formatCurrency } from "@/lib/utils"
import { BarChart3, TrendingUp, PieChartIcon as PieIcon, Activity, DollarSign, Home } from "lucide-react" // Renamed PieChart to PieIcon
import {
  ChartContainer,
  ChartTooltip,
  ChartTooltipContent,
  ChartLegend,
  ChartLegendContent,
} from "@/components/ui/chart"
import { Bar, XAxis, YAxis, CartesianGrid, ResponsiveContainer, PieChart, Pie, Cell, BarChart } from "recharts" // Recharts components

// ... (MetricCard and formatPriceRange remain the same for now, or can be refactored if needed)
function MetricCard({ title, value, icon: Icon, change }: any) {
  const isPositive = change > 0
  const isNegative = change < 0

  return (
    <Card>
      <CardHeader className="flex flex-row items-center justify-between space-y-0 pb-2">
        <CardTitle className="text-xs font-medium text-gray-600">{title}</CardTitle>
        <Icon className="h-3.5 w-3.5 text-gray-400" />
      </CardHeader>
      <CardContent>
        <div className="text-lg font-bold">{value}</div>
        {change !== undefined && (
          <p className="text-xs text-muted-foreground">
            <span
              className={`inline-flex items-center gap-x-1 ${
                isPositive ? "text-green-600" : isNegative ? "text-red-600" : "text-gray-600"
              }`}
            >
              {isPositive ? "▲" : isNegative ? "▼" : ""}
              {Math.abs(change)}% from last month
            </span>
          </p>
        )}
      </CardContent>
    </Card>
  )
}

function formatPriceRange(range: string): string {
  const ranges: Record<string, string> = {
    under500k: "Under $500K",
    "500k-1M": "$500K - $1M",
    "1M-2M": "$1M - $2M",
    "2M-5M": "$2M - $5M",
    over5M: "Over $5M",
  }
  return ranges[range] || range
}

const PRICE_RANGE_COLORS = [
  "hsl(var(--chart-1))",
  "hsl(var(--chart-2))",
  "hsl(var(--chart-3))",
  "hsl(var(--chart-4))",
  "hsl(var(--chart-5))",
]

export default function AnalyticsPage() {
  const [analytics, setAnalytics] = useState<any>(null)
  const [loading, setLoading] = useState(true)

  useEffect(() => {
    fetchAnalytics()
  }, [])

  async function fetchAnalytics() {
    setLoading(true)
    try {
      const { data: properties } = await supabase
        .from("listings")
        .select("list_price, interior_sqft, status, new_construction, city")
      const { data: builders } = await supabase.from("builders").select("id, name, company_name")

      if (!properties) {
        setAnalytics(null) // Or some default empty state
        return
      }
      if (properties.length === 0) {
        setAnalytics({
          totalProperties: 0,
          totalValue: 0,
          avgListPrice: 0,
          avgPricePerSqft: 0,
          activeListings: 0,
          newConstruction: 0,
          soldProperties: 0,
          priceRanges: {},
          cityStats: {},
          builderStats: [],
          inventoryTurnover: 0,
          newConstructionShare: 0,
        })
        return
      }

      const totalValue = properties.reduce((sum, p) => sum + (p.list_price || 0), 0)
      const propertiesWithPrice = properties.filter((p) => p.list_price != null && p.list_price > 0)
      const avgListPrice =
        propertiesWithPrice.length > 0
          ? propertiesWithPrice.reduce((sum, p) => sum + p.list_price!, 0) / propertiesWithPrice.length
          : 0

      const propertiesWithPriceAndSqft = properties.filter(
        (p) => p.list_price != null && p.list_price > 0 && p.interior_sqft != null && p.interior_sqft > 0,
      )
      const avgPricePerSqft =
        propertiesWithPriceAndSqft.length > 0
          ? propertiesWithPriceAndSqft.reduce((sum, p) => sum + p.list_price! / p.interior_sqft!, 0) /
            propertiesWithPriceAndSqft.length
          : 0

      const activeListings = properties.filter((p) => p.status === "Active")
      const newConstructionProps = properties.filter((p) => p.new_construction)
      const soldProperties = properties.filter((p) => p.status === "Sold")

      const priceRangesData = [
        {
          name: "Under $500K",
          value: properties.filter((p) => (p.list_price || 0) < 500000).length,
          fill: PRICE_RANGE_COLORS[0],
        },
        {
          name: "$500K - $1M",
          value: properties.filter((p) => (p.list_price || 0) >= 500000 && (p.list_price || 0) < 1000000).length,
          fill: PRICE_RANGE_COLORS[1],
        },
        {
          name: "$1M - $2M",
          value: properties.filter((p) => (p.list_price || 0) >= 1000000 && (p.list_price || 0) < 2000000).length,
          fill: PRICE_RANGE_COLORS[2],
        },
        {
          name: "$2M - $5M",
          value: properties.filter((p) => (p.list_price || 0) >= 2000000 && (p.list_price || 0) < 5000000).length,
          fill: PRICE_RANGE_COLORS[3],
        },
        {
          name: "Over $5M",
          value: properties.filter((p) => (p.list_price || 0) >= 5000000).length,
          fill: PRICE_RANGE_COLORS[4],
        },
      ].filter((range) => range.value > 0)

      const cityStats = properties.reduce((acc: any, p) => {
        const city = p.city || "Unknown"
        if (!acc[city]) {
          acc[city] = { name: city, count: 0, totalValue: 0, avgPrice: 0 }
        }
        acc[city].count++
        acc[city].totalValue += p.list_price || 0
        acc[city].avgPrice = acc[city].totalValue / acc[city].count
        return acc
      }, {})
      const cityChartData = Object.values(cityStats)
        .sort((a: any, b: any) => b.totalValue - a.totalValue)
        .slice(0, 6)

      const builderStats = await Promise.all(
        (builders || []).map(async (builder) => {
          const { data: builderProperties, error } = await supabase
            .from("listings")
            .select("list_price")
            .eq("builder_id", builder.id)
          if (error) {
            console.error(`Error fetching properties for builder ${builder.id}:`, error)
            return { ...builder, propertyCount: 0, totalValue: 0, avgPrice: 0 }
          }

          return {
            ...builder,
            propertyCount: builderProperties?.length || 0,
            totalValue: builderProperties?.reduce((sum, p) => sum + (p.list_price || 0), 0) || 0,
            avgPrice: builderProperties?.length
              ? builderProperties.reduce((sum, p) => sum + (p.list_price || 0), 0) / builderProperties.length
              : 0,
          }
        }),
      )

      setAnalytics({
        totalProperties: properties.length,
        totalValue,
        avgListPrice,
        avgPricePerSqft,
        activeListings: activeListings.length,
        newConstruction: newConstructionProps.length,
        soldProperties: soldProperties.length,
        priceRangesChartData: priceRangesData,
        cityChartData: cityChartData,
        builderStats: builderStats.sort((a, b) => b.totalValue - a.totalValue),
        inventoryTurnover: properties.length > 0 ? (soldProperties.length / properties.length) * 100 : 0,
        newConstructionShare: properties.length > 0 ? (newConstructionProps.length / properties.length) * 100 : 0,
      })
    } catch (error) {
      console.error("Error fetching analytics:", error)
    } finally {
      setLoading(false)
    }
  }

  if (loading) {
    return (
      <div className="space-y-4 p-4 md:p-6">
        <div className="h-8 bg-muted rounded w-1/4 animate-pulse mb-2"></div>
        <div className="h-4 bg-muted rounded w-1/2 animate-pulse"></div>
        <div className="grid gap-4 md:grid-cols-2 lg:grid-cols-4 mt-4">
          {[...Array(4)].map((_, i) => (
            <Card key={i} className="h-28 animate-pulse bg-muted/50"></Card>
          ))}
        </div>
        <div className="grid gap-4 lg:grid-cols-2 mt-4">
          <Card className="h-72 animate-pulse bg-muted/50"></Card>
          <Card className="h-72 animate-pulse bg-muted/50"></Card>
        </div>
      </div>
    )
  }

  if (!analytics) {
    return <div className="p-4 md:p-6 text-center text-muted-foreground">No analytics data available.</div>
  }

  return (
    <div className="space-y-6 p-4 md:p-6">
      <div>
        <h1 className="text-2xl font-semibold">Market Analytics</h1>
        <p className="text-sm text-muted-foreground">Advanced market analytics and performance metrics</p>
      </div>

      <div className="grid gap-4 md:grid-cols-2 lg:grid-cols-4">
        <MetricCard
          title="Total Portfolio Value"
          value={formatCurrency(analytics?.totalValue)}
          icon={DollarSign}
          change={analytics?.totalValue > 1000000 ? 8.5 : undefined} // Example change
        />
        <MetricCard
          title="Avg List Price"
          value={formatCurrency(analytics?.avgListPrice)}
          icon={Home}
          change={analytics?.avgListPrice > 100000 ? 3.2 : undefined}
        />
        <MetricCard
          title="Avg Price/SqFt"
          value={formatCurrency(analytics?.avgPricePerSqft)}
          icon={TrendingUp}
          change={analytics?.avgPricePerSqft > 100 ? 5.1 : undefined}
        />
        <MetricCard
          title="Inventory Turnover"
          value={`${analytics?.inventoryTurnover?.toFixed(1)}%`}
          icon={Activity}
          change={analytics?.inventoryTurnover > 10 ? -2.3 : undefined}
        />
      </div>

      <div className="grid gap-6 lg:grid-cols-2">
        <Card>
          <CardHeader>
            <CardTitle className="text-base flex items-center gap-x-2">
              <PieIcon className="h-5 w-5 text-primary" />
              Price Distribution
            </CardTitle>
            <CardDescription>Distribution of listings by list price ranges.</CardDescription>
          </CardHeader>
          <CardContent>
            <ChartContainer config={{}} className="mx-auto aspect-square max-h-[300px]">
              <PieChart>
                <ChartTooltip content={<ChartTooltipContent nameKey="name" hideLabel />} />
                <Pie
                  data={analytics.priceRangesChartData}
                  dataKey="value"
                  nameKey="name"
                  labelLine={false}
                  label={({ cx, cy, midAngle, innerRadius, outerRadius, percent, index }) => {
                    const RADIAN = Math.PI / 180
                    const radius = innerRadius + (outerRadius - innerRadius) * 0.5
                    const x = cx + radius * Math.cos(-midAngle * RADIAN)
                    const y = cy + radius * Math.sin(-midAngle * RADIAN)
                    return percent * 100 > 5 ? ( // Only show label if percent is > 5%
                      <text
                        x={x}
                        y={y}
                        fill="white"
                        textAnchor={x > cx ? "start" : "end"}
                        dominantBaseline="central"
                        fontSize="10px"
                      >
                        {`${(percent * 100).toFixed(0)}%`}
                      </text>
                    ) : null
                  }}
                >
                  {analytics.priceRangesChartData.map((entry: any, index: number) => (
                    <Cell key={`cell-${index}`} fill={entry.fill} />
                  ))}
                </Pie>
                <ChartLegend
                  content={<ChartLegendContent nameKey="name" />}
                  className="-translate-y-2 flex-wrap gap-2 [&>*]:basis-1/4 [&>*]:justify-center"
                />
              </PieChart>
            </ChartContainer>
          </CardContent>
        </Card>

        <Card>
          <CardHeader>
            <CardTitle className="text-base flex items-center gap-x-2">
              <BarChart3 className="h-5 w-5 text-primary" />
              Top Markets by Value
            </CardTitle>
            <CardDescription>Total listing value by city (Top 6).</CardDescription>
          </CardHeader>
          <CardContent>
            <ChartContainer
              config={{
                totalValue: { label: "Total Value", color: "hsl(var(--chart-1))" },
              }}
              className="h-[300px] w-full"
            >
              <ResponsiveContainer width="100%" height="100%">
                <BarChart data={analytics.cityChartData} layout="vertical" margin={{ left: 10, right: 30 }}>
                  <CartesianGrid horizontal={false} />
                  <XAxis
                    type="number"
                    dataKey="totalValue"
                    tickFormatter={(value) => `$${(value / 1000000).toFixed(0)}M`}
                  />
                  <YAxis type="category" dataKey="name" width={80} tickLine={false} axisLine={false} />
                  <ChartTooltip cursor={false} content={<ChartTooltipContent indicator="line" />} />
                  <Bar dataKey="totalValue" radius={5}>
                    {analytics.cityChartData.map((entry: any, index: number) => (
                      <Cell key={`cell-${index}`} fill={PRICE_RANGE_COLORS[index % PRICE_RANGE_COLORS.length]} />
                    ))}
                  </Bar>
                </BarChart>
              </ResponsiveContainer>
            </ChartContainer>
          </CardContent>
        </Card>
      </div>

      <Card>
        <CardHeader>
          <CardTitle className="text-base">Top Builder Performance</CardTitle>
          <CardDescription>Overview of top builders by total listing value.</CardDescription>
        </CardHeader>
        <CardContent>
          <div className="space-y-3">
            {analytics?.builderStats?.slice(0, 5).map((builder: any) => (
              <div
                key={builder.id}
                className="flex flex-col sm:flex-row justify-between items-start sm:items-center p-3 border rounded-lg hover:bg-muted/50"
              >
                <div>
                  <div className="text-sm font-medium text-primary">{builder.name}</div>
                  <div className="text-xs text-muted-foreground">{builder.company_name}</div>
                </div>
                <div className="flex gap-4 mt-2 sm:mt-0 text-xs text-right">
                  <div>
                    <div className="text-muted-foreground">Listings</div>
                    <div className="font-medium">{builder.propertyCount}</div>
                  </div>
                  <div>
                    <div className="text-muted-foreground">Avg Price</div>
                    <div className="font-medium">{formatCurrency(builder.avgPrice)}</div>
                  </div>
                  <div>
                    <div className="text-muted-foreground">Total Value</div>
                    <div className="font-medium">{formatCurrency(builder.totalValue)}</div>
                  </div>
                </div>
              </div>
            ))}
            {analytics?.builderStats?.length === 0 && (
              <p className="text-sm text-muted-foreground text-center py-4">No builder data available.</p>
            )}
          </div>
        </CardContent>
      </Card>
    </div>
  )
}
```

## File: dkl-microapp-2-main/app/(dashboard)/builders/[id]/edit/page.tsx
```typescript
"use client"

import type React from "react"

import { useState, useEffect } from "react"
import { useParams, useRouter } from "next/navigation"
import { supabase } from "@/lib/supabase/client"
import { Card, CardContent, CardHeader, CardTitle } from "@/components/ui/card"
import { Button } from "@/components/ui/button"
import { Input } from "@/components/ui/input"
import { Label } from "@/components/ui/label"
import { Textarea } from "@/components/ui/textarea"
import { ArrowLeft, Save } from "lucide-react"
import Link from "next/link"
import { useToast } from "@/hooks/use-toast"

export default function EditBuilderPage() {
  const params = useParams()
  const router = useRouter()
  const { toast } = useToast()
  const [loading, setLoading] = useState(false)
  const [initialLoading, setInitialLoading] = useState(true)
  const [formData, setFormData] = useState({
    name: "",
    company_name: "",
    phone: "",
    email: "",
    website: "",
    address: "",
    city: "",
    state: "",
    zip_code: "",
    years_in_business: "",
    total_projects: "",
    active_projects: "",
    price_range_min: "",
    price_range_max: "",
    specialties: "",
    notes: "",
  })

  useEffect(() => {
    if (params.id) {
      fetchBuilder()
    }
  }, [params.id])

  async function fetchBuilder() {
    try {
      const { data, error } = await supabase.from("builders").select("*").eq("id", params.id).single()

      if (error) throw error

      setFormData({
        name: data.name || "",
        company_name: data.company_name || "",
        phone: data.phone || "",
        email: data.email || "",
        website: data.website || "",
        address: data.address || "",
        city: data.city || "",
        state: data.state || "",
        zip_code: data.zip_code || "",
        years_in_business: data.years_in_business?.toString() || "",
        total_projects: data.total_projects?.toString() || "",
        active_projects: data.active_projects?.toString() || "",
        price_range_min: data.price_range_min?.toString() || "",
        price_range_max: data.price_range_max?.toString() || "",
        specialties: data.specialties?.join(", ") || "",
        notes: data.notes || "",
      })
    } catch (error) {
      console.error("Error fetching builder:", error)
      toast({
        title: "Error",
        description: "Failed to load builder data.",
        variant: "destructive",
      })
    } finally {
      setInitialLoading(false)
    }
  }

  const handleSubmit = async (e: React.FormEvent) => {
    e.preventDefault()
    setLoading(true)

    try {
      // Convert string numbers to actual numbers and process specialties
      const builderData = {
        ...formData,
        years_in_business: formData.years_in_business ? Number.parseInt(formData.years_in_business) : null,
        total_projects: formData.total_projects ? Number.parseInt(formData.total_projects) : null,
        active_projects: formData.active_projects ? Number.parseInt(formData.active_projects) : null,
        price_range_min: formData.price_range_min ? Number.parseFloat(formData.price_range_min) : null,
        price_range_max: formData.price_range_max ? Number.parseFloat(formData.price_range_max) : null,
        specialties: formData.specialties
          ? formData.specialties
              .split(",")
              .map((s) => s.trim())
              .filter(Boolean)
          : null,
      }

      const { error } = await supabase.from("builders").update(builderData).eq("id", params.id)

      if (error) throw error

      toast({
        title: "Builder updated",
        description: "Builder has been successfully updated.",
      })

      router.push(`/builders/${params.id}`)
    } catch (error: any) {
      toast({
        title: "Error",
        description: error.message || "Failed to update builder.",
        variant: "destructive",
      })
    } finally {
      setLoading(false)
    }
  }

  if (initialLoading) {
    return <div className="text-xs text-gray-600">Loading...</div>
  }

  return (
    <div className="space-y-4">
      <div className="flex items-center gap-x-2">
        <Button variant="ghost" size="sm" asChild>
          <Link href={`/builders/${params.id}`}>
            <ArrowLeft className="h-4 w-4" />
          </Link>
        </Button>
        <h1 className="text-lg font-semibold">Edit Builder</h1>
      </div>

      <form onSubmit={handleSubmit}>
        <div className="grid gap-4 lg:grid-cols-2">
          <Card>
            <CardHeader>
              <CardTitle className="text-sm">Basic Information</CardTitle>
            </CardHeader>
            <CardContent className="space-y-3">
              <div>
                <Label htmlFor="name" className="text-xs">
                  Builder Name *
                </Label>
                <Input
                  id="name"
                  value={formData.name}
                  onChange={(e) => setFormData({ ...formData, name: e.target.value })}
                  className="h-8 text-xs"
                  required
                />
              </div>

              <div>
                <Label htmlFor="company_name" className="text-xs">
                  Company Name
                </Label>
                <Input
                  id="company_name"
                  value={formData.company_name}
                  onChange={(e) => setFormData({ ...formData, company_name: e.target.value })}
                  className="h-8 text-xs"
                />
              </div>

              <div>
                <Label htmlFor="phone" className="text-xs">
                  Phone
                </Label>
                <Input
                  id="phone"
                  value={formData.phone}
                  onChange={(e) => setFormData({ ...formData, phone: e.target.value })}
                  className="h-8 text-xs"
                />
              </div>

              <div>
                <Label htmlFor="email" className="text-xs">
                  Email
                </Label>
                <Input
                  id="email"
                  type="email"
                  value={formData.email}
                  onChange={(e) => setFormData({ ...formData, email: e.target.value })}
                  className="h-8 text-xs"
                />
              </div>

              <div>
                <Label htmlFor="website" className="text-xs">
                  Website
                </Label>
                <Input
                  id="website"
                  value={formData.website}
                  onChange={(e) => setFormData({ ...formData, website: e.target.value })}
                  className="h-8 text-xs"
                  placeholder="https://"
                />
              </div>
            </CardContent>
          </Card>

          <Card>
            <CardHeader>
              <CardTitle className="text-sm">Address</CardTitle>
            </CardHeader>
            <CardContent className="space-y-3">
              <div>
                <Label htmlFor="address" className="text-xs">
                  Street Address
                </Label>
                <Input
                  id="address"
                  value={formData.address}
                  onChange={(e) => setFormData({ ...formData, address: e.target.value })}
                  className="h-8 text-xs"
                />
              </div>

              <div>
                <Label htmlFor="city" className="text-xs">
                  City
                </Label>
                <Input
                  id="city"
                  value={formData.city}
                  onChange={(e) => setFormData({ ...formData, city: e.target.value })}
                  className="h-8 text-xs"
                />
              </div>

              <div className="grid grid-cols-2 gap-2">
                <div>
                  <Label htmlFor="state" className="text-xs">
                    State
                  </Label>
                  <Input
                    id="state"
                    value={formData.state}
                    onChange={(e) => setFormData({ ...formData, state: e.target.value })}
                    className="h-8 text-xs"
                    placeholder="VA"
                  />
                </div>
                <div>
                  <Label htmlFor="zip_code" className="text-xs">
                    Zip Code
                  </Label>
                  <Input
                    id="zip_code"
                    value={formData.zip_code}
                    onChange={(e) => setFormData({ ...formData, zip_code: e.target.value })}
                    className="h-8 text-xs"
                  />
                </div>
              </div>
            </CardContent>
          </Card>

          <Card>
            <CardHeader>
              <CardTitle className="text-sm">Business Details</CardTitle>
            </CardHeader>
            <CardContent className="space-y-3">
              <div>
                <Label htmlFor="years_in_business" className="text-xs">
                  Years in Business
                </Label>
                <Input
                  id="years_in_business"
                  type="number"
                  value={formData.years_in_business}
                  onChange={(e) => setFormData({ ...formData, years_in_business: e.target.value })}
                  className="h-8 text-xs"
                />
              </div>

              <div className="grid grid-cols-2 gap-2">
                <div>
                  <Label htmlFor="total_projects" className="text-xs">
                    Total Projects
                  </Label>
                  <Input
                    id="total_projects"
                    type="number"
                    value={formData.total_projects}
                    onChange={(e) => setFormData({ ...formData, total_projects: e.target.value })}
                    className="h-8 text-xs"
                  />
                </div>
                <div>
                  <Label htmlFor="active_projects" className="text-xs">
                    Active Projects
                  </Label>
                  <Input
                    id="active_projects"
                    type="number"
                    value={formData.active_projects}
                    onChange={(e) => setFormData({ ...formData, active_projects: e.target.value })}
                    className="h-8 text-xs"
                  />
                </div>
              </div>

              <div className="grid grid-cols-2 gap-2">
                <div>
                  <Label htmlFor="price_range_min" className="text-xs">
                    Min Price Range
                  </Label>
                  <Input
                    id="price_range_min"
                    type="number"
                    value={formData.price_range_min}
                    onChange={(e) => setFormData({ ...formData, price_range_min: e.target.value })}
                    className="h-8 text-xs"
                  />
                </div>
                <div>
                  <Label htmlFor="price_range_max" className="text-xs">
                    Max Price Range
                  </Label>
                  <Input
                    id="price_range_max"
                    type="number"
                    value={formData.price_range_max}
                    onChange={(e) => setFormData({ ...formData, price_range_max: e.target.value })}
                    className="h-8 text-xs"
                  />
                </div>
              </div>
            </CardContent>
          </Card>

          <Card>
            <CardHeader>
              <CardTitle className="text-sm">Additional Information</CardTitle>
            </CardHeader>
            <CardContent className="space-y-3">
              <div>
                <Label htmlFor="specialties" className="text-xs">
                  Specialties
                </Label>
                <Input
                  id="specialties"
                  value={formData.specialties}
                  onChange={(e) => setFormData({ ...formData, specialties: e.target.value })}
                  className="h-8 text-xs"
                  placeholder="Luxury Homes, Custom Builds (comma separated)"
                />
              </div>

              <div>
                <Label htmlFor="notes" className="text-xs">
                  Notes
                </Label>
                <Textarea
                  id="notes"
                  value={formData.notes}
                  onChange={(e) => setFormData({ ...formData, notes: e.target.value })}
                  className="text-xs"
                  rows={3}
                />
              </div>
            </CardContent>
          </Card>
        </div>

        <div className="flex justify-end gap-x-2 mt-4">
          <Button type="button" variant="outline" asChild>
            <Link href={`/builders/${params.id}`}>Cancel</Link>
          </Button>
          <Button type="submit" disabled={loading}>
            {loading ? (
              "Updating..."
            ) : (
              <>
                <Save className="mr-2 h-4 w-4" />
                Update Builder
              </>
            )}
          </Button>
        </div>
      </form>
    </div>
  )
}
```

## File: dkl-microapp-2-main/app/(dashboard)/builders/[id]/page.tsx
```typescript
"use client"

import React from "react"

import { useEffect, useState } from "react"
import { useParams } from "next/navigation"
import { supabase } from "@/lib/supabase/client"
import { Card, CardContent, CardHeader, CardTitle, CardDescription } from "@/components/ui/card"
import { Button } from "@/components/ui/button"
import { Badge } from "@/components/ui/badge"
import { Select, SelectContent, SelectItem, SelectTrigger, SelectValue } from "@/components/ui/select"
import { DataTable } from "@/components/ui/data-table" // Assuming this is the enhanced one
import { formatCurrency, formatNumber, formatDate, getFullAddress, getStatusColor } from "@/lib/utils"
import { ArrowLeft, Edit, Building2, Phone, Mail, Globe, BarChartIcon } from "lucide-react"
import Link from "next/link"
import type { ColumnDef } from "@tanstack/react-table"
import { DataTableColumnHeader } from "@/components/ui/data-table-column-header"
import { ChartContainer, ChartTooltip, ChartTooltipContent } from "@/components/ui/chart"
import { BarChart, Bar, XAxis, YAxis, CartesianGrid, ResponsiveContainer, Cell } from "recharts"
import type { Database } from "@/types/supabase"

type Listing = Database["public"]["Tables"]["listings"]["Row"]
type Builder = Database["public"]["Tables"]["builders"]["Row"]

const LISTING_CHART_COLORS = [
  "hsl(var(--chart-1))",
  "hsl(var(--chart-2))",
  "hsl(var(--chart-3))",
  "hsl(var(--chart-4))",
  "hsl(var(--chart-5))",
]

export default function BuilderDetailPage() {
  const params = useParams()
  const builderId = params.id as string
  const [builder, setBuilder] = useState<Builder | null>(null)
  const [listings, setListings] = useState<Listing[]>([])
  const [loading, setLoading] = useState(true)
  const [timeRange, setTimeRange] = useState("all")

  useEffect(() => {
    if (builderId) {
      fetchBuilderData()
    }
  }, [builderId, timeRange]) // Re-fetch if timeRange changes for properties

  async function fetchBuilderData() {
    setLoading(true)
    try {
      const { data: builderData, error: builderError } = await supabase
        .from("builders")
        .select("*")
        .eq("id", builderId)
        .single()

      if (builderError) throw builderError
      setBuilder(builderData)

      let query = supabase
        .from("listings")
        .select("*")
        .eq("builder_id", builderId)
        .order("list_date", { ascending: false })

      if (timeRange !== "all") {
        const now = new Date()
        let cutoffDate: Date | null = null
        switch (timeRange) {
          case "3m":
            cutoffDate = new Date(now.getFullYear(), now.getMonth() - 3, now.getDate())
            break
          case "6m":
            cutoffDate = new Date(now.getFullYear(), now.getMonth() - 6, now.getDate())
            break
          case "1y":
            cutoffDate = new Date(now.getFullYear() - 1, now.getMonth(), now.getDate())
            break
          case "3y":
            cutoffDate = new Date(now.getFullYear() - 3, now.getMonth(), now.getDate())
            break
          case "5y":
            cutoffDate = new Date(now.getFullYear() - 5, now.getMonth(), now.getDate())
            break
        }
        if (cutoffDate) {
          query = query.gte("list_date", cutoffDate.toISOString().split("T")[0])
        }
      }

      const { data: listingsData, error: listingsError } = await query
      if (listingsError) throw listingsError
      setListings(listingsData || [])
    } catch (error) {
      console.error("Error fetching builder data:", error)
      setBuilder(null) // Reset on error
      setListings([])
    } finally {
      setLoading(false)
    }
  }

  const chartData = listings
    .filter((p) => p.list_date && p.list_price)
    .map((property) => ({
      date: new Date(property.list_date as string), // Ensure list_date is string
      price: property.list_price,
      mls: property.mls_number,
      // For tooltip:
      name: `${property.mls_number} - ${formatDate(property.list_date as string)}`,
      value: property.list_price,
    }))
    .sort((a, b) => a.date.getTime() - b.date.getTime())

  const listingColumns = React.useMemo<ColumnDef<Listing>[]>(
    () => [
      {
        accessorKey: "mls_number",
        header: ({ column }) => <DataTableColumnHeader column={column} title="MLS #" />,
        cell: ({ row }) => (
          <Link href={`/listings/${row.original.id}`} className="font-medium hover:underline text-xs text-primary">
            {row.getValue("mls_number") || "-"}
          </Link>
        ),
      },
      {
        accessorKey: "status",
        header: ({ column }) => <DataTableColumnHeader column={column} title="Status" />,
        cell: ({ row }) => {
          const status = row.getValue("status") as string
          return status ? (
            <Badge variant="secondary" className={`text-[10px] px-1.5 py-0 ${getStatusColor(status)}`}>
              {status}
            </Badge>
          ) : (
            "-"
          )
        },
      },
      {
        accessorKey: "address",
        header: ({ column }) => <DataTableColumnHeader column={column} title="Address" />,
        cell: ({ row }) => <div className="max-w-xs truncate text-xs">{getFullAddress(row.original)}</div>,
      },
      {
        accessorKey: "list_price",
        header: ({ column }) => <DataTableColumnHeader column={column} title="List Price" />,
        cell: ({ row }) => <span className="text-xs">{formatCurrency(row.getValue("list_price"))}</span>,
      },
      {
        accessorKey: "list_date",
        header: ({ column }) => <DataTableColumnHeader column={column} title="Listed" />,
        cell: ({ row }) => <span className="text-xs">{formatDate(row.getValue("list_date"))}</span>,
      },
    ],
    [],
  )

  if (loading) {
    return (
      <div className="space-y-4 p-4 md:p-6">
        <div className="h-8 bg-muted rounded w-1/3 animate-pulse mb-2"></div>
        <div className="grid gap-4 lg:grid-cols-3">
          {[...Array(3)].map((_, i) => (
            <Card key={i} className="h-36 animate-pulse bg-muted/50"></Card>
          ))}
        </div>
        <Card className="h-72 animate-pulse bg-muted/50"></Card>
        <Card className="h-96 animate-pulse bg-muted/50"></Card>
      </div>
    )
  }

  if (!builder) {
    return <div className="p-4 md:p-6 text-center text-muted-foreground">Builder not found or failed to load.</div>
  }

  const totalPropertyValue = listings.reduce((sum, l) => sum + (l.list_price || 0), 0)
  const avgPropertyValue = listings.length > 0 ? totalPropertyValue / listings.length : 0

  return (
    <div className="space-y-6 p-4 md:p-6">
      <div className="flex items-center justify-between">
        <div className="flex items-center gap-x-3">
          <Button variant="outline" size="icon" className="h-8 w-8" asChild>
            <Link href="/builders">
              <ArrowLeft className="h-4 w-4" />
              <span className="sr-only">Back to Builders</span>
            </Link>
          </Button>
          <div>
            <h1 className="text-2xl font-semibold">{builder.name}</h1>
            {builder.company_name && <p className="text-sm text-muted-foreground">{builder.company_name}</p>}
          </div>
        </div>
        <Button size="sm" className="h-8 text-xs" asChild>
          <Link href={`/builders/${builderId}/edit`}>
            <Edit className="mr-1.5 h-3.5 w-3.5" />
            Edit Builder
          </Link>
        </Button>
      </div>

      <div className="grid gap-4 md:grid-cols-2 lg:grid-cols-3">
        <Card>
          <CardHeader>
            <CardTitle className="text-base">Contact Information</CardTitle>
          </CardHeader>
          <CardContent className="space-y-2 text-sm">
            {builder.phone && (
              <div className="flex items-center gap-x-2">
                <Phone className="h-4 w-4 text-muted-foreground" />
                <span>{builder.phone}</span>
              </div>
            )}
            {builder.email && (
              <div className="flex items-center gap-x-2">
                <Mail className="h-4 w-4 text-muted-foreground" />
                <a href={`mailto:${builder.email}`} className="text-primary hover:underline">
                  {builder.email}
                </a>
              </div>
            )}
            {builder.website && (
              <div className="flex items-center gap-x-2">
                <Globe className="h-4 w-4 text-muted-foreground" />
                <a
                  href={builder.website}
                  target="_blank"
                  rel="noopener noreferrer"
                  className="text-primary hover:underline truncate"
                >
                  {builder.website.replace(/^https?:\/\//, "")}
                </a>
              </div>
            )}
            {builder.address && (
              <div className="flex items-start gap-x-2">
                <Building2 className="h-4 w-4 text-muted-foreground mt-0.5" />
                <span>
                  {builder.address}
                  {builder.city && `, ${builder.city}`}
                  {builder.state && `, ${builder.state}`} {builder.zip_code}
                </span>
              </div>
            )}
          </CardContent>
        </Card>

        <Card>
          <CardHeader>
            <CardTitle className="text-base">Builder Stats</CardTitle>
          </CardHeader>
          <CardContent className="space-y-1.5 text-sm">
            <div className="flex justify-between">
              <span>Years in Business:</span> <span className="font-medium">{builder.years_in_business || "-"}</span>
            </div>
            <div className="flex justify-between">
              <span>Total Projects:</span> <span className="font-medium">{formatNumber(builder.total_projects)}</span>
            </div>
            <div className="flex justify-between">
              <span>Active Projects:</span> <span className="font-medium">{formatNumber(builder.active_projects)}</span>
            </div>
            <div className="flex justify-between">
              <span>Listings in DB:</span> <span className="font-medium">{listings.length}</span>
            </div>
            {builder.rating && (
              <div className="flex justify-between">
                <span>Rating:</span> <Badge variant="secondary">★ {builder.rating}</Badge>
              </div>
            )}
          </CardContent>
        </Card>

        <Card>
          <CardHeader>
            <CardTitle className="text-base">Financials</CardTitle>
          </CardHeader>
          <CardContent className="space-y-1.5 text-sm">
            <div className="flex justify-between">
              <span>Min Price Range:</span>{" "}
              <span className="font-medium">{formatCurrency(builder.price_range_min)}</span>
            </div>
            <div className="flex justify-between">
              <span>Max Price Range:</span>{" "}
              <span className="font-medium">{formatCurrency(builder.price_range_max)}</span>
            </div>
            <div className="flex justify-between">
              <span>Avg. Listing (DB):</span> <span className="font-medium">{formatCurrency(avgPropertyValue)}</span>
            </div>
            <div className="flex justify-between">
              <span>Total Value (DB):</span> <span className="font-medium">{formatCurrency(totalPropertyValue)}</span>
            </div>
          </CardContent>
        </Card>

        {builder.specialties && (builder.specialties as string[]).length > 0 && (
          <Card className="md:col-span-2 lg:col-span-1">
            <CardHeader>
              <CardTitle className="text-base">Specialties</CardTitle>
            </CardHeader>
            <CardContent>
              <div className="flex flex-wrap gap-2">
                {(builder.specialties as string[]).map((specialty: string, index: number) => (
                  <Badge key={index} variant="outline">
                    {specialty}
                  </Badge>
                ))}
              </div>
            </CardContent>
          </Card>
        )}
      </div>

      <Card>
        <CardHeader className="flex flex-row items-center justify-between">
          <div>
            <CardTitle className="text-base flex items-center gap-x-2">
              <BarChartIcon className="h-5 w-5 text-primary" />
              Listings Over Time
            </CardTitle>
            <CardDescription>Price of properties listed by this builder.</CardDescription>
          </div>
          <Select value={timeRange} onValueChange={setTimeRange}>
            <SelectTrigger className="w-36 h-8 text-xs">
              <SelectValue placeholder="Select time range" />
            </SelectTrigger>
            <SelectContent>
              <SelectItem value="3m">Last 3 Months</SelectItem>
              <SelectItem value="6m">Last 6 Months</SelectItem>
              <SelectItem value="1y">Last Year</SelectItem>
              <SelectItem value="3y">Last 3 Years</SelectItem>
              <SelectItem value="5y">Last 5 Years</SelectItem>
              <SelectItem value="all">All Time</SelectItem>
            </SelectContent>
          </Select>
        </CardHeader>
        <CardContent>
          {chartData.length > 0 ? (
            <ChartContainer
              config={{ price: { label: "Price", color: "hsl(var(--chart-1))" } }}
              className="h-[300px] w-full"
            >
              <ResponsiveContainer width="100%" height="100%">
                <BarChart data={chartData} margin={{ top: 5, right: 20, left: 20, bottom: 5 }}>
                  <CartesianGrid strokeDasharray="3 3" vertical={false} />
                  <XAxis
                    dataKey="date"
                    tickFormatter={(value) =>
                      new Date(value).toLocaleDateString("en-US", { month: "short", year: "2-digit" })
                    }
                    angle={-45}
                    textAnchor="end"
                    height={50}
                    interval="preserveStartEnd"
                  />
                  <YAxis tickFormatter={(value) => `$${(value / 1000000).toFixed(1)}M`} />
                  <ChartTooltip
                    cursor={false}
                    content={
                      <ChartTooltipContent
                        formatter={(value, name) => (name === "price" ? formatCurrency(value as number) : value)}
                        labelFormatter={(label, payload) =>
                          payload?.[0]?.payload.name || new Date(label).toLocaleDateString()
                        }
                      />
                    }
                  />
                  <Bar dataKey="price" radius={4}>
                    {chartData.map((entry, index) => (
                      <Cell key={`cell-${index}`} fill={LISTING_CHART_COLORS[index % LISTING_CHART_COLORS.length]} />
                    ))}
                  </Bar>
                </BarChart>
              </ResponsiveContainer>
            </ChartContainer>
          ) : (
            <div className="h-[300px] flex items-center justify-center text-muted-foreground text-sm">
              No listings found for the selected time range.
            </div>
          )}
        </CardContent>
      </Card>

      <Card>
        <CardHeader>
          <CardTitle className="text-base">Associated Listings ({listings.length})</CardTitle>
          <CardDescription>All listings by this builder in the database.</CardDescription>
        </CardHeader>
        <CardContent>
          <DataTable columns={listingColumns} data={listings} loading={loading} />
        </CardContent>
      </Card>

      {/* Map placeholder can remain or be enhanced later */}
      <Card>
        <CardHeader>
          <CardTitle className="text-base">Listing Locations (Placeholder)</CardTitle>
        </CardHeader>
        <CardContent>
          <div className="h-64 bg-muted border rounded flex items-center justify-center text-muted-foreground">
            Map integration coming soon
          </div>
        </CardContent>
      </Card>
    </div>
  )
}
```

## File: dkl-microapp-2-main/app/(dashboard)/builders/loading.tsx
```typescript
export default function Loading() {
  return null
}
```

## File: dkl-microapp-2-main/app/(dashboard)/builders/page.tsx
```typescript
"use client"

import * as React from "react" // Changed from useEffect, useState
import { supabase } from "@/lib/supabase/client"
import { Input } from "@/components/ui/input" // Keep for search
import { Button } from "@/components/ui/button"
import { Card, CardContent, CardDescription, CardFooter, CardHeader, CardTitle } from "@/components/ui/card"
import { Badge } from "@/components/ui/badge"
import { Plus, Building2, Phone, Mail, Globe, Edit, Trash2 } from "lucide-react" // Added Edit, Trash2
import Link from "next/link" // Keep for builder name link
import type { Database } from "@/types/supabase"
import { BuilderFormDialog } from "@/components/builder-form-dialog" // Import new dialog
import { useToast } from "@/hooks/use-toast" // For delete action

type Builder = Database["public"]["Tables"]["builders"]["Row"] & {
  listings_count?: number // Renamed from properties_count
}

function BuilderCard({
  builder,
  onEdit,
  onDelete,
}: {
  builder: Builder
  onEdit: (builder: Builder) => void
  onDelete: (builderId: string, builderName: string) => void
}) {
  return (
    <Card className="flex flex-col h-full group relative">
      <div className="absolute top-2 right-2 opacity-0 group-hover:opacity-100 transition-opacity flex gap-1">
        <Button variant="outline" size="icon" className="h-7 w-7" onClick={() => onEdit(builder)}>
          <Edit className="h-3.5 w-3.5" />
          <span className="sr-only">Edit Builder</span>
        </Button>
        <Button
          variant="destructive"
          size="icon"
          className="h-7 w-7"
          onClick={() => onDelete(builder.id, builder.name || "this builder")}
        >
          <Trash2 className="h-3.5 w-3.5" />
          <span className="sr-only">Delete Builder</span>
        </Button>
      </div>
      <CardHeader className="pb-3">
        <CardTitle className="text-sm">
          <Link href={`/builders/${builder.id}`} className="hover:underline">
            {builder.name}
          </Link>
        </CardTitle>
        {builder.company_name && <CardDescription className="text-xs">{builder.company_name}</CardDescription>}
      </CardHeader>
      <CardContent className="flex-grow space-y-2 text-xs">
        {builder.phone && (
          <div className="flex items-center gap-x-1.5 text-muted-foreground">
            <Phone className="h-3 w-3" />
            <span>{builder.phone}</span>
          </div>
        )}
        {builder.email && (
          <div className="flex items-center gap-x-1.5 text-muted-foreground">
            <Mail className="h-3 w-3" />
            <a href={`mailto:${builder.email}`} className="hover:underline text-primary">
              {builder.email}
            </a>
          </div>
        )}
        {builder.website && (
          <div className="flex items-center gap-x-1.5 text-muted-foreground">
            <Globe className="h-3 w-3" />
            <a
              href={builder.website}
              target="_blank"
              rel="noopener noreferrer"
              className="hover:underline text-primary truncate"
            >
              {builder.website.replace(/^https?:\/\//, "")}
            </a>
          </div>
        )}
        {builder.specialties && builder.specialties.length > 0 && (
          <div className="pt-1">
            <span className="font-medium text-foreground">Specialties:</span>
            <div className="flex flex-wrap gap-1 mt-1">
              {(builder.specialties as string[]).slice(0, 3).map((specialty: string, index: number) => (
                <Badge key={index} variant="secondary" className="text-[10px] px-1.5 py-0.5">
                  {specialty}
                </Badge>
              ))}
              {(builder.specialties as string[]).length > 3 && (
                <Badge variant="outline" className="text-[10px] px-1.5 py-0.5">
                  +{(builder.specialties as string[]).length - 3} more
                </Badge>
              )}
            </div>
          </div>
        )}
      </CardContent>
      <CardFooter className="text-xs text-muted-foreground pt-3">
        <div className="flex items-center gap-x-1">
          <Building2 className="h-3 w-3" />
          <span>{builder.listings_count || 0} Listings</span>
        </div>
      </CardFooter>
    </Card>
  )
}

export default function BuildersPage() {
  const [builders, setBuilders] = React.useState<Builder[]>([])
  const [loading, setLoading] = React.useState(true)
  const [searchTerm, setSearchTerm] = React.useState("")
  const [isBuilderFormOpen, setIsBuilderFormOpen] = React.useState(false) // State for new dialog
  const [editingBuilder, setEditingBuilder] = React.useState<Partial<Builder> | undefined>(undefined)
  const { toast } = useToast()

  const fetchBuilders = React.useCallback(async () => {
    setLoading(true)
    try {
      const { data, error } = await supabase.from("builders").select(`*, listings (count)`).order("name") // Changed 'properties' to 'listings'

      if (error) throw error

      const enrichedBuilders =
        data?.map((builder) => ({
          ...builder,
          // @ts-ignore - Supabase types for related table counts can be tricky
          listings_count: builder.listings && builder.listings.length > 0 ? builder.listings[0]?.count || 0 : 0, // Access count from 'listings'
        })) || []

      setBuilders(enrichedBuilders)
    } catch (error) {
      console.error("Error fetching builders:", error)
    } finally {
      setLoading(false)
    }
  }, [])

  React.useEffect(() => {
    fetchBuilders()
  }, [fetchBuilders])

  const handleOpenNewBuilderDialog = () => {
    setEditingBuilder(undefined)
    setIsBuilderFormOpen(true)
  }

  const handleOpenEditBuilderDialog = (builder: Builder) => {
    setEditingBuilder(builder)
    setIsBuilderFormOpen(true)
  }

  const handleDeleteBuilder = async (builderId: string, builderName: string) => {
    if (!confirm(`Are you sure you want to delete ${builderName}? This action cannot be undone.`)) {
      return
    }
    try {
      const { error } = await supabase.from("builders").delete().eq("id", builderId)
      if (error) throw error
      toast({ title: "Builder Deleted", description: `${builderName} has been successfully deleted.` })
      fetchBuilders() // Refresh the list
    } catch (error: any) {
      toast({ title: "Error", description: error.message || "Failed to delete builder.", variant: "destructive" })
    }
  }

  const filteredBuilders = builders.filter((builder) => {
    if (!searchTerm) return true
    const searchLower = searchTerm.toLowerCase()
    return (
      builder.name?.toLowerCase().includes(searchLower) ||
      builder.company_name?.toLowerCase().includes(searchLower) ||
      builder.email?.toLowerCase().includes(searchLower) ||
      (builder.specialties as string[])?.some((s: string) => s.toLowerCase().includes(searchLower))
    )
  })

  return (
    <div className="space-y-4">
      <div className="flex items-center justify-between">
        <div>
          <h1 className="text-lg font-semibold">Builders</h1>
          <p className="text-xs text-muted-foreground">{filteredBuilders.length} builders found</p>
        </div>
        <Button size="sm" className="h-7 text-xs" onClick={handleOpenNewBuilderDialog}>
          {" "}
          {/* Changed this line */}
          <Plus className="mr-1.5 h-3 w-3" />
          Add Builder
        </Button>
      </div>

      <Input
        placeholder="Search builders by name, company, email, specialty..."
        value={searchTerm}
        onChange={(e) => setSearchTerm(e.target.value)}
        className="h-8 text-xs max-w-md attio-input"
      />

      {loading ? (
        <div className="grid grid-cols-1 gap-3 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4">
          {[...Array(8)].map((_, i) => (
            <Card key={i}>
              <CardHeader className="pb-3">
                <div className="h-4 bg-muted rounded w-3/4 animate-pulse"></div>
                <div className="h-3 bg-muted rounded w-1/2 mt-1 animate-pulse"></div>
              </CardHeader>
              <CardContent className="space-y-2">
                <div className="h-3 bg-muted rounded w-full animate-pulse"></div>
                <div className="h-3 bg-muted rounded w-5/6 animate-pulse"></div>
              </CardContent>
              <CardFooter>
                <div className="h-3 bg-muted rounded w-1/4 animate-pulse"></div>
              </CardFooter>
            </Card>
          ))}
        </div>
      ) : filteredBuilders.length > 0 ? (
        <div className="grid grid-cols-1 gap-4 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4">
          {filteredBuilders.map((builder) => (
            <BuilderCard
              key={builder.id}
              builder={builder}
              onEdit={handleOpenEditBuilderDialog}
              onDelete={handleDeleteBuilder}
            />
          ))}
        </div>
      ) : (
        <div className="text-center py-10 text-muted-foreground">No builders found matching your search.</div>
      )}
      <BuilderFormDialog // Add the new dialog component
        open={isBuilderFormOpen}
        onOpenChange={setIsBuilderFormOpen}
        onBuilderCreated={fetchBuilders} // Refresh list on creation
        builder={editingBuilder}
      />
    </div>
  )
}
```

## File: dkl-microapp-2-main/app/(dashboard)/dashboard/page.tsx
```typescript
"use client"

import type React from "react"
import { useEffect, useState } from "react"
import { supabase } from "@/lib/supabase/client"
import { Card, CardContent, CardHeader, CardTitle } from "@/components/ui/card"
import { formatCurrency, formatNumber } from "@/lib/utils"
import { Building2, TrendingUp, DollarSign, Home, MapPin } from "lucide-react"
import MapboxMap, { type MappableListing } from "@/components/mapbox-map" // Import the new MapboxMap component
import { useAuth } from "@/contexts/auth-context"
import { Loader2 } from "lucide-react"

interface DashboardStats {
  totalProperties: number
  activeListings: number
  newConstruction: number
  avgListPrice: number
  totalBuilders: number
  underConstruction: number
}

export default function DashboardPage() {
  const { user } = useAuth()
  const [stats, setStats] = useState<DashboardStats | null>(null)
  const [loadingStats, setLoadingStats] = useState(true)
  const [mapProperties, setMapProperties] = useState<MappableListing[]>([])
  const [loadingMapProps, setLoadingMapProps] = useState(true)
  const [userMapboxApiKey, setUserMapboxApiKey] = useState<string | null>(null)
  const [loadingApiKey, setLoadingApiKey] = useState(true)

  useEffect(() => {
    async function fetchStats() {
      setLoadingStats(true)
      try {
        const { count: totalProperties } = await supabase.from("listings").select("*", { count: "exact", head: true })
        const { count: activeListings } = await supabase
          .from("listings")
          .select("*", { count: "exact", head: true })
          .eq("status", "Active")
        const { count: newConstruction } = await supabase
          .from("listings")
          .select("*", { count: "exact", head: true })
          .eq("new_construction", true)
        const { count: underConstruction } = await supabase
          .from("listings")
          .select("*", { count: "exact", head: true })
          .eq("development_status", "under_construction")
        const { data: priceData } = await supabase.from("listings").select("list_price").not("list_price", "is", null)
        const avgListPrice = priceData?.length
          ? priceData.reduce((sum, p) => sum + (p.list_price || 0), 0) / priceData.length
          : 0
        const { count: totalBuilders } = await supabase.from("builders").select("*", { count: "exact", head: true })

        setStats({
          totalProperties: totalProperties || 0,
          activeListings: activeListings || 0,
          newConstruction: newConstruction || 0,
          avgListPrice,
          totalBuilders: totalBuilders || 0,
          underConstruction: underConstruction || 0,
        })
      } catch (error) {
        console.error("Error fetching stats:", error)
      } finally {
        setLoadingStats(false)
      }
    }

    // Update the fetchMapProperties function to include additional fields for the popup
    async function fetchMapProperties() {
      setLoadingMapProps(true)
      try {
        const { data, error } = await supabase
          .from("listings")
          .select(`
        id, 
        address_line_1, 
        city, 
        state, 
        latitude, 
        longitude, 
        status, 
        list_price,
        builders(name)
      `)
          .in("status", ["Active", "Coming Soon"]) // Filter for Active or Coming Soon

        if (error) throw error

        // Transform the data to include builder_name
        const transformedData =
          data?.map((property) => ({
            ...property,
            builder_name: property.builders?.name || null,
          })) || []

        setMapProperties(transformedData as MappableListing[])
      } catch (error) {
        console.error("Error fetching map properties:", error)
        setMapProperties([])
      } finally {
        setLoadingMapProps(false)
      }
    }

    async function fetchUserApiKey() {
      if (!user) {
        setLoadingApiKey(false)
        return
      }
      setLoadingApiKey(true)
      try {
        const { data, error } = await supabase
          .from("user_settings")
          .select("mapbox_api_key")
          .eq("user_id", user.id)
          .single()
        if (error && error.code !== "PGRST116") throw error
        setUserMapboxApiKey(data?.mapbox_api_key || null)
      } catch (error) {
        console.error("Error fetching Mapbox API key:", error)
      } finally {
        setLoadingApiKey(false)
      }
    }

    fetchStats()
    fetchMapProperties()
    fetchUserApiKey()
  }, [user])

  const isLoading = loadingStats || loadingMapProps || loadingApiKey

  return (
    <div className="space-y-4 h-full flex flex-col">
      <div>
        <h1 className="text-lg font-semibold">Dashboard</h1>
        <p className="text-xs text-gray-600">Luxury residential new construction market overview</p>
      </div>

      <div className="grid grid-cols-2 gap-3 lg:grid-cols-3 xl:grid-cols-6">
        <StatCard title="Total Listings" value={stats?.totalProperties} icon={Home} loading={isLoading} />
        <StatCard title="Active Listings" value={stats?.activeListings} icon={Building2} loading={isLoading} />
        <StatCard title="New Construction" value={stats?.newConstruction} icon={TrendingUp} loading={isLoading} />
        <StatCard title="Under Construction" value={stats?.underConstruction} icon={Building2} loading={isLoading} />
        <StatCard
          title="Avg List Price"
          value={stats?.avgListPrice}
          icon={DollarSign}
          loading={isLoading}
          formatter={formatCurrency}
        />
        <StatCard title="Total Builders" value={stats?.totalBuilders} icon={Building2} loading={isLoading} />
      </div>

      <div className="grid grid-cols-1 gap-4 lg:grid-cols-3 flex-1 min-h-0">
        <Card className="lg:col-span-2 flex flex-col h-full">
          <CardHeader className="pb-3">
            <CardTitle className="text-sm flex items-center">
              <MapPin className="mr-2 h-4 w-4" /> Listing Map (Active & Coming Soon)
            </CardTitle>
          </CardHeader>
          <CardContent className="flex-1 p-0 min-h-0">
            {" "}
            {/* Set a fixed height for the map container */}
            {loadingApiKey ? (
              <div className="flex items-center justify-center h-full">
                <Loader2 className="h-6 w-6 animate-spin" /> <span className="ml-2">Loading Map Data...</span>
              </div>
            ) : (
              <MapboxMap
                userApiKey={userMapboxApiKey}
                properties={mapProperties}
                className="rounded-b-lg w-full h-full" // Ensure full width and height
              />
            )}
          </CardContent>
        </Card>

        <div className="space-y-4 lg:col-span-1">
          <Card>
            <CardHeader className="pb-3">
              <CardTitle className="text-sm">Recent Activity</CardTitle>
            </CardHeader>
            <CardContent>
              <div className="space-y-2 text-xs">
                <div className="flex justify-between border-b pb-1">
                  <span className="text-gray-600">New listings (7d)</span>
                  <span className="font-medium">12</span>
                </div>
                <div className="flex justify-between border-b pb-1">
                  <span className="text-gray-600">Price changes (7d)</span>
                  <span className="font-medium">8</span>
                </div>
                <div className="flex justify-between border-b pb-1">
                  <span className="text-gray-600">Sold (30d)</span>
                  <span className="font-medium">23</span>
                </div>
                <div className="flex justify-between">
                  <span className="text-gray-600">Avg DOM</span>
                  <span className="font-medium">45 days</span>
                </div>
              </div>
            </CardContent>
          </Card>

          <Card>
            <CardHeader className="pb-3">
              <CardTitle className="text-sm">Market Trends</CardTitle>
            </CardHeader>
            <CardContent>
              <div className="space-y-2 text-xs">
                <div className="flex justify-between border-b pb-1">
                  <span className="text-gray-600">Median price change</span>
                  <span className="font-medium text-green-600">+3.2%</span>
                </div>
                <div className="flex justify-between border-b pb-1">
                  <span className="text-gray-600">Inventory change</span>
                  <span className="font-medium text-red-600">-12%</span>
                </div>
                <div className="flex justify-between border-b pb-1">
                  <span className="text-gray-600">New construction share</span>
                  <span className="font-medium">18%</span>
                </div>
                <div className="flex justify-between">
                  <span className="text-gray-600">Price per sq ft</span>
                  <span className="font-medium">$425</span>
                </div>
              </div>
            </CardContent>
          </Card>
        </div>
      </div>
    </div>
  )
}

interface StatCardProps {
  title: string
  value?: number
  icon: React.ElementType
  loading: boolean
  formatter?: (value: number) => string
}

function StatCard({ title, value, icon: Icon, loading, formatter = formatNumber }: StatCardProps) {
  return (
    <Card>
      <CardHeader className="flex flex-row items-center justify-between space-y-0 pb-2">
        <CardTitle className="text-xs font-medium text-gray-600">{title}</CardTitle>
        <Icon className="h-3.5 w-3.5 text-gray-400" />
      </CardHeader>
      <CardContent>
        <div className="text-lg font-bold">
          {loading ? <div className="h-6 w-16 animate-pulse rounded bg-gray-200" /> : formatter(value || 0)}
        </div>
      </CardContent>
    </Card>
  )
}
```

## File: dkl-microapp-2-main/app/(dashboard)/import/page.tsx
```typescript
"use client"

import type React from "react"
import { useState, useCallback, useMemo, useEffect } from "react"
import { useDropzone } from "react-dropzone"
import Papa from "papaparse"
import { Button } from "@/components/ui/button"
import { Progress } from "@/components/ui/progress"
import { useToast } from "@/hooks/use-toast"
import { supabase } from "@/lib/supabase/client"
import { useAuth } from "@/contexts/auth-context"
import { Alert, AlertDescription, AlertTitle } from "@/components/ui/alert"
import { Card, CardContent, CardDescription, CardHeader, CardTitle } from "@/components/ui/card"
import {
  UploadCloud,
  FileText,
  CheckCircle,
  XCircle,
  Info,
  Loader2,
  AlertCircle,
  Settings2,
  ChevronLeft,
  ChevronRight,
} from "lucide-react"
import type { Database } from "@/types/supabase"
import { parseCSVValue, toTitleCase, formatDate, normalizeHeader } from "@/lib/utils"
import { FieldMappingSheet } from "@/components/field-mapping-sheet"
import { listingTableColumns, type MappedDbColumn, type ListingFieldDefinition } from "@/lib/listing-fields"
import { Table, TableBody, TableCell, TableHead, TableHeader, TableRow } from "@/components/ui/table"
import { Badge } from "@/components/ui/badge"
import { Switch } from "@/components/ui/switch"
import { Label } from "@/components/ui/label"

type ListingInsert = Database["public"]["Tables"]["listings"]["Insert"]
type ListingRow = Database["public"]["Tables"]["listings"]["Row"]
type UserFieldMappingInsert = Database["public"]["Tables"]["user_field_mappings"]["Insert"]

interface ImportResult {
  totalRecords: number
  newRecordsAdded: number
  recordsUpdated: number
  ignoredOrDuplicate: number
  failedDueToError: number
  errors: string[]
}

interface PreprocessingStats {
  totalCsvRecords: number
  newCsvRecords: number
  matchedCsvRecords: number
  totalCsvFields: number
  autoMatchedCsvFields: number
  unmatchedCsvFields: number
}

type UploadHistoryEntry = Database["public"]["Tables"]["csv_uploads"]["Row"]

// Define a more specific type for metadata if its structure is known
interface CsvUploadMetadata {
  duration_seconds?: number
  ignored_records?: number
  override_existing?: boolean
  // Add other potential metadata fields here
}

const baseStyle: React.CSSProperties = {
  flex: 1,
  display: "flex",
  flexDirection: "column",
  alignItems: "center",
  justifyContent: "center",
  padding: "20px",
  borderWidth: 2,
  borderRadius: "0.5rem",
  borderColor: "#e2e8f0",
  borderStyle: "dashed",
  backgroundColor: "#f8fafc",
  color: "#64748b",
  outline: "none",
  transition: "border .24s ease-in-out",
  minHeight: "160px",
}

const activeStyle: React.CSSProperties = { borderColor: "#2563eb" }
const acceptStyle: React.CSSProperties = { borderColor: "#16a34a" }
const rejectStyle: React.CSSProperties = { borderColor: "#dc2626" }

const statusMapping: Record<string, string> = {
  "A/C": "Active Under Contract",
  ACT: "Active",
  "C/S": "Coming Soon",
  CLS: "Closed",
  CNL: "Canceled",
  PND: "Pending",
  "T/O": "Temporary Off Market",
  WTH: "Withdrawn",
  EXP: "Expired",
}

const defaultCsvToDbMapping: Record<
  string,
  { dbCol: ListingFieldDefinition["value"]; typeHint: ListingFieldDefinition["typeHint"] }
> = {
  MLS_NUMBER: { dbCol: "mls_number", typeHint: "string" },
  MLS_: { dbCol: "mls_number", typeHint: "string" },
  DOM: { dbCol: "dom", typeHint: "number" },
  CDOM: { dbCol: "cdom", typeHint: "number" },
  LIST_DATE: { dbCol: "list_date", typeHint: "date" },
  STATUS: { dbCol: "status", typeHint: "string" },
  SUBDIVISION: { dbCol: "subdivision", typeHint: "string" },
  AGREEMENT_DATE: { dbCol: "agreement_date", typeHint: "date" },
  OFF_MARKET_DATE: { dbCol: "off_market_date", typeHint: "date" },
  SETTLED_DATE: { dbCol: "settled_date", typeHint: "date" },
  ORIGINAL_PRICE: { dbCol: "original_price", typeHint: "number" },
  LIST_PRICE: { dbCol: "list_price", typeHint: "number" },
  SOLD_PRICE: { dbCol: "sold_price", typeHint: "number" },
  STREET_NUMBER: { dbCol: "street_number", typeHint: "string" },
  STREET_DIRECTION: { dbCol: "street_direction", typeHint: "string" },
  STREET_NAME: { dbCol: "street_name", typeHint: "string" },
  UNIT_NUMBER: { dbCol: "unit_number", typeHint: "string" },
  CITY: { dbCol: "city", typeHint: "string" },
  STATE: { dbCol: "state", typeHint: "string" },
  ZIP_CODE: { dbCol: "zip_code", typeHint: "string" },
  COUNTY: { dbCol: "county", typeHint: "string" },
  MLS_AREA: { dbCol: "mls_area", typeHint: "string" },
  LIST_AGENT_NAME: { dbCol: "list_agent_name", typeHint: "string" },
  LIST_AGENT_CODE: { dbCol: "list_agent_code", typeHint: "string" },
  LIST_OFFICE_NAME: { dbCol: "list_office_name", typeHint: "string" },
  LIST_OFFICE_CODE: { dbCol: "list_office_code", typeHint: "string" },
  LIST_OFFICE_PHONE: { dbCol: "list_office_phone", typeHint: "string" },
  SELLING_AGENT: { dbCol: "selling_agent", typeHint: "string" },
  SELLING_AGENT_CODE: { dbCol: "selling_agent_code", typeHint: "string" },
  SELLING_OFFICE_NAME: { dbCol: "selling_office_name", typeHint: "string" },
  SELLING_OFFICE_CODE: { dbCol: "selling_office_code", typeHint: "string" },
  SELLING_OFFICE_PHONE: { dbCol: "selling_office_phone", typeHint: "string" },
  FINAL_FINANCING: { dbCol: "final_financing", typeHint: "string" },
  FINAL_SHORT_SALE: { dbCol: "final_short_sale", typeHint: "boolean" },
  FINAL_THIRD_PARTY_APPROVAL: { dbCol: "final_third_party_approval", typeHint: "boolean" },
  FINAL_BANK_OWNED: { dbCol: "final_bank_owned", typeHint: "boolean" },
  TAX_ANNUAL_TOTAL: { dbCol: "tax_annual_total", typeHint: "number" },
  TAX_YEAR: { dbCol: "tax_year", typeHint: "number" },
  ACRES_TOTAL: { dbCol: "acres_total", typeHint: "number" },
  LAND_USE_CODE: { dbCol: "land_use_code", typeHint: "string" },
  OWNERSHIP: { dbCol: "ownership", typeHint: "string" },
  SENIOR_COMMUNITY: { dbCol: "senior_community", typeHint: "boolean" },
  CONDO_COOP_ASSOC: { dbCol: "condo_coop_assoc", typeHint: "boolean" },
  HOA: { dbCol: "hoa", typeHint: "boolean" },
  ONE_TIME_ASSOCIATION_FEE: { dbCol: "one_time_association_fee", typeHint: "number" },
  ASSOCIATION_FEE: { dbCol: "association_fee", typeHint: "number" },
  ASSOCIATION_FEE_FREQUENCY: { dbCol: "association_fee_frequency", typeHint: "string" },
  AGE: { dbCol: "age", typeHint: "number" },
  INTERIOR_SQFT: { dbCol: "interior_sqft", typeHint: "number" },
  SQUARE_FEET: { dbCol: "interior_sqft", typeHint: "number" },
  PROPERTY_CONDITION: { dbCol: "property_condition", typeHint: "string" },
  BEDROOMS: { dbCol: "bedrooms", typeHint: "number" },
  BATHS_FULL: { dbCol: "baths_full", typeHint: "number" },
  BATHS_HALF: { dbCol: "baths_half", typeHint: "number" },
  DESIGN: { dbCol: "design", typeHint: "string" },
  STYLE: { dbCol: "style", typeHint: "string" },
  NUMBER_OF_STORIES: { dbCol: "number_of_stories", typeHint: "string" },
  FLOOR_NUMBER: { dbCol: "floor_number", typeHint: "string" },
  BASEMENT: { dbCol: "basement", typeHint: "boolean" },
  GARAGE_SPACES: { dbCol: "garage_spaces", typeHint: "number" },
  FIREPLACE: { dbCol: "fireplace", typeHint: "boolean" },
  LAUNDRY: { dbCol: "laundry", typeHint: "string" },
  OTHER_ROOMS: { dbCol: "other_rooms", typeHint: "string" },
  ROOM_COUNT: { dbCol: "room_count", typeHint: "number" },
  CENTRAL_AIR: { dbCol: "central_air", typeHint: "boolean" },
  WATERFRONT: { dbCol: "waterfront", typeHint: "boolean" },
  NEW_CONSTRUCTION_YN: { dbCol: "new_construction", typeHint: "boolean" },
  NEW_CONSTRUCTION: { dbCol: "new_construction_details", typeHint: "string" },
  MODEL_NAME: { dbCol: "model_name", typeHint: "string" },
  ORIGINATING_MLS: { dbCol: "originating_mls", typeHint: "string" },
  ABOVE_GRADE_SQFT: { dbCol: "above_grade_sqft", typeHint: "number" },
  BELOW_GRADE_SQFT: { dbCol: "below_grade_sqft", typeHint: "number" },
  HOME_BUILT: { dbCol: "home_built", typeHint: "string" },
  BASEMENT_FOOTPRINT_PCT: { dbCol: "basement_footprint_pct", typeHint: "number" },
  BASEMENT_FINISHED_PCT: { dbCol: "basement_finished_pct", typeHint: "number" },
  DEVELOPMENT_STATUS: { dbCol: "development_status", typeHint: "string" },
  IN_SOCIAL_QUEUE: { dbCol: "in_social_queue", typeHint: "boolean" },
  LATITUDE: { dbCol: "latitude", typeHint: "number" },
  LONGITUDE: { dbCol: "longitude", typeHint: "number" },
  LAST_SOLD_DATE: { dbCol: "last_sold_date", typeHint: "date" },
  LAST_SOLD_PRICE: { dbCol: "last_sold_price", typeHint: "number" },
  DESCRIPTION: { dbCol: "description", typeHint: "string" },
  OWNER_NAME: { dbCol: "owner_name", typeHint: "string" },
  CONSTRUCTION_COMPLETED_YN: { dbCol: "construction_completed_yn", typeHint: "boolean" },
  YEAR_BUILT: { dbCol: "year_built", typeHint: "number" },
  YEAR_BUILT_SOURCE: { dbCol: "year_built_source", typeHint: "string" },
  IMPORTED_BUILDER_NAME: { dbCol: "imported_builder_name", typeHint: "string" },
  BUILDER_NAME: { dbCol: "imported_builder_name", typeHint: "string" },
  OCCUPANT_TYPE: { dbCol: "occupant_type", typeHint: "string" },
  OCCUPANT_NAME: { dbCol: "occupant_name", typeHint: "string" },
  PREVIOUS_LIST_PRICE: { dbCol: "previous_list_price", typeHint: "number" },
  ARCHITECT_NAME: { dbCol: "architect_name", typeHint: "string" },
  STRUCTURE_TYPE: { dbCol: "structure_type", typeHint: "string" },
  BLOCK_LOT: { dbCol: "block_lot", typeHint: "string" },
  REMARKS_PRIVATE: { dbCol: "remarks_private", typeHint: "string" },
  REMARKS_PUBLIC: { dbCol: "remarks_public", typeHint: "string" },
  YEAR_MAJOR_RENO_REMODEL: { dbCol: "year_major_reno_remodel", typeHint: "number" },
  CHANGE_INFO: { dbCol: "change_info", typeHint: "string" },
  CHG_INFO: { dbCol: "change_info", typeHint: "string" },
  CLOSE_DATE: { dbCol: "close_date", typeHint: "date" },
  CLOSE_PRICE: { dbCol: "close_price", typeHint: "number" },
  CLOSE_SALE_TYPE: { dbCol: "close_sale_type", typeHint: "string" },
  FOUNDATION_DETAILS: { dbCol: "foundation_details", typeHint: "string" },
  LAND_ASSESSED_VALUE: { dbCol: "land_assessed_value", typeHint: "number" },
  LIST_PICTURE_URL: { dbCol: "list_picture_url", typeHint: "string" },
  LOT_FEATURES: { dbCol: "lot_features", typeHint: "array_string" },
  LOT_SIZE_SQFT: { dbCol: "lot_size_sqft", typeHint: "number" },
  ADDRESS_LINE_1: { dbCol: "address_line_1", typeHint: "string" },
}

const defaultIgnoredHeaders: string[] = [
  "ADDRESS",
  "BEDS",
  "BATHS",
  "SUB_TYPE",
  "STATUS_CONTRACTUAL_SEARCH_DATE",
  "PRICE",
].map(normalizeHeader)

const CHUNK_SIZE = 200 // For main import processing
const STATS_QUERY_CHUNK_SIZE = 500 // For fetching MLS numbers for stats

export default function ImportPage() {
  const [file, setFile] = useState<File | null>(null)
  const [isProcessing, setIsProcessing] = useState(false)
  const [isSavingMappings, setIsSavingMappings] = useState(false)
  const [progress, setProgress] = useState(0)
  const [result, setResult] = useState<ImportResult | null>(null)
  const [error, setError] = useState<string | null>(null)
  const { toast } = useToast()
  const { user } = useAuth()

  const [csvHeaders, setCsvHeaders] = useState<string[]>([])
  const [fieldMappings, setFieldMappings] = useState<Record<string, MappedDbColumn>>({})
  const [isMappingSheetOpen, setIsMappingSheetOpen] = useState(false)
  const [parsedCsvData, setParsedCsvData] = useState<any[]>([])
  const [preprocessingStats, setPreprocessingStats] = useState<PreprocessingStats | null>(null)

  const [uploadHistory, setUploadHistory] = useState<UploadHistoryEntry[]>([])
  const [isLoadingHistory, setIsLoadingHistory] = useState(false)
  const [historyPage, setHistoryPage] = useState(1)
  const [totalHistoryCount, setTotalHistoryCount] = useState(0)
  const historyRowsPerPage = 5

  const [overrideExisting, setOverrideExisting] = useState(false)

  const [userSavedMappings, setUserSavedMappings] = useState<Record<string, string>>({})

  const fetchUserSavedMappings = useCallback(async () => {
    if (!user) {
      setUserSavedMappings({})
      return
    }
    try {
      const { data, error: fetchErr } = await supabase
        .from("user_field_mappings")
        .select("source_csv_header, target_database_column")
        .eq("user_id", user.id)
        .eq("target_table_name", "listings")

      if (fetchErr) throw fetchErr

      const mappings: Record<string, string> = {}
      data?.forEach((m) => {
        mappings[m.source_csv_header] = m.target_database_column
      })
      setUserSavedMappings(mappings)
    } catch (err: any) {
      console.error("Error fetching user field mappings:", err)
      toast({ title: "Error", description: "Could not load your saved field mappings.", variant: "destructive" })
    }
  }, [user, toast])

  useEffect(() => {
    fetchUserSavedMappings()
  }, [fetchUserSavedMappings])

  const fetchHistory = useCallback(async () => {
    if (!user) return
    setIsLoadingHistory(true)
    try {
      const from = (historyPage - 1) * historyRowsPerPage
      const to = historyPage * historyRowsPerPage - 1

      const {
        data,
        error: fetchError,
        count,
      } = await supabase
        .from("csv_uploads")
        .select("*", { count: "exact" })
        .eq("user_id", user.id)
        .order("upload_date", { ascending: false })
        .range(from, to)

      if (fetchError) {
        toast({ title: "Error fetching history", description: fetchError.message, variant: "destructive" })
        setUploadHistory([])
      } else if (data) {
        setUploadHistory(data)
        setTotalHistoryCount(count || 0)
      }
    } catch (e: any) {
      toast({ title: "Error fetching history", description: e.message, variant: "destructive" })
      setUploadHistory([])
    } finally {
      setIsLoadingHistory(false)
    }
  }, [user, toast, historyPage])

  useEffect(() => {
    fetchHistory()
  }, [fetchHistory])

  const onDrop = useCallback(
    (acceptedFiles: File[]) => {
      if (acceptedFiles && acceptedFiles.length > 0) {
        const selectedFile = acceptedFiles[0]
        setFile(selectedFile)
        setResult(null)
        setError(null)
        setCsvHeaders([])
        setFieldMappings({})
        setParsedCsvData([])
        setPreprocessingStats(null)

        const reader = new FileReader()

        reader.onload = (event) => {
          if (event.target && typeof event.target.result === "string") {
            const csvString = event.target.result

            // Main parse (for data)
            Papa.parse(csvString, {
              header: true,
              skipEmptyLines: true,
              worker: false, // Explicitly false, though default for string input
              transformHeader: (header) => normalizeHeader(header),
              complete: (results) => {
                // Second parse (for raw headers from the first line)
                Papa.parse(csvString, {
                  preview: 1,
                  header: false,
                  complete: (headerResults) => {
                    const rawHeadersFromFile = (headerResults.data[0] as string[]) || []
                    setCsvHeaders(rawHeadersFromFile)
                    setParsedCsvData(results.data as any[])

                    const initialMappings: Record<string, MappedDbColumn> = {}
                    const dbColumnsMappedInThisFile = new Set<string>()

                    rawHeadersFromFile.forEach((rawHeader) => {
                      const normalizedHeaderKeyFromFile = normalizeHeader(rawHeader)
                      let mappedDbColumnTarget: MappedDbColumn | undefined = undefined

                      // 1. Try user-saved mappings
                      if (userSavedMappings[normalizedHeaderKeyFromFile]) {
                        const dbColFromUser = userSavedMappings[normalizedHeaderKeyFromFile] as MappedDbColumn
                        if (!dbColumnsMappedInThisFile.has(dbColFromUser) || dbColFromUser === "ignore_field") {
                          mappedDbColumnTarget = dbColFromUser
                        } else {
                          // If taken, try to ignore, or let further logic decide
                        }
                      }

                      // 2. Try default mappings if not found or if user mapping was 'ignore_field' and we want to reconsider
                      if (!mappedDbColumnTarget || mappedDbColumnTarget === "ignore_field") {
                        const defaultMappingEntry = defaultCsvToDbMapping[normalizedHeaderKeyFromFile]
                        if (defaultMappingEntry) {
                          const dbColFromDefault = defaultMappingEntry.dbCol as MappedDbColumn
                          if (!dbColumnsMappedInThisFile.has(dbColFromDefault) || dbColFromDefault === "ignore_field") {
                            if (mappedDbColumnTarget !== "ignore_field") {
                              // Prioritize user's explicit ignore
                              mappedDbColumnTarget = dbColFromDefault
                            } else if (!mappedDbColumnTarget) {
                              mappedDbColumnTarget = dbColFromDefault
                            }
                          } else if (!mappedDbColumnTarget) {
                            // Default mapping is taken, will be set to ignore later if still no target
                          }
                        }
                      }

                      // 3. Check default ignored headers if still no mapping
                      if (!mappedDbColumnTarget && defaultIgnoredHeaders.includes(normalizedHeaderKeyFromFile)) {
                        mappedDbColumnTarget = "ignore_field"
                      }

                      // 4. Try direct match by label or value if still no mapping
                      if (!mappedDbColumnTarget) {
                        const directMatch = listingTableColumns.find(
                          (ptc) =>
                            normalizeHeader(ptc.label) === normalizedHeaderKeyFromFile ||
                            ptc.value === normalizedHeaderKeyFromFile,
                        )
                        if (directMatch) {
                          const dbColFromDirect = directMatch.value as MappedDbColumn
                          if (!dbColumnsMappedInThisFile.has(dbColFromDirect) || dbColFromDirect === "ignore_field") {
                            mappedDbColumnTarget = dbColFromDirect
                          }
                        }
                      }

                      // 5. Default to ignore_field if no mapping found or if a chosen mapping was already taken by a previous header
                      if (
                        !mappedDbColumnTarget ||
                        (mappedDbColumnTarget !== "ignore_field" && dbColumnsMappedInThisFile.has(mappedDbColumnTarget))
                      ) {
                        mappedDbColumnTarget = "ignore_field"
                      }

                      initialMappings[rawHeader] = mappedDbColumnTarget
                      if (mappedDbColumnTarget !== "ignore_field") {
                        dbColumnsMappedInThisFile.add(mappedDbColumnTarget)
                      }
                    })
                    setFieldMappings(initialMappings)

                    // Preprocessing Stats Logic (remains largely the same)
                    const currentParsedData = results.data as any[]
                    const currentRawHeaders = rawHeadersFromFile
                    const currentInitialMappings = initialMappings

                    const stats: PreprocessingStats = {
                      totalCsvRecords: currentParsedData.length,
                      newCsvRecords: 0,
                      matchedCsvRecords: 0,
                      totalCsvFields: currentRawHeaders.length,
                      autoMatchedCsvFields: 0,
                      unmatchedCsvFields: 0,
                    }

                    currentRawHeaders.forEach((header) => {
                      if (currentInitialMappings[header] && currentInitialMappings[header] !== "ignore_field") {
                        stats.autoMatchedCsvFields++
                      } else {
                        stats.unmatchedCsvFields++
                      }
                    })

                    if (user && currentParsedData.length > 0) {
                      let mlsCsvHeaderKey: string | undefined
                      for (const [rawHeader, dbCol] of Object.entries(currentInitialMappings)) {
                        if (dbCol === "mls_number") {
                          mlsCsvHeaderKey = normalizeHeader(rawHeader) // Ensure we use the *normalized* header that PapaParse used for data keys
                          break
                        }
                      }

                      // If no mls_number mapping, try to find it from common default names in the raw CSV data keys
                      if (!mlsCsvHeaderKey && results.data.length > 0) {
                        const firstRecordKeys = Object.keys(results.data[0])
                        const commonMlsKeys = ["MLS_NUMBER", "MLS#", "MLS_"] // Normalized common keys
                        for (const commonKey of commonMlsKeys) {
                          if (firstRecordKeys.includes(commonKey)) {
                            mlsCsvHeaderKey = commonKey
                            break
                          }
                        }
                      }

                      if (mlsCsvHeaderKey) {
                        const allMlsNumbersInCsv = currentParsedData
                          .map((row) => (row[mlsCsvHeaderKey!] ? String(row[mlsCsvHeaderKey!]) : null))
                          .filter(Boolean) as string[]

                        if (allMlsNumbersInCsv.length > 0) {
                          const uniqueMlsNumbersInCsv = Array.from(new Set(allMlsNumbersInCsv))
                          const existingDbMlsNumbers = new Set<string>()
                          let fetchErrorOccurred = false
                          ;(async () => {
                            for (let i = 0; i < uniqueMlsNumbersInCsv.length; i += STATS_QUERY_CHUNK_SIZE) {
                              if (fetchErrorOccurred) break
                              const chunk = uniqueMlsNumbersInCsv.slice(i, i + STATS_QUERY_CHUNK_SIZE)
                              if (chunk.length === 0) continue

                              try {
                                const { data: chunkExistingPropsData, error: chunkMlsFetchError } = await supabase
                                  .from("listings")
                                  .select("mls_number")
                                  .in("mls_number", chunk)

                                if (chunkMlsFetchError) {
                                  console.error(
                                    `Error fetching existing MLS numbers for stats (chunk ${
                                      i / STATS_QUERY_CHUNK_SIZE + 1
                                    }): ${chunkMlsFetchError.message}`,
                                    chunkMlsFetchError,
                                  )
                                  fetchErrorOccurred = true
                                  stats.newCsvRecords = -1
                                  stats.matchedCsvRecords = -1
                                  break
                                }

                                if (chunkExistingPropsData) {
                                  chunkExistingPropsData.forEach((p) => {
                                    if (p.mls_number) existingDbMlsNumbers.add(p.mls_number)
                                  })
                                }
                              } catch (e: any) {
                                console.error(
                                  `Exception during fetching MLS numbers for stats (chunk ${
                                    i / STATS_QUERY_CHUNK_SIZE + 1
                                  }): ${e.message}`,
                                  e,
                                )
                                fetchErrorOccurred = true
                                stats.newCsvRecords = -1
                                stats.matchedCsvRecords = -1
                                break
                              }
                            }

                            if (!fetchErrorOccurred) {
                              let newCount = 0
                              let matchedCount = 0
                              uniqueMlsNumbersInCsv.forEach((csvMls) => {
                                if (existingDbMlsNumbers.has(csvMls)) matchedCount++
                                else newCount++
                              })
                              stats.newCsvRecords = newCount
                              stats.matchedCsvRecords = matchedCount
                            }
                            setPreprocessingStats({ ...stats })
                          })()
                        } else {
                          stats.newCsvRecords = 0
                          stats.matchedCsvRecords = 0
                          setPreprocessingStats(stats)
                        }
                      } else {
                        // MLS number column not found or not mapped, can't determine new/matched
                        stats.newCsvRecords = currentParsedData.length // Assume all are new if MLS# can't be identified
                        stats.matchedCsvRecords = 0
                        setPreprocessingStats(stats)
                      }
                    } else {
                      // No user or no parsed data
                      if (currentParsedData.length === 0) {
                        stats.totalCsvRecords = 0
                      }
                      setPreprocessingStats(stats)
                    }
                  },
                  error: (err: any) => {
                    console.error("PapaParse error on header pre-parse:", err)
                    // Fallback: use transformed headers if raw header parsing fails
                    const transformedHeaders = results.meta?.fields || Object.keys(results.data[0] || {})
                    setCsvHeaders(transformedHeaders)
                    setParsedCsvData(results.data as any[])
                    const initialMappingsOnError: Record<string, MappedDbColumn> = {}
                    transformedHeaders.forEach((th) => (initialMappingsOnError[th] = "ignore_field"))
                    setFieldMappings(initialMappingsOnError)
                    toast({
                      title: "Header Parsing Issue",
                      description:
                        "Could not read raw headers accurately, using transformed headers. Please verify mappings.",
                      variant: "default",
                    })
                  },
                })
              },
              error: (err: any) => {
                console.error("PapaParse error on main data parse:", err)
                setError(`Failed to parse CSV: ${err.message}`)
                setFile(null) // Clear the file on parse error
              },
            })
          } else {
            setError("Failed to read file content.")
            setFile(null)
          }
        }

        reader.onerror = () => {
          console.error("FileReader error:", reader.error)
          setError("Failed to read the file. Please ensure it's a valid CSV and try again.")
          setFile(null)
          setResult(null)
          setCsvHeaders([])
          setFieldMappings({})
          setParsedCsvData([])
          setPreprocessingStats(null)
        }

        reader.readAsText(selectedFile)
      }
    },
    [toast, user, userSavedMappings, fetchUserSavedMappings], // Added fetchUserSavedMappings if it's stable
  )

  const { getRootProps, getInputProps, isDragActive, isDragAccept, isDragReject } = useDropzone({
    onDrop,
    accept: { "text/csv": [".csv"] },
    multiple: false,
  })

  const style = useMemo(
    () => ({
      ...baseStyle,
      ...(isDragActive ? activeStyle : {}),
      ...(isDragAccept ? acceptStyle : {}),
      ...(isDragReject ? rejectStyle : {}),
    }),
    [isDragActive, isDragReject, isDragAccept],
  )

  const handleSaveMappings = async (updatedSheetMappings: Record<string, MappedDbColumn>) => {
    if (!user) {
      toast({ title: "Error", description: "User not authenticated.", variant: "destructive" })
      return
    }

    setIsSavingMappings(true)
    try {
      const { data: currentPersistentMappingsData, error: fetchError } = await supabase
        .from("user_field_mappings")
        .select("id, source_csv_header, target_database_column")
        .eq("user_id", user.id)
        .eq("target_table_name", "listings")

      if (fetchError) throw fetchError

      const currentPersistentMap = new Map(
        currentPersistentMappingsData.map((m) => [m.source_csv_header, { id: m.id, dbCol: m.target_database_column }]),
      )

      const operations = {
        toDeleteIds: [] as string[],
        toUpsert: [] as UserFieldMappingInsert[],
      }

      for (const rawCsvHeader of csvHeaders) {
        const normalizedCsvHeader = normalizeHeader(rawCsvHeader)
        if (!normalizedCsvHeader) continue

        const targetDbColumn = updatedSheetMappings[rawCsvHeader]
        const existingPersistentEntry = currentPersistentMap.get(normalizedCsvHeader)

        if (targetDbColumn === "ignore_field" || targetDbColumn === undefined) {
          if (existingPersistentEntry) {
            operations.toDeleteIds.push(existingPersistentEntry.id)
          }
        } else {
          if (existingPersistentEntry) {
            if (existingPersistentEntry.dbCol !== targetDbColumn) {
              operations.toUpsert.push({
                user_id: user.id,
                target_table_name: "listings",
                source_csv_header: normalizedCsvHeader,
                target_database_column: targetDbColumn,
              })
            }
          } else {
            operations.toUpsert.push({
              user_id: user.id,
              target_table_name: "listings",
              source_csv_header: normalizedCsvHeader,
              target_database_column: targetDbColumn,
            })
          }
        }
      }

      if (operations.toDeleteIds.length > 0) {
        const { error: deleteError } = await supabase
          .from("user_field_mappings")
          .delete()
          .in("id", operations.toDeleteIds)
        if (deleteError) throw deleteError
      }

      if (operations.toUpsert.length > 0) {
        const { error: upsertError } = await supabase
          .from("user_field_mappings")
          .upsert(operations.toUpsert, { onConflict: "user_id,target_table_name,source_csv_header" })
        if (upsertError) throw upsertError
      }

      setFieldMappings(updatedSheetMappings)
      await fetchUserSavedMappings()

      toast({ title: "Field mappings saved", description: "Your preferences have been updated for future imports." })
    } catch (err: any) {
      console.error("Error saving field mappings:", err)
      toast({ title: "Error", description: `Failed to save mappings: ${err.message}`, variant: "destructive" })
    } finally {
      setIsSavingMappings(false)
      setIsMappingSheetOpen(false)
    }
  }

  const handleImport = async () => {
    if (!file || !user) {
      setError("Please select a file and ensure you are logged in.")
      return
    }
    if (parsedCsvData.length === 0) {
      setError("No data parsed from CSV. Please re-upload or check the file.")
      return
    }
    if (Object.keys(fieldMappings).length === 0) {
      setError("Field mappings are not set. Please map fields before importing.")
      toast({
        title: "Mapping Required",
        description: "Click 'Map Fields' to configure mappings.",
        variant: "destructive",
      })
      return
    }

    setIsProcessing(true)
    setProgress(0)
    setResult(null)
    setError(null)
    const startTime = Date.now()

    const { data: uploadLog, error: uploadLogError } = await supabase
      .from("csv_uploads")
      .insert({ user_id: user.id, filename: file.name, status: "processing", upload_date: new Date().toISOString() })
      .select()
      .single()

    if (uploadLogError || !uploadLog) {
      console.error("Error creating upload log entry:", uploadLogError?.message || "Unknown error")
      setError(`Failed to start import process. Could not log upload: ${uploadLogError?.message}`)
      setIsProcessing(false)
      return
    }
    console.log("Created upload log entry with ID:", uploadLog.id)

    const recordsToProcess = parsedCsvData
    const totalRecords = recordsToProcess.length
    let newRecordsAdded = 0
    let recordsUpdated = 0
    let ignoredForOtherReasons = 0
    let failedDueToError = 0
    const errorsList: string[] = []

    if (totalRecords === 0) {
      setError("CSV file is empty or has no data rows.")
      setIsProcessing(false)
      const { error: emptyUpdateError } = await supabase
        .from("csv_uploads")
        .update({ status: "failed", error_log: "CSV empty or no data rows" })
        .eq("id", uploadLog.id)
      if (emptyUpdateError) console.error("Error updating log for empty CSV:", emptyUpdateError.message)
      await fetchHistory()
      return
    }

    const mlsHeaderKeys: string[] = []
    for (const [csvHeader, dbCol] of Object.entries(fieldMappings)) {
      if (dbCol === "mls_number") {
        mlsHeaderKeys.push(normalizeHeader(csvHeader))
      }
    }

    const recordsToInsert: ListingInsert[] = []
    const recordsToUpdate: { id: string; payload: Partial<ListingRow> }[] = []

    for (let chunkStart = 0; chunkStart < totalRecords; chunkStart += CHUNK_SIZE) {
      const chunkEnd = Math.min(chunkStart + CHUNK_SIZE, totalRecords)
      const chunk = recordsToProcess.slice(chunkStart, chunkEnd)

      const mlsNumbersForChunk: string[] = []
      if (mlsHeaderKeys.length > 0) {
        chunk.forEach((record) => {
          for (const key of mlsHeaderKeys) {
            if (record[key]) {
              mlsNumbersForChunk.push(String(record[key]))
              break
            }
          }
        })
      }

      const existingPropertiesMapForChunk = new Map<string, ListingRow>()
      if (mlsNumbersForChunk.length > 0) {
        const { data: existingPropsData, error: fetchChunkError } = await supabase
          .from("listings")
          .select("*")
          .in("mls_number", mlsNumbersForChunk)

        if (fetchChunkError) {
          errorsList.push(
            `Failed to fetch existing properties for chunk (records ${chunkStart + 1}-${chunkEnd}): ${
              fetchChunkError.message
            }`,
          )
          failedDueToError += chunk.length
          continue
        } else if (existingPropsData) {
          existingPropsData.forEach(
            (prop) => prop.mls_number && existingPropertiesMapForChunk.set(prop.mls_number, prop as ListingRow),
          )
        }
      }

      for (let i = 0; i < chunk.length; i++) {
        const record = chunk[i]
        const overallRecordIndex = chunkStart + i
        setProgress(((overallRecordIndex + 1) / totalRecords) * 100)

        const propertyData: ListingInsert = {}
        let mlsNumberForRecord: string | null = null

        for (const [rawCsvHeader, dbTargetColumn] of Object.entries(fieldMappings)) {
          if (dbTargetColumn === "ignore_field") continue

          const normalizedCsvHeaderKey = normalizeHeader(rawCsvHeader)
          const rawValue = record[normalizedCsvHeaderKey]

          const columnDefinition = listingTableColumns.find((c) => c.value === dbTargetColumn)
          const typeHint = columnDefinition ? columnDefinition.typeHint : "string"
          let parsedValue = parseCSVValue(rawValue, typeHint)

          if (dbTargetColumn === "subdivision" && typeof parsedValue === "string") {
            parsedValue = toTitleCase(parsedValue)
          }
          if (dbTargetColumn === "status" && typeof parsedValue === "string") {
            const upperParsedValue = parsedValue.toUpperCase()
            parsedValue = statusMapping[upperParsedValue] || parsedValue
          }

          if (parsedValue !== null && parsedValue !== undefined) {
            ;(propertyData as any)[dbTargetColumn] = parsedValue
            if (dbTargetColumn === "mls_number" && parsedValue) {
              mlsNumberForRecord = String(parsedValue)
            }
          }
        }

        if (!mlsNumberForRecord) {
          errorsList.push(`Row ${overallRecordIndex + 2}: Missing or invalid MLS_NUMBER after mapping. Record skipped.`)
          ignoredForOtherReasons++
          continue
        }
        propertyData.mls_number = mlsNumberForRecord

        if (propertyData.new_construction === undefined && propertyData.new_construction_details) {
          const detailsLower = String(propertyData.new_construction_details).toLowerCase()
          if (detailsLower.startsWith("yes") || detailsLower === "true" || detailsLower === "1") {
            propertyData.new_construction = true
          } else if (detailsLower.startsWith("no") || detailsLower === "false" || detailsLower === "0") {
            propertyData.new_construction = false
          }
        }

        const existingProperty = existingPropertiesMapForChunk.get(mlsNumberForRecord)

        if (existingProperty) {
          const updatePayload: Partial<ListingRow> = {}
          let needsUpdate = false
          for (const key in propertyData) {
            if (!Object.prototype.hasOwnProperty.call(propertyData, key)) continue
            const dbKey = key as keyof ListingRow
            const csvValue = propertyData[dbKey as keyof ListingInsert]

            if (overrideExisting) {
              if (Object.prototype.hasOwnProperty.call(propertyData, dbKey)) {
                if (existingProperty[dbKey] !== csvValue) {
                  ;(updatePayload as any)[dbKey] = csvValue
                  needsUpdate = true
                }
              }
            } else {
              if (csvValue !== null && csvValue !== undefined) {
                if (
                  existingProperty[dbKey] === null ||
                  existingProperty[dbKey] === undefined ||
                  JSON.stringify(existingProperty[dbKey]) !== JSON.stringify(csvValue)
                ) {
                  if (Array.isArray(csvValue) && Array.isArray(existingProperty[dbKey])) {
                    const sortedCsv = [...csvValue].sort().join(",")
                    const sortedDb = [...(existingProperty[dbKey] as any[])].sort().join(",")
                    if (sortedCsv !== sortedDb) {
                      ;(updatePayload as any)[dbKey] = csvValue
                      needsUpdate = true
                    }
                  } else if (existingProperty[dbKey] !== csvValue) {
                    ;(updatePayload as any)[dbKey] = csvValue
                    needsUpdate = true
                  }
                }
              }
            }
          }
          if (needsUpdate && Object.keys(updatePayload).length > 0) {
            recordsToUpdate.push({ id: existingProperty.id, payload: updatePayload })
          } else {
            ignoredForOtherReasons++
          }
        } else {
          const { user_id, ...insertData } = propertyData as any
          recordsToInsert.push(insertData)
        }
      }
    }

    if (recordsToInsert.length > 0) {
      const { error: insertError } = await supabase.from("listings").insert(recordsToInsert)
      if (insertError) {
        errorsList.push(`Batch insert failed: ${insertError.message}`)
        failedDueToError += recordsToInsert.length
      } else {
        newRecordsAdded = recordsToInsert.length
      }
    }

    if (recordsToUpdate.length > 0) {
      const updatePromises = recordsToUpdate.map((item) =>
        supabase.from("listings").update(item.payload).eq("id", item.id),
      )
      const updateChunkSize = 50
      for (let i = 0; i < updatePromises.length; i += updateChunkSize) {
        const chunkPromises = updatePromises.slice(i, i + updateChunkSize)
        const updateResults = await Promise.allSettled(chunkPromises)
        updateResults.forEach((res, idxInChunk) => {
          const originalIdx = i + idxInChunk
          if (res.status === "fulfilled" && !res.value.error) {
            recordsUpdated++
          } else {
            const errorMsg = res.status === "rejected" ? res.reason?.message : res.value.error?.message
            const mlsForFailedUpdate = recordsToUpdate[originalIdx].payload.mls_number || "unknown MLS"
            errorsList.push(
              `Update for MLS ${mlsForFailedUpdate} (ID: ${recordsToUpdate[originalIdx].id}) failed: ${errorMsg}`,
            )
            failedDueToError++
          }
        })
      }
    }

    const endTime = Date.now()
    const duration = (endTime - startTime) / 1000
    setResult({
      totalRecords,
      newRecordsAdded,
      recordsUpdated,
      ignoredOrDuplicate: ignoredForOtherReasons,
      failedDueToError,
      errors: errorsList,
    })
    toast({ title: "Import Complete", description: `Processed ${totalRecords} records in ${duration.toFixed(2)}s.` })

    try {
      const updatePayloadForHistory = {
        status: failedDueToError > 0 || errorsList.length > 0 ? "completed_with_errors" : "completed",
        records_processed: totalRecords,
        records_created: newRecordsAdded,
        records_updated: recordsUpdated,
        records_failed: failedDueToError,
        error_log: errorsList.length > 0 ? errorsList.slice(0, 50).join("\n") : null,
        metadata: {
          duration_seconds: duration,
          ignored_records: ignoredForOtherReasons,
          override_existing: overrideExisting,
        },
      }

      console.log("Attempting to update csv_uploads with ID:", uploadLog.id)
      console.log("Update payload for csv_uploads:", JSON.stringify(updatePayloadForHistory, null, 2))

      const { data: updateData, error: updateDbError } = await supabase
        .from("csv_uploads")
        .update(updatePayloadForHistory)
        .eq("id", uploadLog.id)
        .select() // Important: .select() to get back the updated row(s)

      if (updateDbError) {
        console.error("Supabase error during csv_uploads update:", updateDbError)
        throw updateDbError // Throw to be caught by the catch block
      }

      if (!updateData || updateData.length === 0) {
        console.warn(
          "csv_uploads update did not affect any rows. This might be due to RLS or an incorrect ID. uploadLog.id:",
          uploadLog.id,
        )
        throw new Error("Failed to update upload history: No record found or RLS prevented update.")
      }

      console.log("csv_uploads successfully updated, returned data:", updateData)
    } catch (finalUpdateError: any) {
      console.error("Error in catch block for updating csv_uploads log:", finalUpdateError)
      toast({
        title: "History Update Failed",
        description: `The import completed, but its final status could not be saved. Error: ${finalUpdateError.message}`,
        variant: "destructive",
      })
    } finally {
      setIsProcessing(false)
      await fetchHistory() // Refresh history regardless of update success/failure
    }
  }

  const totalHistoryPages = Math.ceil(totalHistoryCount / historyRowsPerPage)

  return (
    <div className="container mx-auto p-4 space-y-8">
      <Card>
        <CardHeader>
          <CardTitle className="text-xl font-semibold">Import Listing Data</CardTitle>
          <CardDescription>
            Upload a CSV file to import listing data. Map fields as needed, then start the import.
          </CardDescription>
        </CardHeader>
        <CardContent className="space-y-6">
          <div {...getRootProps({ style })}>
            <input {...getInputProps()} />
            <UploadCloud className="w-12 h-12 mb-3 text-gray-400" />
            {isDragActive ? (
              <p>Drop the files here ...</p>
            ) : (
              <p>Drag 'n' drop a CSV file here, or click to select file</p>
            )}
            <p className="text-xs mt-1">Max file size: 10MB. Supported format: .csv</p>
          </div>

          {file && (
            <div className="mt-4 p-3 border rounded-md bg-gray-50">
              <div className="flex items-center justify-between">
                <div className="flex items-center space-x-2">
                  <FileText className="w-5 h-5 text-gray-600" />
                  <span className="text-sm font-medium">{file.name}</span>
                  <span className="text-xs text-gray-500">({(file.size / 1024).toFixed(2)} KB)</span>
                </div>
                <Button
                  variant="ghost"
                  size="sm"
                  onClick={() => {
                    setFile(null)
                    setCsvHeaders([])
                    setFieldMappings({})
                    setParsedCsvData([])
                    setResult(null)
                    setError(null)
                    setPreprocessingStats(null)
                  }}
                >
                  <XCircle className="w-4 h-4" />
                </Button>
              </div>
            </div>
          )}

          {preprocessingStats && file && (
            <Card className="mt-4 bg-slate-50">
              <CardHeader className="pb-2 pt-4">
                <CardTitle className="text-md font-semibold">File Pre-processing Summary</CardTitle>
              </CardHeader>
              <CardContent className="text-sm space-y-1 pb-4">
                <div className="flex justify-between">
                  <span>Total Records in File:</span> <strong>{preprocessingStats.totalCsvRecords}</strong>
                </div>
                <div className="flex justify-between">
                  <span>Potential New Records (New MLS #):</span>{" "}
                  <strong>
                    {preprocessingStats.newCsvRecords === -1 ? "Error" : preprocessingStats.newCsvRecords}
                  </strong>
                </div>
                <div className="flex justify-between">
                  <span>Potential Matched Records (Existing MLS #):</span>{" "}
                  <strong>
                    {preprocessingStats.matchedCsvRecords === -1 ? "Error" : preprocessingStats.matchedCsvRecords}
                  </strong>
                </div>
                <hr className="my-1" />
                <div className="flex justify-between">
                  <span>Total Columns in File:</span> <strong>{preprocessingStats.totalCsvFields}</strong>
                </div>
                <div className="flex justify-between">
                  <span>Columns Auto-Mapped:</span> <strong>{preprocessingStats.autoMatchedCsvFields}</strong>
                </div>
                <div className="flex justify-between">
                  <span>Columns Not Auto-Mapped:</span> <strong>{preprocessingStats.unmatchedCsvFields}</strong>
                </div>
              </CardContent>
            </Card>
          )}
          {(isProcessing || isSavingMappings) && (
            <div className="mt-4">
              {isProcessing && <Progress value={progress} className="w-full" />}
              <p className="text-sm text-center mt-2">
                {isSavingMappings ? "Saving mappings..." : `Processing... ${Math.round(progress)}%`}
              </p>
            </div>
          )}

          {error && (
            <Alert variant="destructive" className="mt-4">
              <AlertCircle className="h-4 w-4" />
              <AlertTitle>Error</AlertTitle>
              <AlertDescription>{error}</AlertDescription>
            </Alert>
          )}

          <div className="flex flex-col sm:flex-row sm:justify-between sm:items-center gap-4 mt-6 pt-4 border-t">
            <div className="flex items-center space-x-2">
              <Button
                onClick={() => setIsMappingSheetOpen(true)}
                disabled={!file || csvHeaders.length === 0 || isProcessing || isSavingMappings}
                variant="outline"
              >
                <Settings2 className="mr-2 h-4 w-4" /> Map Fields
              </Button>
              <div className="flex items-center space-x-2">
                <Switch
                  id="override-existing"
                  checked={overrideExisting}
                  onCheckedChange={setOverrideExisting}
                  disabled={isProcessing || isSavingMappings}
                />
                <Label htmlFor="override-existing" className="text-sm">
                  Override Existing Values
                </Label>
              </div>
            </div>
            <Button
              onClick={handleImport}
              disabled={
                !file ||
                parsedCsvData.length === 0 ||
                isProcessing ||
                isSavingMappings ||
                Object.keys(fieldMappings).length === 0
              }
              className="w-full sm:w-auto"
            >
              {isProcessing ? (
                <>
                  <Loader2 className="mr-2 h-4 w-4 animate-spin" /> Importing...
                </>
              ) : (
                "Start Import"
              )}
            </Button>
          </div>
        </CardContent>
      </Card>

      {result && (
        <Card>
          <CardHeader>
            <CardTitle className="text-xl font-semibold">Import Results</CardTitle>
            <CardDescription>Summary of the data import process.</CardDescription>
          </CardHeader>
          <CardContent className="space-y-4">
            <div className="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-5 gap-4 text-center">
              <div className="p-3 bg-blue-50 rounded-md">
                <p className="text-xs text-blue-700 font-medium">Total Records</p>
                <p className="text-2xl font-bold text-blue-900">{result.totalRecords}</p>
              </div>
              <div className="p-3 bg-green-50 rounded-md">
                <p className="text-xs text-green-700 font-medium">New Added</p>
                <p className="text-2xl font-bold text-green-900">{result.newRecordsAdded}</p>
              </div>
              <div className="p-3 bg-yellow-50 rounded-md">
                <p className="text-xs text-yellow-700 font-medium">Updated</p>
                <p className="text-2xl font-bold text-yellow-900">{result.recordsUpdated}</p>
              </div>
              <div className="p-3 bg-gray-100 rounded-md">
                <p className="text-xs text-gray-700 font-medium">Ignored/No Change</p>
                <p className="text-2xl font-bold text-gray-900">{result.ignoredOrDuplicate}</p>
              </div>
              <div className="p-3 bg-red-50 rounded-md">
                <p className="text-xs text-red-700 font-medium">Failed (Errors)</p>
                <p className="text-2xl font-bold text-red-900">{result.failedDueToError}</p>
              </div>
            </div>

            {result.errors && result.errors.length > 0 && (
              <Alert variant="destructive">
                <Info className="h-4 w-4" />
                <AlertTitle>Encountered {result.errors.length} Error(s) During Import</AlertTitle>
                <AlertDescription>
                  <ul className="list-disc list-inside max-h-60 overflow-y-auto text-xs">
                    {result.errors.slice(0, 10).map((err, index) => (
                      <li key={index}>{err}</li>
                    ))}
                    {result.errors.length > 10 && (
                      <li>...and {result.errors.length - 10} more errors. Check server logs for full details.</li>
                    )}
                  </ul>
                </AlertDescription>
              </Alert>
            )}
            {result.errors.length === 0 && result.failedDueToError === 0 && (
              <Alert className="bg-green-50 border-green-200 text-green-800">
                <CheckCircle className="h-4 w-4 text-green-600" />
                <AlertTitle>Import Successful</AlertTitle>
                <AlertDescription>All records processed without errors.</AlertDescription>
              </Alert>
            )}
          </CardContent>
        </Card>
      )}
      <FieldMappingSheet
        isOpen={isMappingSheetOpen}
        onClose={() => setIsMappingSheetOpen(false)}
        csvHeaders={csvHeaders}
        currentMappings={fieldMappings}
        onSaveMappings={handleSaveMappings}
        availableDbColumns={listingTableColumns}
      />
      <Card>
        <CardHeader>
          <CardTitle className="text-xl font-semibold">Upload History</CardTitle>
          <CardDescription>Recent CSV import attempts and their outcomes.</CardDescription>
        </CardHeader>
        <CardContent>
          {isLoadingHistory && (
            <p className="text-sm text-gray-500 flex items-center">
              <Loader2 className="mr-2 h-4 w-4 animate-spin" />
              Loading history...
            </p>
          )}
          {!isLoadingHistory && uploadHistory.length === 0 && (
            <p className="text-sm text-gray-500">No upload history found.</p>
          )}
          {!isLoadingHistory && uploadHistory.length > 0 && (
            <>
              <Table>
                <TableHeader>
                  <TableRow>
                    <TableHead className="font-normal">Filename</TableHead>
                    <TableHead className="font-normal">Date</TableHead>
                    <TableHead className="font-normal">Status</TableHead>
                    <TableHead className="text-right font-normal w-20">Total</TableHead>
                    <TableHead className="text-right font-normal w-20 text-green-600">New</TableHead>
                    <TableHead className="text-right font-normal w-20 text-yellow-600">Updated</TableHead>
                    <TableHead className="text-right font-normal w-20 text-gray-600">Ignored</TableHead>
                    <TableHead className="text-right font-normal w-20 text-red-600">Failed</TableHead>
                  </TableRow>
                </TableHeader>
                <TableBody>
                  {uploadHistory.map((item) => {
                    const metadata = item.metadata as CsvUploadMetadata | null
                    return (
                      <TableRow key={item.id}>
                        <TableCell className="font-normal truncate max-w-xs">{item.filename || "N/A"}</TableCell>
                        <TableCell className="font-normal">{formatDate(item.upload_date)}</TableCell>
                        <TableCell className="font-normal">
                          <Badge
                            variant={
                              item.status === "completed"
                                ? "default"
                                : item.status === "completed_with_errors"
                                  ? "yellow"
                                  : item.status === "failed"
                                    ? "destructive"
                                    : "secondary"
                            }
                          >
                            {item.status || "N/A"}
                          </Badge>
                        </TableCell>
                        <TableCell className="text-right font-normal">{item.records_processed ?? "-"}</TableCell>
                        <TableCell className="text-right font-normal text-green-700">
                          {item.records_created ?? "-"}
                        </TableCell>
                        <TableCell className="text-right font-normal text-yellow-700">
                          {item.records_updated ?? "-"}
                        </TableCell>
                        <TableCell className="text-right font-normal text-gray-700">
                          {metadata?.ignored_records ?? "-"}
                        </TableCell>
                        <TableCell className="text-right font-normal text-red-700">
                          {item.records_failed ?? "-"}
                        </TableCell>
                      </TableRow>
                    )
                  })}
                </TableBody>
              </Table>
              {totalHistoryPages > 1 && (
                <div className="flex items-center justify-end space-x-2 py-4">
                  <Button
                    variant="outline"
                    size="sm"
                    onClick={() => setHistoryPage((prev) => Math.max(1, prev - 1))}
                    disabled={historyPage === 1 || isLoadingHistory}
                  >
                    <ChevronLeft className="h-4 w-4 mr-1" /> Previous
                  </Button>
                  <span className="text-sm text-muted-foreground">
                    Page {historyPage} of {totalHistoryPages}
                  </span>
                  <Button
                    variant="outline"
                    size="sm"
                    onClick={() => setHistoryPage((prev) => Math.min(totalHistoryPages, prev + 1))}
                    disabled={historyPage === totalHistoryPages || isLoadingHistory}
                  >
                    Next <ChevronRight className="h-4 w-4 ml-1" />
                  </Button>
                </div>
              )}
            </>
          )}
        </CardContent>
      </Card>
    </div>
  )
}
```

## File: dkl-microapp-2-main/app/(dashboard)/insights/page.tsx
```typescript
"use client"

import type React from "react"

import { useEffect, useState } from "react"
import { supabase } from "@/lib/supabase/client"
import { Card, CardContent, CardHeader, CardTitle } from "@/components/ui/card"
import { formatCurrency } from "@/lib/utils"
import { TrendingUp, TrendingDown, Minus, BarChart3, PieChart, Activity } from "lucide-react"

export default function InsightsPage() {
  const [insights, setInsights] = useState<any>(null)
  const [loading, setLoading] = useState(true)

  useEffect(() => {
    fetchInsights()
  }, [])

  async function fetchInsights() {
    try {
      // Fetch various market insights
      const { data: properties } = await supabase.from("properties").select("*")

      if (!properties) return

      // Calculate insights
      const activeListings = properties.filter((p) => p.status === "Active")
      const newConstruction = properties.filter((p) => p.new_construction)
      const soldProperties = properties.filter((p) => p.status === "Sold")

      const avgListPrice = activeListings.reduce((sum, p) => sum + (p.list_price || 0), 0) / activeListings.length
      const avgSoldPrice = soldProperties.reduce((sum, p) => sum + (p.sold_price || 0), 0) / soldProperties.length

      const avgDOM = activeListings.reduce((sum, p) => sum + (p.dom || 0), 0) / activeListings.length

      // Price ranges
      const priceRanges = {
        under1M: properties.filter((p) => (p.list_price || 0) < 1000000).length,
        "1M-2M": properties.filter((p) => (p.list_price || 0) >= 1000000 && (p.list_price || 0) < 2000000).length,
        "2M-5M": properties.filter((p) => (p.list_price || 0) >= 2000000 && (p.list_price || 0) < 5000000).length,
        over5M: properties.filter((p) => (p.list_price || 0) >= 5000000).length,
      }

      // Geographic distribution
      const cityDistribution = properties.reduce((acc: any, p) => {
        const city = p.city || "Unknown"
        acc[city] = (acc[city] || 0) + 1
        return acc
      }, {})

      setInsights({
        totalProperties: properties.length,
        activeListings: activeListings.length,
        newConstruction: newConstruction.length,
        soldProperties: soldProperties.length,
        avgListPrice,
        avgSoldPrice,
        avgDOM,
        priceRanges,
        cityDistribution,
        newConstructionShare: (newConstruction.length / properties.length) * 100,
      })
    } catch (error) {
      console.error("Error fetching insights:", error)
    } finally {
      setLoading(false)
    }
  }

  if (loading) {
    return (
      <div className="space-y-4">
        <div>
          <h1 className="text-lg font-semibold">Market Insights</h1>
          <p className="text-xs text-gray-600">Loading market analysis...</p>
        </div>
        <div className="grid gap-4 md:grid-cols-2 lg:grid-cols-4">
          {Array.from({ length: 8 }).map((_, i) => (
            <Card key={i}>
              <CardContent className="p-4">
                <div className="space-y-2">
                  <div className="h-4 w-24 animate-pulse rounded bg-gray-200" />
                  <div className="h-6 w-16 animate-pulse rounded bg-gray-200" />
                </div>
              </CardContent>
            </Card>
          ))}
        </div>
      </div>
    )
  }

  return (
    <div className="space-y-4">
      <div>
        <h1 className="text-lg font-semibold">Market Insights</h1>
        <p className="text-xs text-gray-600">Luxury residential new construction market analysis</p>
      </div>

      <div className="grid gap-3 md:grid-cols-2 lg:grid-cols-4">
        <InsightCard
          title="Avg List Price"
          value={formatCurrency(insights?.avgListPrice)}
          change={+3.2}
          icon={TrendingUp}
        />
        <InsightCard
          title="Avg Sold Price"
          value={formatCurrency(insights?.avgSoldPrice)}
          change={+1.8}
          icon={TrendingUp}
        />
        <InsightCard
          title="Avg Days on Market"
          value={Math.round(insights?.avgDOM)}
          change={-5.2}
          icon={TrendingDown}
        />
        <InsightCard
          title="New Construction Share"
          value={`${insights?.newConstructionShare?.toFixed(1)}%`}
          change={+2.1}
          icon={TrendingUp}
        />
      </div>

      <div className="grid gap-4 lg:grid-cols-2">
        <Card>
          <CardHeader className="pb-3">
            <CardTitle className="text-sm flex items-center gap-x-2">
              <PieChart className="h-4 w-4" />
              Price Distribution
            </CardTitle>
          </CardHeader>
          <CardContent>
            <div className="space-y-3">
              <PriceRangeBar
                label="Under $1M"
                count={insights?.priceRanges?.under1M}
                total={insights?.totalProperties}
              />
              <PriceRangeBar
                label="$1M - $2M"
                count={insights?.priceRanges?.["1M-2M"]}
                total={insights?.totalProperties}
              />
              <PriceRangeBar
                label="$2M - $5M"
                count={insights?.priceRanges?.["2M-5M"]}
                total={insights?.totalProperties}
              />
              <PriceRangeBar label="Over $5M" count={insights?.priceRanges?.over5M} total={insights?.totalProperties} />
            </div>
          </CardContent>
        </Card>

        <Card>
          <CardHeader className="pb-3">
            <CardTitle className="text-sm flex items-center gap-x-2">
              <BarChart3 className="h-4 w-4" />
              Geographic Distribution
            </CardTitle>
          </CardHeader>
          <CardContent>
            <div className="space-y-2">
              {Object.entries(insights?.cityDistribution || {})
                .sort(([, a]: any, [, b]: any) => b - a)
                .slice(0, 6)
                .map(([city, count]: any) => (
                  <div key={city} className="flex justify-between items-center text-xs">
                    <span className="text-gray-600">{city}</span>
                    <span className="font-medium">{count}</span>
                  </div>
                ))}
            </div>
          </CardContent>
        </Card>
      </div>

      <div className="grid gap-4 lg:grid-cols-3">
        <Card>
          <CardHeader className="pb-3">
            <CardTitle className="text-sm flex items-center gap-x-2">
              <Activity className="h-4 w-4" />
              Market Activity
            </CardTitle>
          </CardHeader>
          <CardContent>
            <div className="space-y-2 text-xs">
              <div className="flex justify-between border-b pb-1">
                <span className="text-gray-600">Active Listings</span>
                <span className="font-medium">{insights?.activeListings}</span>
              </div>
              <div className="flex justify-between border-b pb-1">
                <span className="text-gray-600">New Construction</span>
                <span className="font-medium">{insights?.newConstruction}</span>
              </div>
              <div className="flex justify-between border-b pb-1">
                <span className="text-gray-600">Recently Sold</span>
                <span className="font-medium">{insights?.soldProperties}</span>
              </div>
              <div className="flex justify-between">
                <span className="text-gray-600">Total Properties</span>
                <span className="font-medium">{insights?.totalProperties}</span>
              </div>
            </div>
          </CardContent>
        </Card>

        <Card>
          <CardHeader className="pb-3">
            <CardTitle className="text-sm">Market Trends</CardTitle>
          </CardHeader>
          <CardContent>
            <div className="space-y-2 text-xs">
              <div className="flex justify-between items-center border-b pb-1">
                <span className="text-gray-600">Price Growth (YoY)</span>
                <span className="font-medium text-green-600 flex items-center gap-x-1">
                  <TrendingUp className="h-3 w-3" />
                  +8.5%
                </span>
              </div>
              <div className="flex justify-between items-center border-b pb-1">
                <span className="text-gray-600">Inventory Change</span>
                <span className="font-medium text-red-600 flex items-center gap-x-1">
                  <TrendingDown className="h-3 w-3" />
                  -12.3%
                </span>
              </div>
              <div className="flex justify-between items-center border-b pb-1">
                <span className="text-gray-600">Sales Volume</span>
                <span className="font-medium text-gray-600 flex items-center gap-x-1">
                  <Minus className="h-3 w-3" />
                  +0.8%
                </span>
              </div>
              <div className="flex justify-between items-center">
                <span className="text-gray-600">New Listings</span>
                <span className="font-medium text-green-600 flex items-center gap-x-1">
                  <TrendingUp className="h-3 w-3" />
                  +15.2%
                </span>
              </div>
            </div>
          </CardContent>
        </Card>

        <Card>
          <CardHeader className="pb-3">
            <CardTitle className="text-sm">Key Metrics</CardTitle>
          </CardHeader>
          <CardContent>
            <div className="space-y-2 text-xs">
              <div className="flex justify-between border-b pb-1">
                <span className="text-gray-600">Median Price/SqFt</span>
                <span className="font-medium">$425</span>
              </div>
              <div className="flex justify-between border-b pb-1">
                <span className="text-gray-600">Months of Supply</span>
                <span className="font-medium">3.2</span>
              </div>
              <div className="flex justify-between border-b pb-1">
                <span className="text-gray-600">Absorption Rate</span>
                <span className="font-medium">85%</span>
              </div>
              <div className="flex justify-between">
                <span className="text-gray-600">Price Reduction Rate</span>
                <span className="font-medium">22%</span>
              </div>
            </div>
          </CardContent>
        </Card>
      </div>
    </div>
  )
}

function InsightCard({
  title,
  value,
  change,
  icon: Icon,
}: {
  title: string
  value: string | number
  change: number
  icon: React.ElementType
}) {
  const isPositive = change > 0
  const isNegative = change < 0

  return (
    <Card>
      <CardHeader className="flex flex-row items-center justify-between space-y-0 pb-2">
        <CardTitle className="text-xs font-medium text-gray-600">{title}</CardTitle>
        <Icon className="h-3.5 w-3.5 text-gray-400" />
      </CardHeader>
      <CardContent>
        <div className="text-lg font-bold">{value}</div>
        <p className="text-xs text-muted-foreground">
          <span
            className={`inline-flex items-center gap-x-1 ${
              isPositive ? "text-green-600" : isNegative ? "text-red-600" : "text-gray-600"
            }`}
          >
            {isPositive ? (
              <TrendingUp className="h-3 w-3" />
            ) : isNegative ? (
              <TrendingDown className="h-3 w-3" />
            ) : (
              <Minus className="h-3 w-3" />
            )}
            {Math.abs(change)}% from last month
          </span>
        </p>
      </CardContent>
    </Card>
  )
}

function PriceRangeBar({ label, count, total }: { label: string; count: number; total: number }) {
  const percentage = total > 0 ? (count / total) * 100 : 0

  return (
    <div className="space-y-1">
      <div className="flex justify-between text-xs">
        <span className="text-gray-600">{label}</span>
        <span className="font-medium">{count}</span>
      </div>
      <div className="w-full bg-gray-200 rounded-full h-1.5">
        <div className="bg-blue-600 h-1.5 rounded-full" style={{ width: `${percentage}%` }} />
      </div>
    </div>
  )
}
```

## File: dkl-microapp-2-main/app/(dashboard)/listings/[id]/edit/page.tsx
```typescript
"use client"

import type React from "react"

import { useState, useEffect } from "react"
import { useParams, useRouter } from "next/navigation"
import { supabase } from "@/lib/supabase/client"
import { Card, CardContent, CardHeader, CardTitle } from "@/components/ui/card"
import { Button } from "@/components/ui/button"
import { Input } from "@/components/ui/input"
import { Label } from "@/components/ui/label"
import { Select, SelectContent, SelectItem, SelectTrigger, SelectValue } from "@/components/ui/select"
import { Checkbox } from "@/components/ui/checkbox"
import { ArrowLeft, Save } from "lucide-react"
import Link from "next/link"
import { useToast } from "@/hooks/use-toast"

export default function EditListingPage() {
  const params = useParams()
  const router = useRouter()
  const { toast } = useToast()
  const [builders, setBuilders] = useState<any[]>([])
  const [loading, setLoading] = useState(false)
  const [initialLoading, setInitialLoading] = useState(true)
  const [formData, setFormData] = useState({
    mls_number: "",
    status: "Active",
    list_price: "",
    street_number: "",
    street_name: "",
    city: "",
    state: "",
    zip_code: "",
    bedrooms: "",
    baths_full: "",
    baths_half: "",
    interior_sqft: "",
    new_construction: false,
    builder_id: "",
    property_condition: "",
    garage_spaces: "",
    fireplace: false,
    central_air: false,
    basement: false,
  })

  useEffect(() => {
    fetchBuilders()
    if (params.id) {
      fetchListing()
    }
  }, [params.id])

  async function fetchBuilders() {
    try {
      const { data } = await supabase.from("builders").select("id, name, company_name").order("name")
      setBuilders(data || [])
    } catch (error) {
      console.error("Error fetching builders:", error)
    }
  }

  async function fetchListing() {
    try {
      const { data, error } = await supabase.from("listings").select("*").eq("id", params.id).single()

      if (error) throw error

      setFormData({
        mls_number: data.mls_number || "",
        status: data.status || "Active",
        list_price: data.list_price?.toString() || "",
        street_number: data.street_number || "",
        street_name: data.street_name || "",
        city: data.city || "",
        state: data.state || "",
        zip_code: data.zip_code || "",
        bedrooms: data.bedrooms?.toString() || "",
        baths_full: data.baths_full?.toString() || "",
        baths_half: data.baths_half?.toString() || "",
        interior_sqft: data.interior_sqft?.toString() || "",
        new_construction: data.new_construction || false,
        builder_id: data.builder_id || "",
        property_condition: data.property_condition || "",
        garage_spaces: data.garage_spaces?.toString() || "",
        fireplace: data.fireplace || false,
        central_air: data.central_air || false,
        basement: data.basement || false,
      })
    } catch (error) {
      console.error("Error fetching property:", error)
      toast({
        title: "Error",
        description: "Failed to load listing data.",
        variant: "destructive",
      })
    } finally {
      setInitialLoading(false)
    }
  }

  const handleSubmit = async (e: React.FormEvent) => {
    e.preventDefault()
    setLoading(true)

    try {
      // Convert string numbers to actual numbers
      const listingData = {
        ...formData,
        list_price: formData.list_price ? Number.parseFloat(formData.list_price) : null,
        bedrooms: formData.bedrooms ? Number.parseInt(formData.bedrooms) : null,
        baths_full: formData.baths_full ? Number.parseInt(formData.baths_full) : null,
        baths_half: formData.baths_half ? Number.parseInt(formData.baths_half) : null,
        interior_sqft: formData.interior_sqft ? Number.parseInt(formData.interior_sqft) : null,
        garage_spaces: formData.garage_spaces ? Number.parseInt(formData.garage_spaces) : null,
        builder_id: formData.builder_id || null,
      }

      const { error } = await supabase.from("listings").update(listingData).eq("id", params.id)

      if (error) throw error

      toast({
        title: "Listing updated",
        description: "Listing has been successfully updated.",
      })

      router.push(`/listings/${params.id}`)
    } catch (error: any) {
      toast({
        title: "Error",
        description: error.message || "Failed to update listing.",
        variant: "destructive",
      })
    } finally {
      setLoading(false)
    }
  }

  if (initialLoading) {
    return <div className="text-xs text-gray-600">Loading...</div>
  }

  return (
    <div className="space-y-4">
      <div className="flex items-center gap-x-2">
        <Button variant="ghost" size="sm" asChild>
          <Link href={`/listings/${params.id}`}>
            <ArrowLeft className="h-4 w-4" />
          </Link>
        </Button>
        <h1 className="text-lg font-semibold">Edit Listing</h1>
      </div>

      <form onSubmit={handleSubmit}>
        <div className="grid gap-4 lg:grid-cols-2">
          <Card>
            <CardHeader>
              <CardTitle className="text-sm">Basic Information</CardTitle>
            </CardHeader>
            <CardContent className="space-y-3">
              <div>
                <Label htmlFor="mls_number" className="text-xs">
                  MLS Number *
                </Label>
                <Input
                  id="mls_number"
                  value={formData.mls_number}
                  onChange={(e) => setFormData({ ...formData, mls_number: e.target.value })}
                  className="h-8 text-xs"
                  required
                />
              </div>

              <div>
                <Label htmlFor="status" className="text-xs">
                  Status
                </Label>
                <Select value={formData.status} onValueChange={(value) => setFormData({ ...formData, status: value })}>
                  <SelectTrigger className="h-8 text-xs">
                    <SelectValue />
                  </SelectTrigger>
                  <SelectContent>
                    <SelectItem value="Active">Active</SelectItem>
                    <SelectItem value="Pending">Pending</SelectItem>
                    <SelectItem value="Under Contract">Under Contract</SelectItem>
                    <SelectItem value="Sold">Sold</SelectItem>
                    <SelectItem value="Coming Soon">Coming Soon</SelectItem>
                  </SelectContent>
                </Select>
              </div>

              <div>
                <Label htmlFor="list_price" className="text-xs">
                  List Price
                </Label>
                <Input
                  id="list_price"
                  type="number"
                  value={formData.list_price}
                  onChange={(e) => setFormData({ ...formData, list_price: e.target.value })}
                  className="h-8 text-xs"
                  placeholder="0"
                />
              </div>

              <div>
                <Label htmlFor="builder_id" className="text-xs">
                  Builder
                </Label>
                <Select
                  value={formData.builder_id}
                  onValueChange={(value) => setFormData({ ...formData, builder_id: value })}
                >
                  <SelectTrigger className="h-8 text-xs">
                    <SelectValue placeholder="Select builder" />
                  </SelectTrigger>
                  <SelectContent>
                    <SelectItem value="no_builder">No builder</SelectItem>
                    {builders.map((builder) => (
                      <SelectItem key={builder.id} value={builder.id}>
                        {builder.name} {builder.company_name && `(${builder.company_name})`}
                      </SelectItem>
                    ))}
                  </SelectContent>
                </Select>
              </div>
            </CardContent>
          </Card>

          <Card>
            <CardHeader>
              <CardTitle className="text-sm">Address</CardTitle>
            </CardHeader>
            <CardContent className="space-y-3">
              <div className="grid grid-cols-2 gap-2">
                <div>
                  <Label htmlFor="street_number" className="text-xs">
                    Street Number
                  </Label>
                  <Input
                    id="street_number"
                    value={formData.street_number}
                    onChange={(e) => setFormData({ ...formData, street_number: e.target.value })}
                    className="h-8 text-xs"
                  />
                </div>
                <div>
                  <Label htmlFor="street_name" className="text-xs">
                    Street Name
                  </Label>
                  <Input
                    id="street_name"
                    value={formData.street_name}
                    onChange={(e) => setFormData({ ...formData, street_name: e.target.value })}
                    className="h-8 text-xs"
                  />
                </div>
              </div>

              <div>
                <Label htmlFor="city" className="text-xs">
                  City
                </Label>
                <Input
                  id="city"
                  value={formData.city}
                  onChange={(e) => setFormData({ ...formData, city: e.target.value })}
                  className="h-8 text-xs"
                />
              </div>

              <div className="grid grid-cols-2 gap-2">
                <div>
                  <Label htmlFor="state" className="text-xs">
                    State
                  </Label>
                  <Input
                    id="state"
                    value={formData.state}
                    onChange={(e) => setFormData({ ...formData, state: e.target.value })}
                    className="h-8 text-xs"
                    placeholder="VA"
                  />
                </div>
                <div>
                  <Label htmlFor="zip_code" className="text-xs">
                    Zip Code
                  </Label>
                  <Input
                    id="zip_code"
                    value={formData.zip_code}
                    onChange={(e) => setFormData({ ...formData, zip_code: e.target.value })}
                    className="h-8 text-xs"
                  />
                </div>
              </div>
            </CardContent>
          </Card>

          <Card>
            <CardHeader>
              <CardTitle className="text-sm">Property Details</CardTitle>
            </CardHeader>
            <CardContent className="space-y-3">
              <div className="grid grid-cols-3 gap-2">
                <div>
                  <Label htmlFor="bedrooms" className="text-xs">
                    Bedrooms
                  </Label>
                  <Input
                    id="bedrooms"
                    type="number"
                    value={formData.bedrooms}
                    onChange={(e) => setFormData({ ...formData, bedrooms: e.target.value })}
                    className="h-8 text-xs"
                  />
                </div>
                <div>
                  <Label htmlFor="baths_full" className="text-xs">
                    Full Baths
                  </Label>
                  <Input
                    id="baths_full"
                    type="number"
                    value={formData.baths_full}
                    onChange={(e) => setFormData({ ...formData, baths_full: e.target.value })}
                    className="h-8 text-xs"
                  />
                </div>
                <div>
                  <Label htmlFor="baths_half" className="text-xs">
                    Half Baths
                  </Label>
                  <Input
                    id="baths_half"
                    type="number"
                    value={formData.baths_half}
                    onChange={(e) => setFormData({ ...formData, baths_half: e.target.value })}
                    className="h-8 text-xs"
                  />
                </div>
              </div>

              <div>
                <Label htmlFor="interior_sqft" className="text-xs">
                  Square Feet
                </Label>
                <Input
                  id="interior_sqft"
                  type="number"
                  value={formData.interior_sqft}
                  onChange={(e) => setFormData({ ...formData, interior_sqft: e.target.value })}
                  className="h-8 text-xs"
                />
              </div>

              <div>
                <Label htmlFor="garage_spaces" className="text-xs">
                  Garage Spaces
                </Label>
                <Input
                  id="garage_spaces"
                  type="number"
                  value={formData.garage_spaces}
                  onChange={(e) => setFormData({ ...formData, garage_spaces: e.target.value })}
                  className="h-8 text-xs"
                />
              </div>
            </CardContent>
          </Card>

          <Card>
            <CardHeader>
              <CardTitle className="text-sm">Features</CardTitle>
            </CardHeader>
            <CardContent className="space-y-3">
              <div className="flex items-center space-x-2">
                <Checkbox
                  id="new_construction"
                  checked={formData.new_construction}
                  onCheckedChange={(checked) => setFormData({ ...formData, new_construction: !!checked })}
                />
                <Label htmlFor="new_construction" className="text-xs">
                  New Construction
                </Label>
              </div>

              <div className="flex items-center space-x-2">
                <Checkbox
                  id="fireplace"
                  checked={formData.fireplace}
                  onCheckedChange={(checked) => setFormData({ ...formData, fireplace: !!checked })}
                />
                <Label htmlFor="fireplace" className="text-xs">
                  Fireplace
                </Label>
              </div>

              <div className="flex items-center space-x-2">
                <Checkbox
                  id="central_air"
                  checked={formData.central_air}
                  onCheckedChange={(checked) => setFormData({ ...formData, central_air: !!checked })}
                />
                <Label htmlFor="central_air" className="text-xs">
                  Central Air
                </Label>
              </div>

              <div className="flex items-center space-x-2">
                <Checkbox
                  id="basement"
                  checked={formData.basement}
                  onCheckedChange={(checked) => setFormData({ ...formData, basement: !!checked })}
                />
                <Label htmlFor="basement" className="text-xs">
                  Basement
                </Label>
              </div>
            </CardContent>
          </Card>
        </div>

        <div className="flex justify-end gap-x-2 mt-4">
          <Button type="button" variant="outline" asChild>
            <Link href={`/listings/${params.id}`}>Cancel</Link>
          </Button>
          <Button type="submit" disabled={loading}>
            {loading ? (
              "Updating..."
            ) : (
              <>
                <Save className="mr-2 h-4 w-4" />
                Update Listing
              </>
            )}
          </Button>
        </div>
      </form>
    </div>
  )
}
```

## File: dkl-microapp-2-main/app/(dashboard)/listings/[id]/page.tsx
```typescript
"use client"

import { useEffect, useState } from "react"
import { useParams } from "next/navigation"
import { supabase } from "@/lib/supabase/client"
import { Card, CardContent, CardHeader, CardTitle } from "@/components/ui/card"
import { Button } from "@/components/ui/button"
import { Badge } from "@/components/ui/badge"
import { formatCurrency, formatDate, getFullAddress, getStatusColor } from "@/lib/utils"
import { ArrowLeft, Edit, Share2 } from "lucide-react"
import Link from "next/link"

export default function ListingDetailPage() {
  const params = useParams()
  const [listing, setListing] = useState<any>(null)
  const [loading, setLoading] = useState(true)

  useEffect(() => {
    if (params.id) {
      fetchListing()
    }
  }, [params.id])

  async function fetchListing() {
    try {
      const { data, error } = await supabase.from("listings").select("*, builders(*)").eq("id", params.id).single()

      if (error) throw error
      setListing(data)
    } catch (error) {
      console.error("Error fetching listing:", error)
    } finally {
      setLoading(false)
    }
  }

  if (loading) {
    return <div className="text-xs text-gray-600">Loading...</div>
  }

  if (!listing) {
    return <div className="text-xs text-gray-600">Listing not found</div>
  }

  return (
    <div className="space-y-4">
      <div className="flex items-center justify-between">
        <div className="flex items-center gap-x-2">
          <Button variant="ghost" size="sm" asChild>
            <Link href="/listings">
              <ArrowLeft className="h-4 w-4" />
            </Link>
          </Button>
          <div>
            <h1 className="text-lg font-semibold">{listing.mls_number}</h1>
            <p className="text-xs text-gray-600">{getFullAddress(listing)}</p>
          </div>
        </div>
        <div className="flex items-center gap-x-2">
          <Button size="sm" variant="outline" className="h-7 text-xs">
            <Share2 className="mr-1.5 h-3 w-3" />
            Add to Social
          </Button>
          <Button size="sm" className="h-7 text-xs" asChild>
            <Link href={`/listings/${params.id}/edit`}>
              <Edit className="mr-1.5 h-3 w-3" />
              Edit
            </Link>
          </Button>
        </div>
      </div>

      <div className="grid gap-4 lg:grid-cols-3">
        <div className="lg:col-span-2 space-y-4">
          <Card>
            <CardHeader>
              <CardTitle className="text-sm">Listing Details</CardTitle>
            </CardHeader>
            <CardContent className="space-y-3">
              <div className="grid grid-cols-2 gap-4 text-xs">
                <div>
                  <span className="text-gray-600">Status:</span>
                  <Badge
                    variant="secondary"
                    className={cn("ml-2 text-[10px] px-1.5 py-0", getStatusColor(listing.status))}
                  >
                    {listing.status}
                  </Badge>
                </div>
                <div>
                  <span className="text-gray-600">List Price:</span>
                  <span className="ml-2 font-medium">{formatCurrency(listing.list_price)}</span>
                </div>
                <div>
                  <span className="text-gray-600">Bedrooms:</span>
                  <span className="ml-2">{listing.bedrooms || "-"}</span>
                </div>
                <div>
                  <span className="text-gray-600">Bathrooms:</span>
                  <span className="ml-2">
                    {listing.baths_full || 0}
                    {listing.baths_half ? `.${listing.baths_half}` : ""}
                  </span>
                </div>
                <div>
                  <span className="text-gray-600">Square Feet:</span>
                  <span className="ml-2">{listing.interior_sqft?.toLocaleString() || "-"}</span>
                </div>
                <div>
                  <span className="text-gray-600">List Date:</span>
                  <span className="ml-2">{formatDate(listing.list_date)}</span>
                </div>
                <div>
                  <span className="text-gray-600">New Construction:</span>
                  <span className="ml-2">{listing.new_construction ? "Yes" : "No"}</span>
                </div>
                <div>
                  <span className="text-gray-600">Builder:</span>
                  <span className="ml-2">
                    {listing.builders ? (
                      <Link href={`/builders/${listing.builders.id}`} className="text-blue-600 hover:underline">
                        {listing.builders.name}
                      </Link>
                    ) : (
                      "-"
                    )}
                  </span>
                </div>
              </div>
            </CardContent>
          </Card>

          {listing.builders && (
            <Card>
              <CardHeader>
                <CardTitle className="text-sm">Builder Information</CardTitle>
              </CardHeader>
              <CardContent>
                <div className="text-xs">
                  <div className="font-medium">{listing.builders.name}</div>
                  <div className="text-gray-600">{listing.builders.company_name}</div>
                  {listing.builders.phone && <div className="text-gray-600">{listing.builders.phone}</div>}
                </div>
              </CardContent>
            </Card>
          )}
        </div>

        <div className="space-y-4">
          <Card>
            <CardHeader>
              <CardTitle className="text-sm">Financial Details</CardTitle>
            </CardHeader>
            <CardContent className="space-y-2 text-xs">
              <div className="flex justify-between">
                <span className="text-gray-600">Original Price:</span>
                <span>{formatCurrency(listing.original_price)}</span>
              </div>
              <div className="flex justify-between">
                <span className="text-gray-600">Current Price:</span>
                <span className="font-medium">{formatCurrency(listing.list_price)}</span>
              </div>
              <div className="flex justify-between">
                <span className="text-gray-600">Annual Taxes:</span>
                <span>{formatCurrency(listing.tax_annual_total)}</span>
              </div>
              {listing.association_fee && (
                <div className="flex justify-between">
                  <span className="text-gray-600">HOA Fee:</span>
                  <span>
                    {formatCurrency(listing.association_fee)} {listing.association_fee_frequency}
                  </span>
                </div>
              )}
            </CardContent>
          </Card>

          <Card>
            <CardHeader>
              <CardTitle className="text-sm">Property Features</CardTitle>
            </CardHeader>
            <CardContent className="space-y-2 text-xs">
              <div className="flex justify-between">
                <span className="text-gray-600">Garage Spaces:</span>
                <span>{listing.garage_spaces || "-"}</span>
              </div>
              <div className="flex justify-between">
                <span className="text-gray-600">Fireplace:</span>
                <span>{listing.fireplace ? "Yes" : "No"}</span>
              </div>
              <div className="flex justify-between">
                <span className="text-gray-600">Central Air:</span>
                <span>{listing.central_air ? "Yes" : "No"}</span>
              </div>
              <div className="flex justify-between">
                <span className="text-gray-600">Basement:</span>
                <span>{listing.basement ? "Yes" : "No"}</span>
              </div>
              {listing.property_condition && (
                <div className="flex justify-between">
                  <span className="text-gray-600">Condition:</span>
                  <span>{listing.property_condition}</span>
                </div>
              )}
            </CardContent>
          </Card>
        </div>
      </div>
    </div>
  )
}

function cn(...classes: string[]) {
  return classes.filter(Boolean).join(" ")
}
```

## File: dkl-microapp-2-main/app/(dashboard)/listings/page.tsx
```typescript
"use client"

import * as React from "react"
import { supabase } from "@/lib/supabase/client"
import { DataTable } from "@/components/ui/data-table"
import { Button } from "@/components/ui/button"
import { Checkbox } from "@/components/ui/checkbox"
import {
  DropdownMenu,
  DropdownMenuContent,
  DropdownMenuItem,
  DropdownMenuLabel,
  DropdownMenuSeparator,
  DropdownMenuTrigger,
} from "@/components/ui/dropdown-menu"
import { formatCurrency, formatDate, getFullAddress, getStatusColor } from "@/lib/utils"
import { MoreHorizontal, Plus, Download, Eye, Share2, EyeOff, Building2, Trash2, Edit } from "lucide-react" // Added Edit
import Link from "next/link"
import { Badge } from "@/components/ui/badge"
import { useToast } from "@/hooks/use-toast"
import { BuilderAssignmentDialog } from "@/components/builder-assignment-dialog"
import { ListingFormDialog } from "@/components/listing-form-dialog" // Import new dialog
import type { ColumnDef } from "@tanstack/react-table"
import { DataTableColumnHeader } from "@/components/ui/data-table-column-header"
import type { Database } from "@/types/supabase"

type Listing = Database["public"]["Tables"]["listings"]["Row"] & {
  builders: Pick<Database["public"]["Tables"]["builders"]["Row"], "id" | "name" | "company_name"> | null
}

export default function PropertiesPage() {
  const [properties, setProperties] = React.useState<Listing[]>([])
  const [loading, setLoading] = React.useState(true)
  const [showBuilderDialog, setShowBuilderDialog] = React.useState(false)
  const [selectedPropertyIdsForDialog, setSelectedPropertyIdsForDialog] = React.useState<string[]>([])
  const [isListingFormOpen, setIsListingFormOpen] = React.useState(false) // State for new dialog
  const [editingListing, setEditingListing] = React.useState<Partial<Listing> | undefined>(undefined) // State for editing

  const { toast } = useToast()

  const fetchProperties = React.useCallback(async () => {
    setLoading(true)
    try {
      const { data, error } = await supabase
        .from("listings")
        .select(
          `
      *,
      builders (
        id,
        name,
        company_name
      )
    `,
        )
        .order("list_date", { ascending: false })

      if (error) throw error
      setProperties((data as Listing[]) || [])
    } catch (error) {
      console.error("Error fetching listings:", error)
      toast({ title: "Error", description: "Could not fetch listings.", variant: "destructive" })
    } finally {
      setLoading(false)
    }
  }, [toast])

  React.useEffect(() => {
    fetchProperties()
  }, [fetchProperties])

  const handleOpenNewListingDialog = () => {
    setEditingListing(undefined)
    setIsListingFormOpen(true)
  }

  const handleOpenEditListingDialog = (listing: Listing) => {
    setEditingListing(listing)
    setIsListingFormOpen(true)
  }

  const handleBulkAction = async (action: string, selectedRows: Listing[]) => {
    const selectedIds = selectedRows.map((row) => row.id)
    if (selectedIds.length === 0) {
      toast({
        title: "No listings selected",
        description: "Please select listings to perform bulk actions.",
        variant: "destructive",
      })
      return
    }

    try {
      let successMessage = ""
      switch (action) {
        case "hide":
          await supabase
            .from("listings")
            .update({ metadata: { hidden: true } })
            .in("id", selectedIds)
          successMessage = `Hid ${selectedIds.length} listings.`
          break
        case "add_to_social":
          await supabase.from("listings").update({ in_social_queue: true }).in("id", selectedIds)
          successMessage = `Added ${selectedIds.length} listings to social queue.`
          break
        case "assign_builder":
          setSelectedPropertyIdsForDialog(selectedIds)
          setShowBuilderDialog(true)
          return // Dialog will handle toast & refresh
        case "delete":
          if (!confirm(`Are you sure you want to delete ${selectedIds.length} listings? This cannot be undone.`)) {
            return
          }
          const { error } = await supabase.from("listings").delete().in("id", selectedIds)
          if (error) throw error
          successMessage = `Deleted ${selectedIds.length} listings.`
          break
      }

      toast({
        title: "Bulk action completed",
        description: successMessage,
      })

      fetchProperties()
    } catch (error: any) {
      toast({
        title: "Error",
        description: error.message || "Failed to perform bulk action.",
        variant: "destructive",
      })
    }
  }

  const handleBuilderAssignmentComplete = () => {
    fetchProperties()
  }

  const exportToCSV = (selectedRows: Listing[]) => {
    const dataToExport = selectedRows.length > 0 ? selectedRows : properties
    if (dataToExport.length === 0) {
      toast({ title: "No data to export", variant: "destructive" })
      return
    }
    const csvContent = [
      [
        "MLS Number",
        "Status",
        "Address",
        "List Price",
        "Bedrooms",
        "Bathrooms",
        "Sq Ft",
        "New Construction",
        "Builder",
        "List Date",
      ].join(","),
      ...dataToExport.map((property) =>
        [
          `"${property.mls_number || ""}"`,
          `"${property.status || ""}"`,
          `"${getFullAddress(property)}"`,
          property.list_price || "",
          property.bedrooms || "",
          `${property.baths_full || 0}${property.baths_half ? `.${property.baths_half}` : ""}`,
          property.interior_sqft || "",
          property.new_construction ? "Yes" : "No",
          `"${property.builders?.name || ""}"`,
          `"${property.list_date || ""}"`,
        ].join(","),
      ),
    ].join("\n")

    const blob = new Blob([csvContent], { type: "text/csv;charset=utf-8;" })
    const url = window.URL.createObjectURL(blob)
    const a = document.createElement("a")
    a.href = url
    a.download = "listings_export.csv"
    a.click()
    window.URL.revokeObjectURL(url)
    toast({ title: "Export Started", description: `${dataToExport.length} listings are being exported.` })
  }

  const columns = React.useMemo<ColumnDef<Listing>[]>(
    () => [
      {
        id: "select",
        header: ({ table }) => (
          <Checkbox
            checked={table.getIsAllPageRowsSelected() || (table.getIsSomePageRowsSelected() && "indeterminate")}
            onCheckedChange={(value) => table.toggleAllPageRowsSelected(!!value)}
            aria-label="Select all"
            className="translate-y-[2px]"
          />
        ),
        cell: ({ row }) => (
          <Checkbox
            checked={row.getIsSelected()}
            onCheckedChange={(value) => row.toggleSelected(!!value)}
            aria-label="Select row"
            className="translate-y-[2px]"
          />
        ),
        enableSorting: false,
        enableHiding: false,
      },
      {
        accessorKey: "mls_number",
        header: ({ column }) => <DataTableColumnHeader column={column} title="MLS #" />,
        cell: ({ row }) => (
          <Link href={`/listings/${row.original.id}`} className="font-medium hover:underline text-primary">
            {row.getValue("mls_number") || "-"}
          </Link>
        ),
      },
      {
        accessorKey: "status",
        header: ({ column }) => <DataTableColumnHeader column={column} title="Status" />,
        cell: ({ row }) => {
          const status = row.getValue("status") as string
          return status ? (
            <Badge variant="secondary" className={cn("text-[10px] px-1.5 py-0", getStatusColor(status))}>
              {status}
            </Badge>
          ) : (
            "-"
          )
        },
        filterFn: (row, id, value) => value.includes(row.getValue(id)),
      },
      {
        accessorKey: "address",
        header: ({ column }) => <DataTableColumnHeader column={column} title="Address" />,
        cell: ({ row }) => (
          <Link href={`/listings/${row.original.id}`} className="max-w-xs truncate hover:underline">
            {getFullAddress(row.original)}
          </Link>
        ),
      },
      {
        accessorKey: "list_price",
        header: ({ column }) => <DataTableColumnHeader column={column} title="List Price" />,
        cell: ({ row }) => formatCurrency(row.getValue("list_price")),
      },
      {
        accessorKey: "bedrooms",
        header: ({ column }) => <DataTableColumnHeader column={column} title="Beds" />,
        cell: ({ row }) => row.getValue("bedrooms") || "-",
      },
      {
        accessorKey: "baths_full",
        header: ({ column }) => <DataTableColumnHeader column={column} title="Baths" />,
        cell: ({ row }) => {
          const full = (row.getValue("baths_full") as number) || 0
          const half = row.original.baths_half || 0
          return `${full}${half > 0 ? `.${half}` : ""}`
        },
      },
      {
        accessorKey: "interior_sqft",
        header: ({ column }) => <DataTableColumnHeader column={column} title="Sq Ft" />,
        cell: ({ row }) => {
          const sqft = row.getValue("interior_sqft") as number
          return sqft ? sqft.toLocaleString() : "-"
        },
      },
      {
        accessorKey: "new_construction",
        header: ({ column }) => <DataTableColumnHeader column={column} title="New" />,
        cell: ({ row }) =>
          row.getValue("new_construction") ? (
            <Badge variant="secondary" className="bg-green-100 text-green-800 text-[10px] px-1.5 py-0">
              NEW
            </Badge>
          ) : (
            "-"
          ),
        filterFn: (row, id, value) => value.includes(row.getValue(id)),
      },
      {
        accessorKey: "builders.name",
        header: ({ column }) => <DataTableColumnHeader column={column} title="Builder" />,
        cell: ({ row }) => {
          const builder = row.original.builders
          return builder ? (
            <Link href={`/builders/${builder.id}`} className="text-primary hover:underline text-xs">
              {builder.name}
            </Link>
          ) : (
            <span className="text-gray-400 text-xs">-</span>
          )
        },
      },
      {
        accessorKey: "list_date",
        header: ({ column }) => <DataTableColumnHeader column={column} title="Listed" />,
        cell: ({ row }) => formatDate(row.getValue("list_date")),
      },
      {
        id: "actions",
        cell: ({ row }) => {
          return (
            <DropdownMenu>
              <DropdownMenuTrigger asChild>
                <Button variant="ghost" className="h-7 w-7 p-0">
                  <span className="sr-only">Open menu</span>
                  <MoreHorizontal className="h-4 w-4" />
                </Button>
              </DropdownMenuTrigger>
              <DropdownMenuContent align="end" className="w-[160px]">
                <DropdownMenuLabel className="text-xs">Actions</DropdownMenuLabel>
                <DropdownMenuItem className="text-xs" asChild>
                  <Link href={`/listings/${row.original.id}`}>
                    <Eye className="mr-2 h-3.5 w-3.5" />
                    View details
                  </Link>
                </DropdownMenuItem>
                <DropdownMenuItem className="text-xs" onClick={() => handleOpenEditListingDialog(row.original)}>
                  <Edit className="mr-2 h-3.5 w-3.5" />
                  Edit Listing
                </DropdownMenuItem>
                <DropdownMenuItem className="text-xs" onClick={() => handleBulkAction("add_to_social", [row.original])}>
                  <Share2 className="mr-2 h-3.5 w-3.5" />
                  Add to Social Queue
                </DropdownMenuItem>
                <DropdownMenuSeparator />
                <DropdownMenuItem className="text-xs" onClick={() => handleBulkAction("hide", [row.original])}>
                  <EyeOff className="mr-2 h-3.5 w-3.5" />
                  Hide Listing
                </DropdownMenuItem>
                <DropdownMenuItem
                  className="text-xs text-red-600 focus:text-red-600 focus:bg-red-50"
                  onClick={() => handleBulkAction("delete", [row.original])}
                >
                  <Trash2 className="mr-2 h-3.5 w-3.5" />
                  Delete Listing
                </DropdownMenuItem>
              </DropdownMenuContent>
            </DropdownMenu>
          )
        },
      },
    ],
    [fetchProperties],
  )

  const renderPropertiesBulkActions = (selectedRows: Listing[]) => (
    <>
      <Button
        variant="outline"
        size="sm"
        className="h-7 text-xs"
        onClick={() => handleBulkAction("add_to_social", selectedRows)}
      >
        <Share2 className="mr-1.5 h-3 w-3" /> Add to Social
      </Button>
      <Button
        variant="outline"
        size="sm"
        className="h-7 text-xs"
        onClick={() => handleBulkAction("assign_builder", selectedRows)}
      >
        <Building2 className="mr-1.5 h-3 w-3" /> Assign Builder
      </Button>
      <Button
        variant="outline"
        size="sm"
        className="h-7 text-xs"
        onClick={() => handleBulkAction("hide", selectedRows)}
      >
        <EyeOff className="mr-1.5 h-3 w-3" /> Hide
      </Button>
      <Button
        variant="destructive"
        size="sm"
        className="h-7 text-xs"
        onClick={() => handleBulkAction("delete", selectedRows)}
      >
        <Trash2 className="mr-1.5 h-3 w-3" /> Delete
      </Button>
    </>
  )

  return (
    <div className="space-y-3">
      <div className="flex items-center justify-between">
        <div>
          <h1 className="text-lg font-semibold">Listings</h1>
          <p className="text-xs text-muted-foreground">Manage your listings.</p>
        </div>
        <div className="flex items-center gap-x-2">
          <Button size="sm" variant="outline" className="h-7 text-xs" onClick={() => exportToCSV([])}>
            <Download className="mr-1.5 h-3 w-3" />
            Export All
          </Button>
          <Button size="sm" className="h-7 text-xs" onClick={handleOpenNewListingDialog}>
            {" "}
            {/* Changed this line */}
            <Plus className="mr-1.5 h-3 w-3" />
            Add Listing
          </Button>
        </div>
      </div>

      <DataTable
        columns={columns}
        data={properties}
        loading={loading}
        renderBulkActions={renderPropertiesBulkActions}
        searchColumn="address" // Example: enable global search on address
      />

      <BuilderAssignmentDialog
        open={showBuilderDialog}
        onOpenChange={setShowBuilderDialog}
        selectedPropertyIds={selectedPropertyIdsForDialog}
        onAssignmentComplete={handleBuilderAssignmentComplete}
      />
      <ListingFormDialog // Add the new dialog component
        open={isListingFormOpen}
        onOpenChange={setIsListingFormOpen}
        onListingCreated={fetchProperties} // Refresh list on creation
        listing={editingListing}
      />
    </div>
  )
}

function cn(...classes: string[]) {
  return classes.filter(Boolean).join(" ")
}
```

## File: dkl-microapp-2-main/app/(dashboard)/reports/page.tsx
```typescript
"use client"

import { Card, CardContent, CardHeader, CardTitle } from "@/components/ui/card"
import { Button } from "@/components/ui/button"
import { FileText, Download, Calendar, BarChart3 } from "lucide-react"

export default function ReportsPage() {
  return (
    <div className="space-y-4">
      <div>
        <h1 className="text-lg font-semibold">Reports</h1>
        <p className="text-xs text-gray-600">Generate and download market reports</p>
      </div>

      <div className="grid gap-4 md:grid-cols-2 lg:grid-cols-3">
        <Card>
          <CardHeader className="pb-3">
            <CardTitle className="text-sm flex items-center gap-x-2">
              <FileText className="h-4 w-4" />
              Market Summary Report
            </CardTitle>
          </CardHeader>
          <CardContent>
            <p className="text-xs text-gray-600 mb-3">Comprehensive overview of market conditions and trends</p>
            <Button size="sm" className="h-7 text-xs w-full">
              <Download className="mr-1.5 h-3 w-3" />
              Generate Report
            </Button>
          </CardContent>
        </Card>

        <Card>
          <CardHeader className="pb-3">
            <CardTitle className="text-sm flex items-center gap-x-2">
              <BarChart3 className="h-4 w-4" />
              Builder Performance
            </CardTitle>
          </CardHeader>
          <CardContent>
            <p className="text-xs text-gray-600 mb-3">Analysis of builder activity and market share</p>
            <Button size="sm" className="h-7 text-xs w-full">
              <Download className="mr-1.5 h-3 w-3" />
              Generate Report
            </Button>
          </CardContent>
        </Card>

        <Card>
          <CardHeader className="pb-3">
            <CardTitle className="text-sm flex items-center gap-x-2">
              <Calendar className="h-4 w-4" />
              Monthly Activity
            </CardTitle>
          </CardHeader>
          <CardContent>
            <p className="text-xs text-gray-600 mb-3">Monthly breakdown of listings and sales activity</p>
            <Button size="sm" className="h-7 text-xs w-full">
              <Download className="mr-1.5 h-3 w-3" />
              Generate Report
            </Button>
          </CardContent>
        </Card>
      </div>
    </div>
  )
}
```

## File: dkl-microapp-2-main/app/(dashboard)/settings/page.tsx
```typescript
"use client"

import { AlertDialogTrigger } from "@/components/ui/alert-dialog" // Keep if used by other parts, otherwise can be removed if only for StyleGuide
import { DialogTrigger } from "@/components/ui/dialog" // Keep if used by other parts, otherwise can be removed if only for StyleGuide

import { useState, useEffect, useCallback } from "react"
import { useAuth } from "@/contexts/auth-context"
import { supabase } from "@/lib/supabase/client" // Used by multiple sub-components
import { Button } from "@/components/ui/button"
import { Card, CardContent, CardDescription, CardFooter, CardHeader, CardTitle } from "@/components/ui/card"
import { Input } from "@/components/ui/input"
import { Label } from "@/components/ui/label"
import { Tabs, TabsContent, TabsList, TabsTrigger } from "@/components/ui/tabs"
import { Switch } from "@/components/ui/switch"
import {
  Select as ShadSelect,
  SelectContent as ShadSelectContent,
  SelectItem as ShadSelectItem,
  SelectTrigger as ShadSelectTrigger,
  SelectValue as ShadSelectValue,
} from "@/components/ui/select"
import { Alert, AlertDescription, AlertTitle } from "@/components/ui/alert"
import { Separator } from "@/components/ui/separator"
import { useToast } from "@/hooks/use-toast" // Corrected path
import {
  AlertCircle,
  CheckCircle,
  Loader2,
  PaletteIcon,
  ChevronDown,
  ChevronsUpDown,
  Mail,
  Github,
  Italic,
  Check,
  DatabaseIcon,
  MapPin,
} from "lucide-react"
import type { Database } from "@/types/supabase"
import { hexToHsl } from "@/lib/color-utils"
import {
  Dialog, // Keep if used by other parts
  DialogContent as DialogContentForStyleGuide, // Alias to avoid conflict if Dialog is used elsewhere
  DialogDescription as DialogDescriptionForStyleGuide,
  DialogFooter as DialogFooterForStyleGuide,
  DialogHeader as DialogHeaderForStyleGuide,
  DialogTitle as DialogTitleForStyleGuide,
} from "@/components/ui/dialog"
import {
  AlertDialog, // Keep if used by other parts
  AlertDialogAction,
  AlertDialogCancel,
  AlertDialogContent as AlertDialogContentForStyleGuide, // Alias
  AlertDialogDescription as AlertDialogDescriptionForStyleGuide,
  AlertDialogFooter as AlertDialogFooterForStyleGuide,
  AlertDialogHeader as AlertDialogHeaderForStyleGuide,
  AlertDialogTitle as AlertDialogTitleForStyleGuide,
} from "@/components/ui/alert-dialog"
import { Popover, PopoverContent, PopoverTrigger } from "@/components/ui/popover"
import {
  DropdownMenu,
  DropdownMenuContent,
  DropdownMenuItem,
  DropdownMenuLabel,
  DropdownMenuSeparator,
  DropdownMenuTrigger,
  DropdownMenuSub,
  DropdownMenuSubContent,
  DropdownMenuSubTrigger,
  DropdownMenuPortal,
} from "@/components/ui/dropdown-menu"
import {
  Select as SelectForStyleGuide,
  SelectContent as SelectContentForStyleGuideSelect, // Further aliasing for clarity
  SelectItem as SelectItemForStyleGuideSelect,
  SelectTrigger as SelectTriggerForStyleGuideSelect,
  SelectValue as SelectValueForStyleGuideSelect,
} from "@/components/ui/select"
import { Command, CommandEmpty, CommandGroup, CommandInput, CommandItem, CommandList } from "@/components/ui/command"
import { Checkbox } from "@/components/ui/checkbox"
import { RadioGroup, RadioGroupItem } from "@/components/ui/radio-group"
import { Switch as SwitchForStyleGuide } from "@/components/ui/switch"
import { Toggle } from "@/components/ui/toggle"
import { cn, normalizeHeader } from "@/lib/utils"
import { Table, TableBody, TableCell, TableHead, TableHeader, TableRow } from "@/components/ui/table"

import { PillInput } from "@/components/pill-input"
import type { ListingFieldDefinition } from "@/lib/listing-fields"
import { builderTableColumns, type BuilderFieldDefinition } from "@/lib/builder-fields"
import { listingTableColumns } from "@/lib/listing-fields"

type UserSettings = Database["public"]["Tables"]["user_settings"]["Row"]
type UserFieldMappingInsert = Database["public"]["Tables"]["user_field_mappings"]["Insert"]

const DEFAULT_PRIMARY_HEX = "#0A0A0A"
const DEFAULT_PRIMARY_FOREGROUND_HEX = "#FAFAFA"

const PREDEFINED_ACCENTS = [
  { name: "Default", primary: DEFAULT_PRIMARY_HEX, foreground: DEFAULT_PRIMARY_FOREGROUND_HEX },
  { name: "Vercel Blue", primary: "#0070F3", foreground: "#FFFFFF" },
  { name: "Forest Green", primary: "#228B22", foreground: "#F0FFF0" },
  { name: "Sunset Orange", primary: "#FF4500", foreground: "#FFFFF0" },
  { name: "Royal Purple", primary: "#6A0DAD", foreground: "#F8F0FF" },
]

const GEOCODING_BATCH_SIZE = 10 // Define batch size for geocoding info

export default function SettingsPage() {
  return (
    <div className="space-y-6">
      <div>
        <h1 className="text-xl font-semibold">Settings</h1>
        <p className="text-sm text-muted-foreground">Manage your account, preferences, and application style</p>
      </div>

      <Tabs defaultValue="preferences" className="w-full">
        <TabsList className="grid w-full max-w-2xl grid-cols-6">
          <TabsTrigger value="preferences">Preferences</TabsTrigger>
          <TabsTrigger value="account">Account</TabsTrigger>
          <TabsTrigger value="notifications">Notifications</TabsTrigger>
          <TabsTrigger value="style-guide">Style Guide</TabsTrigger>
          <TabsTrigger value="integrations">Integrations</TabsTrigger>
          <TabsTrigger value="data-structure">Data Structure</TabsTrigger>
        </TabsList>
        <TabsContent value="preferences">
          <PreferencesSettings />
        </TabsContent>
        <TabsContent value="account">
          <AccountSettings />
        </TabsContent>
        <TabsContent value="notifications">
          <NotificationSettings />
        </TabsContent>
        <TabsContent value="style-guide">
          <StyleGuideSettingsTab />
        </TabsContent>
        <TabsContent value="integrations">
          <IntegrationsSettings />
        </TabsContent>
        <TabsContent value="data-structure">
          <DataStructureSettings />
        </TabsContent>
      </Tabs>
    </div>
  )
}

function PreferencesSettings() {
  const { user } = useAuth()
  const [settings, setSettings] = useState<Partial<UserSettings>>({
    theme: "light",
    default_view: "grid",
    items_per_page: 50,
  })
  const [isLoading, setIsLoading] = useState(true)
  const [isSaving, setIsSaving] = useState(false)
  const [success, setSuccess] = useState<string | null>(null)
  const [error, setError] = useState<string | null>(null)

  useEffect(() => {
    async function fetchSettings() {
      if (!user) {
        setIsLoading(false)
        return
      }
      setIsLoading(true)
      try {
        const { data, error: fetchError } = await supabase
          .from("user_settings")
          .select("theme, default_view, items_per_page")
          .eq("user_id", user.id)
          .single()

        if (fetchError && fetchError.code !== "PGRST116") {
          throw fetchError
        }
        if (data) {
          setSettings((prev) => ({ ...prev, ...data }))
        }
      } catch (err: any) {
        console.error("Error fetching user preferences:", err)
        setError(err.message || "Failed to load preferences.")
      } finally {
        setIsLoading(false)
      }
    }
    fetchSettings()
  }, [user])

  const handleSave = async () => {
    if (!user) return

    setIsSaving(true)
    setSuccess(null)
    setError(null)

    try {
      const { error: upsertError } = await supabase.from("user_settings").upsert(
        {
          user_id: user.id,
          theme: settings.theme,
          default_view: settings.default_view,
          items_per_page: settings.items_per_page,
        },
        { onConflict: "user_id" },
      )

      if (upsertError) throw upsertError

      setSuccess("Preferences saved successfully")
    } catch (err: any) {
      setError(err.message || "Failed to save preferences")
    } finally {
      setIsSaving(false)
    }
  }

  return (
    <Card>
      <CardHeader>
        <CardTitle className="text-base">Display Preferences</CardTitle>
        <CardDescription className="text-xs">Customize how the application looks and behaves</CardDescription>
      </CardHeader>
      <CardContent className="space-y-4">
        {success && (
          <Alert className="bg-green-50 text-green-800 border-green-200">
            <CheckCircle className="h-4 w-4 text-green-600" />
            <AlertTitle>Success</AlertTitle>
            <AlertDescription>{success}</AlertDescription>
          </Alert>
        )}
        {error && (
          <Alert variant="destructive">
            <AlertCircle className="h-4 w-4" />
            <AlertTitle>Error</AlertTitle>
            <AlertDescription>{error}</AlertDescription>
          </Alert>
        )}
        <div className="space-y-2">
          <Label htmlFor="theme">Theme</Label>
          <ShadSelect
            value={settings.theme || "light"}
            onValueChange={(value) => setSettings({ ...settings, theme: value })}
            disabled={isLoading}
          >
            <ShadSelectTrigger id="theme" className="attio-input">
              <ShadSelectValue placeholder="Select theme" />
            </ShadSelectTrigger>
            <ShadSelectContent>
              <ShadSelectItem value="light">Light</ShadSelectItem>
              <ShadSelectItem value="dark">Dark</ShadSelectItem>
              <ShadSelectItem value="system">System</ShadSelectItem>
            </ShadSelectContent>
          </ShadSelect>
        </div>
        <div className="space-y-2">
          <Label htmlFor="default-view">Default View</Label>
          <ShadSelect
            value={settings.default_view || "grid"}
            onValueChange={(value) => setSettings({ ...settings, default_view: value })}
            disabled={isLoading}
          >
            <ShadSelectTrigger id="default-view" className="attio-input">
              <ShadSelectValue placeholder="Select default view" />
            </ShadSelectTrigger>
            <ShadSelectContent>
              <ShadSelectItem value="grid">Grid</ShadSelectItem>
              <ShadSelectItem value="table">Table</ShadSelectItem>
              <ShadSelectItem value="kanban">Kanban</ShadSelectItem>
            </ShadSelectContent>
          </ShadSelect>
        </div>
        <div className="space-y-2">
          <Label htmlFor="items-per-page">Items Per Page</Label>
          <ShadSelect
            value={(settings.items_per_page || 50).toString()}
            onValueChange={(value) => setSettings({ ...settings, items_per_page: Number.parseInt(value) })}
            disabled={isLoading}
          >
            <ShadSelectTrigger id="items-per-page" className="attio-input">
              <ShadSelectValue placeholder="Select items per page" />
            </ShadSelectTrigger>
            <ShadSelectContent>
              <ShadSelectItem value="10">10</ShadSelectItem>
              <ShadSelectItem value="25">25</ShadSelectItem>
              <ShadSelectItem value="50">50</ShadSelectItem>
              <ShadSelectItem value="100">100</ShadSelectItem>
            </ShadSelectContent>
          </ShadSelect>
        </div>
      </CardContent>
      <CardFooter>
        <Button onClick={handleSave} disabled={isLoading || isSaving}>
          {isSaving ? <Loader2 className="mr-2 h-4 w-4 animate-spin" /> : "Save Preferences"}
        </Button>
      </CardFooter>
    </Card>
  )
}

function AccountSettings() {
  const { user } = useAuth()
  const [email, setEmail] = useState("")
  const [password, setPassword] = useState("")
  const [confirmPassword, setConfirmPassword] = useState("")
  const [isUpdating, setIsUpdating] = useState(false)
  const [success, setSuccess] = useState<string | null>(null)
  const [error, setError] = useState<string | null>(null)

  useEffect(() => {
    if (user) {
      setEmail(user.email || "")
    }
  }, [user])

  const handleUpdatePassword = async () => {
    if (!password || password !== confirmPassword) {
      setError("Passwords do not match or are empty.")
      return
    }
    if (password.length < 6) {
      setError("Password must be at least 6 characters long.")
      return
    }

    setIsUpdating(true)
    setSuccess(null)
    setError(null)

    try {
      const { error: updateError } = await supabase.auth.updateUser({ password })
      if (updateError) throw updateError

      setSuccess("Password updated successfully")
      setPassword("")
      setConfirmPassword("")
    } catch (err: any) {
      setError(err.message || "Failed to update password")
    } finally {
      setIsUpdating(false)
    }
  }

  return (
    <Card>
      <CardHeader>
        <CardTitle className="text-base">Account Settings</CardTitle>
        <CardDescription className="text-xs">Update your account information and password</CardDescription>
      </CardHeader>
      <CardContent className="space-y-4">
        {success && (
          <Alert className="bg-green-50 text-green-800 border-green-200">
            <CheckCircle className="h-4 w-4 text-green-600" />
            <AlertTitle>Success</AlertTitle>
            <AlertDescription>{success}</AlertDescription>
          </Alert>
        )}
        {error && (
          <Alert variant="destructive">
            <AlertCircle className="h-4 w-4" />
            <AlertTitle>Error</AlertTitle>
            <AlertDescription>{error}</AlertDescription>
          </Alert>
        )}
        <div className="space-y-2">
          <Label htmlFor="email">Email</Label>
          <Input id="email" value={email} disabled className="attio-input bg-muted" />
          <p className="text-xs text-muted-foreground">Your email address cannot be changed</p>
        </div>
        <div className="space-y-2">
          <Label htmlFor="password">New Password</Label>
          <Input
            id="password"
            type="password"
            value={password}
            onChange={(e) => setPassword(e.target.value)}
            className="attio-input"
          />
        </div>
        <div className="space-y-2">
          <Label htmlFor="confirm-password">Confirm New Password</Label>
          <Input
            id="confirm-password"
            type="password"
            value={confirmPassword}
            onChange={(e) => setConfirmPassword(e.target.value)}
            className="attio-input"
          />
        </div>
      </CardContent>
      <CardFooter>
        <Button onClick={handleUpdatePassword} disabled={!password || !confirmPassword || isUpdating}>
          {isUpdating ? <Loader2 className="mr-2 h-4 w-4 animate-spin" /> : "Update Password"}
        </Button>
      </CardFooter>
    </Card>
  )
}

function NotificationSettings() {
  const { user } = useAuth()
  const [settings, setSettings] = useState<Partial<UserSettings>>({
    notifications_enabled: true,
    email_notifications: true,
  })
  const [isLoading, setIsLoading] = useState(true)
  const [isSaving, setIsSaving] = useState(false)
  const [success, setSuccess] = useState<string | null>(null)
  const [error, setError] = useState<string | null>(null)

  useEffect(() => {
    async function fetchSettings() {
      if (!user) {
        setIsLoading(false)
        return
      }
      setIsLoading(true)
      try {
        const { data, error: fetchError } = await supabase
          .from("user_settings")
          .select("notifications_enabled, email_notifications")
          .eq("user_id", user.id)
          .single()

        if (fetchError && fetchError.code !== "PGRST116") {
          throw fetchError
        }
        if (data) {
          setSettings((prev) => ({ ...prev, ...data }))
        }
      } catch (err: any) {
        console.error("Error fetching notification settings:", err)
        setError(err.message || "Failed to load notification settings.")
      } finally {
        setIsLoading(false)
      }
    }
    fetchSettings()
  }, [user])

  const handleSave = async () => {
    if (!user) return

    setIsSaving(true)
    setSuccess(null)
    setError(null)

    try {
      const { error: upsertError } = await supabase.from("user_settings").upsert(
        {
          user_id: user.id,
          notifications_enabled: settings.notifications_enabled,
          email_notifications: settings.email_notifications,
        },
        { onConflict: "user_id" },
      )

      if (upsertError) throw upsertError

      setSuccess("Notification settings saved successfully")
    } catch (err: any) {
      setError(err.message || "Failed to save notification settings")
    } finally {
      setIsSaving(false)
    }
  }

  return (
    <Card>
      <CardHeader>
        <CardTitle className="text-base">Notification Settings</CardTitle>
        <CardDescription className="text-xs">Manage how and when you receive notifications</CardDescription>
      </CardHeader>
      <CardContent className="space-y-4">
        {success && (
          <Alert className="bg-green-50 text-green-800 border-green-200">
            <CheckCircle className="h-4 w-4 text-green-600" />
            <AlertTitle>Success</AlertTitle>
            <AlertDescription>{success}</AlertDescription>
          </Alert>
        )}
        {error && (
          <Alert variant="destructive">
            <AlertCircle className="h-4 w-4" />
            <AlertTitle>Error</AlertTitle>
            <AlertDescription>{error}</AlertDescription>
          </Alert>
        )}
        <div className="flex items-center justify-between">
          <div className="space-y-0.5">
            <Label htmlFor="notifications-enabled">Enable Notifications</Label>
            <p className="text-xs text-muted-foreground">Receive notifications about important updates</p>
          </div>
          <Switch
            id="notifications-enabled"
            checked={settings.notifications_enabled === true}
            onCheckedChange={(checked) => setSettings({ ...settings, notifications_enabled: checked })}
            disabled={isLoading}
          />
        </div>
        <div className="flex items-center justify-between">
          <div className="space-y-0.5">
            <Label htmlFor="email-notifications">Email Notifications</Label>
            <p className="text-xs text-muted-foreground">Receive notifications via email</p>
          </div>
          <Switch
            id="email-notifications"
            checked={settings.email_notifications === true}
            onCheckedChange={(checked) => setSettings({ ...settings, email_notifications: checked })}
            disabled={isLoading || settings.notifications_enabled === false}
          />
        </div>
      </CardContent>
      <CardFooter>
        <Button onClick={handleSave} disabled={isLoading || isSaving}>
          {isSaving ? <Loader2 className="mr-2 h-4 w-4 animate-spin" /> : "Save Notification Settings"}
        </Button>
      </CardFooter>
    </Card>
  )
}

function StyleGuideSettingsTab() {
  const { user } = useAuth()
  const { toast } = useToast()
  const [primaryHex, setPrimaryHex] = useState(DEFAULT_PRIMARY_HEX)
  const [primaryForegroundHex, setPrimaryForegroundHex] = useState(DEFAULT_PRIMARY_FOREGROUND_HEX)
  const [isLoading, setIsLoading] = useState(true)
  const [isSaving, setIsSaving] = useState(false)
  const [successMessage, setSuccessMessage] = useState<string | null>(null)
  const [errorMessage, setErrorMessage] = useState<string | null>(null)

  const frameworks = [
    { value: "next.js", label: "Next.js" },
    { value: "sveltekit", label: "SvelteKit" },
    { value: "nuxt.js", label: "Nuxt.js" },
    { value: "remix", label: "Remix" },
    { value: "astro", label: "Astro" },
  ]
  const [comboboxOpen, setComboboxOpen] = useState(false)
  const [comboboxValue, setComboboxValue] = useState("")

  const applyColorsToDocument = useCallback((primaryHslColor: string, foregroundHslColor: string) => {
    if (typeof document !== "undefined") {
      document.documentElement.style.setProperty("--primary", primaryHslColor)
      document.documentElement.style.setProperty("--primary-foreground", foregroundHslColor)
    }
  }, [])

  useEffect(() => {
    async function fetchStyleSettings() {
      if (!user) {
        setIsLoading(false)
        const defaultPrimaryHsl = hexToHsl(DEFAULT_PRIMARY_HEX)
        const defaultFgHsl = hexToHsl(DEFAULT_PRIMARY_FOREGROUND_HEX)
        if (defaultPrimaryHsl && defaultFgHsl) {
          applyColorsToDocument(defaultPrimaryHsl, defaultFgHsl)
        }
        return
      }
      setIsLoading(true)
      try {
        const { data, error } = await supabase
          .from("user_settings")
          .select("primary_color_hex, primary_foreground_color_hex")
          .eq("user_id", user.id)
          .single()

        if (error && error.code !== "PGRST116") throw error

        const currentPrimaryHex = data?.primary_color_hex || DEFAULT_PRIMARY_HEX
        const currentFgHex = data?.primary_foreground_color_hex || DEFAULT_PRIMARY_FOREGROUND_HEX

        setPrimaryHex(currentPrimaryHex)
        setPrimaryForegroundHex(currentFgHex)

        const primaryHsl = hexToHsl(currentPrimaryHex)
        const fgHsl = hexToHsl(currentFgHex)
        const defaultPrimaryHsl = hexToHsl(DEFAULT_PRIMARY_HEX)
        const defaultFgHsl = hexToHsl(DEFAULT_PRIMARY_FOREGROUND_HEX)

        if (primaryHsl && fgHsl && defaultPrimaryHsl && defaultFgHsl) {
          applyColorsToDocument(primaryHsl, fgHsl)
        } else if (defaultPrimaryHsl && defaultFgHsl) {
          applyColorsToDocument(defaultPrimaryHsl, defaultFgHsl)
        }
      } catch (err: any) {
        console.error("Error fetching style settings:", err)
        setErrorMessage("Failed to load style settings.")
        const defaultPrimaryHsl = hexToHsl(DEFAULT_PRIMARY_HEX)
        const defaultFgHsl = hexToHsl(DEFAULT_PRIMARY_FOREGROUND_HEX)
        if (defaultPrimaryHsl && defaultFgHsl) {
          applyColorsToDocument(defaultPrimaryHsl, defaultFgHsl)
        }
      } finally {
        setIsLoading(false)
      }
    }
    fetchStyleSettings()
  }, [user, applyColorsToDocument, supabase])

  useEffect(() => {
    const primaryHslValue = hexToHsl(primaryHex)
    const foregroundHslValue = hexToHsl(primaryForegroundHex)
    if (primaryHslValue && foregroundHslValue) {
      applyColorsToDocument(primaryHslValue, foregroundHslValue)
    }
  }, [primaryHex, primaryForegroundHex, applyColorsToDocument])

  const handleSaveAccentColor = async () => {
    if (!user) {
      setErrorMessage("You must be logged in to save settings.")
      return
    }
    setIsSaving(true)
    setSuccessMessage(null)
    setErrorMessage(null)

    if (!hexToHsl(primaryHex) || !hexToHsl(primaryForegroundHex)) {
      setErrorMessage("Invalid HEX color format. Please use #RRGGBB or #RGB.")
      toast({ title: "Invalid HEX", description: "Please check your color codes.", variant: "destructive" })
      setIsSaving(false)
      return
    }

    try {
      const { error } = await supabase.from("user_settings").upsert(
        {
          user_id: user.id,
          primary_color_hex: primaryHex,
          primary_foreground_color_hex: primaryForegroundHex,
        },
        { onConflict: "user_id" },
      )

      if (error) throw error

      setSuccessMessage("Accent color saved successfully! It will be applied globally on next page load or refresh.")
      toast({
        title: "Accent Color Saved",
        description: "Your new accent color has been saved.",
      })
    } catch (err: any) {
      console.error("Error saving accent color:", err)
      setErrorMessage((err as Error).message || "Failed to save accent color.")
      toast({
        title: "Error",
        description: "Failed to save accent color.",
        variant: "destructive",
      })
    } finally {
      setIsSaving(false)
    }
  }

  const handlePresetChange = (primaryHexString: string, foregroundHexString: string) => {
    setPrimaryHex(primaryHexString)
    setPrimaryForegroundHex(foregroundHexString)
  }

  if (isLoading) {
    return (
      <div className="flex h-64 items-center justify-center">
        <Loader2 className="h-8 w-8 animate-spin text-primary" />
      </div>
    )
  }

  return (
    <div className="space-y-6">
      {successMessage && (
        <Alert className="border-green-500 bg-green-50 text-green-700">
          <CheckCircle className="h-4 w-4 !text-green-700" />
          <AlertTitle>Success</AlertTitle>
          <AlertDescription>{successMessage}</AlertDescription>
        </Alert>
      )}
      {errorMessage && (
        <Alert variant="destructive">
          <AlertCircle className="h-4 w-4" />
          <AlertTitle>Error</AlertTitle>
          <AlertDescription>{errorMessage}</AlertDescription>
        </Alert>
      )}
      <Card>
        <CardHeader>
          <CardTitle className="text-base flex items-center">
            <PaletteIcon className="mr-2 h-5 w-5" /> Accent Color Customization
          </CardTitle>
          <CardDescription className="text-xs">
            Customize the primary accent color. Changes are previewed live on this page. Global application requires a
            page refresh after saving.
          </CardDescription>
        </CardHeader>
        <CardContent className="space-y-6">
          <div className="grid grid-cols-1 gap-4 md:grid-cols-2">
            <div className="space-y-2">
              <Label htmlFor="primaryHex">Primary Color HEX</Label>
              <Input
                id="primaryHex"
                value={primaryHex}
                onChange={(e) => setPrimaryHex(e.target.value)}
                placeholder="e.g., #0A0A0A"
                className="attio-input"
              />
            </div>
            <div className="space-y-2">
              <Label htmlFor="primaryForegroundHex">Primary Foreground HEX</Label>
              <Input
                id="primaryForegroundHex"
                value={primaryForegroundHex}
                onChange={(e) => setPrimaryForegroundHex(e.target.value)}
                placeholder="e.g., #FAFAFA"
                className="attio-input"
              />
            </div>
          </div>
          <div className="space-y-2">
            <Label>Predefined Accents</Label>
            <div className="flex flex-wrap gap-2">
              {PREDEFINED_ACCENTS.map((preset) => (
                <Button
                  key={preset.name}
                  variant="outline"
                  size="sm"
                  onClick={() => handlePresetChange(preset.primary, preset.foreground)}
                  className="flex items-center gap-2"
                >
                  <span style={{ backgroundColor: preset.primary }} className="h-4 w-4 rounded-full border" />
                  {preset.name}
                </Button>
              ))}
            </div>
          </div>
        </CardContent>
        <CardFooter>
          <Button onClick={handleSaveAccentColor} disabled={isSaving}>
            {isSaving && <Loader2 className="mr-2 h-4 w-4 animate-spin" />}
            Save Accent Color
          </Button>
        </CardFooter>
      </Card>

      <Separator />

      <section className="space-y-8">
        <h3 className="text-xl font-semibold">Component Previews</h3>
        <Card>
          <CardHeader>
            <CardTitle className="text-base">Typography</CardTitle>
          </CardHeader>
          <CardContent className="space-y-2">
            <h1 className="text-4xl font-bold">Heading 1</h1>
            <h2 className="text-3xl font-semibold">Heading 2</h2>
            <h3 className="text-2xl font-medium">Heading 3</h3>
            <h4 className="text-xl">Heading 4</h4>
            <p>
              This is a paragraph. Links look like{" "}
              <a href="#" className="font-medium text-primary underline underline-offset-4">
                this
              </a>
              . <strong>Bold text</strong>.
            </p>
            <blockquote className="mt-6 border-l-2 pl-6 italic">Blockquote example.</blockquote>
          </CardContent>
        </Card>
        <Card>
          <CardHeader>
            <CardTitle className="text-base">Buttons</CardTitle>
          </CardHeader>
          <CardContent className="flex flex-wrap gap-2">
            <Button>Primary</Button>
            <Button variant="secondary">Secondary</Button>
            <Button variant="destructive">Destructive</Button>
            <Button variant="outline">Outline</Button>
            <Button variant="ghost">Ghost</Button>
            <Button variant="link">Link</Button>
            <Button>
              <Mail className="mr-2 h-4 w-4" /> With Icon
            </Button>
            <Button variant="outline" size="icon">
              <Github className="h-4 w-4" />
            </Button>
          </CardContent>
        </Card>
        <Card>
          <CardHeader>
            <CardTitle className="text-base">Cards</CardTitle>
          </CardHeader>
          <CardContent>
            <Card className="w-full max-w-sm">
              <CardHeader>
                <CardTitle>Card Title</CardTitle>
                <CardDescription>This is a card description.</CardDescription>
              </CardHeader>
              <CardContent>
                <p>Card content goes here. You can put any elements inside.</p>
              </CardContent>
              <CardFooter className="flex justify-between">
                <Button variant="outline">Cancel</Button>
                <Button>Deploy</Button>
              </CardFooter>
            </Card>
          </CardContent>
        </Card>
        <Card>
          <CardHeader>
            <CardTitle className="text-base">Inputs & Selects</CardTitle>
          </CardHeader>
          <CardContent className="space-y-4 max-w-xs">
            <Input placeholder="Standard Input" className="attio-input" />
            <Input type="email" placeholder="Email Input" className="attio-input" />
            <SelectForStyleGuide>
              <SelectTriggerForStyleGuideSelect className="attio-input">
                <SelectValueForStyleGuideSelect placeholder="Select an option" />
              </SelectTriggerForStyleGuideSelect>
              <SelectContentForStyleGuideSelect>
                <SelectItemForStyleGuideSelect value="1">Option 1</SelectItemForStyleGuideSelect>
                <SelectItemForStyleGuideSelect value="2">Option 2</SelectItemForStyleGuideSelect>
              </SelectContentForStyleGuideSelect>
            </SelectForStyleGuide>
          </CardContent>
        </Card>
        <Card>
          <CardHeader>
            <CardTitle className="text-base">Table</CardTitle>
          </CardHeader>
          <CardContent>
            <Table>
              <TableHeader>
                <TableRow>
                  <TableHead className="w-[100px]">Invoice</TableHead>
                  <TableHead>Status</TableHead>
                  <TableHead>Method</TableHead>
                  <TableHead className="text-right">Amount</TableHead>
                </TableRow>
              </TableHeader>
              <TableBody>
                <TableRow>
                  <TableCell className="font-medium">INV001</TableCell>
                  <TableCell>Paid</TableCell>
                  <TableCell>Credit Card</TableCell>
                  <TableCell className="text-right">$250.00</TableCell>
                </TableRow>
                <TableRow>
                  <TableCell className="font-medium">INV002</TableCell>
                  <TableCell>Pending</TableCell>
                  <TableCell>PayPal</TableCell>
                  <TableCell className="text-right">$150.00</TableCell>
                </TableRow>
              </TableBody>
            </Table>
          </CardContent>
        </Card>
        <Card>
          <CardHeader>
            <CardTitle className="text-base">Modals & Dialogs</CardTitle>
          </CardHeader>
          <CardContent className="flex gap-2">
            <Dialog>
              <DialogTrigger asChild>
                <Button variant="outline">Open Dialog</Button>
              </DialogTrigger>
              <DialogContentForStyleGuide>
                <DialogHeaderForStyleGuide>
                  <DialogTitleForStyleGuide>Dialog Title</DialogTitleForStyleGuide>
                  <DialogDescriptionForStyleGuide>This is a dialog.</DialogDescriptionForStyleGuide>
                </DialogHeaderForStyleGuide>
                <DialogFooterForStyleGuide>
                  <Button>OK</Button>
                </DialogFooterForStyleGuide>
              </DialogContentForStyleGuide>
            </Dialog>
            <AlertDialog>
              <AlertDialogTrigger asChild>
                <Button variant="destructive">Open Alert Dialog</Button>
              </AlertDialogTrigger>
              <AlertDialogContentForStyleGuide>
                <AlertDialogHeaderForStyleGuide>
                  <AlertDialogTitleForStyleGuide>Alert!</AlertDialogTitleForStyleGuide>
                  <AlertDialogDescriptionForStyleGuide>This is an alert dialog.</AlertDialogDescriptionForStyleGuide>
                </AlertDialogHeaderForStyleGuide>
                <AlertDialogFooterForStyleGuide>
                  <AlertDialogCancel>Cancel</AlertDialogCancel>
                  <AlertDialogAction>Continue</AlertDialogAction>
                </AlertDialogFooterForStyleGuide>
              </AlertDialogContentForStyleGuide>
            </AlertDialog>
          </CardContent>
        </Card>
        <Card>
          <CardHeader>
            <CardTitle className="text-base">Popovers</CardTitle>
          </CardHeader>
          <CardContent>
            <Popover>
              <PopoverTrigger asChild>
                <Button variant="outline">Open Popover</Button>
              </PopoverTrigger>
              <PopoverContent className="w-80">
                <p>Popover content goes here. Useful for small bits of information or actions.</p>
              </PopoverContent>
            </Popover>
          </CardContent>
        </Card>
        <Card>
          <CardHeader>
            <CardTitle className="text-base">Toast Notifications</CardTitle>
          </CardHeader>
          <CardContent className="space-x-2">
            <Button
              variant="outline"
              onClick={() => toast({ title: "Event Scheduled", description: "Friday, February 10, 2023 at 5:57 PM" })}
            >
              Show Toast
            </Button>
            <Button
              variant="outline"
              onClick={() =>
                toast({
                  title: "Uh oh! Something went wrong.",
                  description: "There was a problem with your request.",
                  variant: "destructive",
                })
              }
            >
              Show Destructive Toast
            </Button>
          </CardContent>
        </Card>
        <Card>
          <CardHeader>
            <CardTitle className="text-base">Dropdown Menus</CardTitle>
          </CardHeader>
          <CardContent>
            <DropdownMenu>
              <DropdownMenuTrigger asChild>
                <Button variant="outline">
                  Open Menu <ChevronDown className="ml-2 h-4 w-4" />
                </Button>
              </DropdownMenuTrigger>
              <DropdownMenuContent>
                <DropdownMenuLabel>My Account</DropdownMenuLabel>
                <DropdownMenuSeparator />
                <DropdownMenuItem>Profile</DropdownMenuItem>
                <DropdownMenuItem>Billing</DropdownMenuItem>
                <DropdownMenuSub>
                  <DropdownMenuSubTrigger>
                    <span>Invite users</span>
                  </DropdownMenuSubTrigger>
                  <DropdownMenuPortal>
                    <DropdownMenuSubContent>
                      <DropdownMenuItem>
                        <span>Email</span>
                      </DropdownMenuItem>
                      <DropdownMenuItem>
                        <span>Message</span>
                      </DropdownMenuItem>
                    </DropdownMenuSubContent>
                  </DropdownMenuPortal>
                </DropdownMenuSub>
                <DropdownMenuItem>Log out</DropdownMenuItem>
              </DropdownMenuContent>
            </DropdownMenu>
          </CardContent>
        </Card>
        <Card>
          <CardHeader>
            <CardTitle className="text-base">Combobox</CardTitle>
          </CardHeader>
          <CardContent>
            <Popover open={comboboxOpen} onOpenChange={setComboboxOpen}>
              <PopoverTrigger asChild>
                <Button
                  variant="outline"
                  role="combobox"
                  aria-expanded={comboboxOpen}
                  className="w-[200px] justify-between"
                >
                  {comboboxValue
                    ? frameworks.find((framework) => framework.value === comboboxValue)?.label
                    : "Select framework..."}
                  <ChevronsUpDown className="ml-2 h-4 w-4 shrink-0 opacity-50" />
                </Button>
              </PopoverTrigger>
              <PopoverContent className="w-[200px] p-0">
                <Command>
                  <CommandInput placeholder="Search framework..." />
                  <CommandList>
                    <CommandEmpty>No framework found.</CommandEmpty>
                    <CommandGroup>
                      {frameworks.map((framework) => (
                        <CommandItem
                          key={framework.value}
                          value={framework.value}
                          onSelect={(currentValue) => {
                            setComboboxValue(currentValue === comboboxValue ? "" : currentValue)
                            setComboboxOpen(false)
                          }}
                        >
                          <Check
                            className={cn(
                              "mr-2 h-4 w-4",
                              comboboxValue === framework.value ? "opacity-100" : "opacity-0",
                            )}
                          />
                          {framework.label}
                        </CommandItem>
                      ))}
                    </CommandGroup>
                  </CommandList>
                </Command>
              </PopoverContent>
            </Popover>
          </CardContent>
        </Card>
        <Card>
          <CardHeader>
            <CardTitle className="text-base">Checkboxes & Radio Group</CardTitle>
          </CardHeader>
          <CardContent className="space-y-2">
            <div className="flex items-center space-x-2">
              <Checkbox id="terms-style" /> <Label htmlFor="terms-style">Accept terms</Label>
            </div>
            <RadioGroup defaultValue="comfortable-style">
              <div className="flex items-center space-x-2">
                <RadioGroupItem value="default-style" id="r1-style" /> <Label htmlFor="r1-style">Default</Label>
              </div>
              <div className="flex items-center space-x-2">
                <RadioGroupItem value="comfortable-style" id="r2-style" /> <Label htmlFor="r2-style">Comfortable</Label>
              </div>
            </RadioGroup>
          </CardContent>
        </Card>
        <Card>
          <CardHeader>
            <CardTitle className="text-base">Switches & Toggles</CardTitle>
          </CardHeader>
          <CardContent className="space-y-2">
            <div className="flex items-center space-x-2">
              <SwitchForStyleGuide id="airplane-mode-style" />{" "}
              <Label htmlFor="airplane-mode-style">Airplane Mode</Label>
            </div>
            <Toggle aria-label="Toggle italic">
              <Italic className="h-4 w-4" />
            </Toggle>
          </CardContent>
        </Card>
      </section>
    </div>
  )
}

function IntegrationsSettings() {
  const { user } = useAuth()
  const { toast } = useToast()
  const [openaiApiKey, setOpenaiApiKey] = useState("")
  const [openaiModel, setOpenaiModel] = useState("gpt-3.5-turbo")
  const [mapboxApiKey, setMapboxApiKey] = useState("")
  const [isLoading, setIsLoading] = useState(true)
  const [isSavingOpenAI, setIsSavingOpenAI] = useState(false)
  const [isSavingMapbox, setIsSavingMapbox] = useState(false)
  const [geocodingLoading, setGeocodingLoading] = useState(false)
  const [geocodingMessage, setGeocodingMessage] = useState<string | null>(null)

  const availableModels = [
    { value: "gpt-4o", label: "GPT-4o (Latest)" },
    { value: "gpt-4-turbo", label: "GPT-4 Turbo" },
    { value: "gpt-3.5-turbo", label: "GPT-3.5 Turbo" },
  ]

  useEffect(() => {
    async function fetchIntegrationSettings() {
      if (!user) {
        setIsLoading(false)
        return
      }
      setIsLoading(true)
      try {
        const { data, error: fetchError } = await supabase
          .from("user_settings")
          .select("openai_api_key, openai_model, mapbox_api_key")
          .eq("user_id", user.id)
          .single()

        if (fetchError && fetchError.code !== "PGRST116") {
          throw fetchError
        }
        if (data) {
          setOpenaiApiKey(data.openai_api_key || "")
          setOpenaiModel(data.openai_model || "gpt-3.5-turbo")
          setMapboxApiKey(data.mapbox_api_key || "")
        }
      } catch (err: any) {
        console.error("Error fetching integration settings:", err)
        toast({ title: "Error", description: "Failed to load integration settings.", variant: "destructive" })
      } finally {
        setIsLoading(false)
      }
    }
    fetchIntegrationSettings()
  }, [user, toast, supabase])

  const handleSaveOpenAISettings = async () => {
    if (!user) return

    setIsSavingOpenAI(true)
    try {
      const { error: upsertError } = await supabase.from("user_settings").upsert(
        {
          user_id: user.id,
          openai_api_key: openaiApiKey,
          openai_model: openaiModel,
        },
        { onConflict: "user_id" },
      )

      if (upsertError) throw upsertError

      toast({ title: "Success", description: "OpenAI settings saved successfully." })
    } catch (err: any) {
      toast({
        title: "Error",
        description: (err as Error).message || "Failed to save OpenAI settings.",
        variant: "destructive",
      })
    } finally {
      setIsSavingOpenAI(false)
    }
  }

  const handleSaveMapboxSettings = async () => {
    if (!user) return

    setIsSavingMapbox(true)
    try {
      const { error: upsertError } = await supabase.from("user_settings").upsert(
        {
          user_id: user.id,
          mapbox_api_key: mapboxApiKey,
        },
        { onConflict: "user_id" },
      )

      if (upsertError) throw upsertError

      toast({ title: "Success", description: "Mapbox settings saved successfully." })
    } catch (err: any) {
      toast({
        title: "Error",
        description: (err as Error).message || "Failed to save Mapbox settings.",
        variant: "destructive",
      })
    } finally {
      setIsSavingMapbox(false)
    }
  }

  const handleGeocodeProperties = async () => {
    setGeocodingLoading(true)
    setGeocodingMessage("Starting geocoding process...")

    if (!user) {
      toast({ title: "Authentication Error", description: "You must be logged in.", variant: "destructive" })
      setGeocodingLoading(false)
      return
    }

    let totalGeocoded = 0
    let totalFailed = 0
    let batchNumber = 1
    let shouldContinue = true

    while (shouldContinue) {
      try {
        setGeocodingMessage(
          `Processing batch ${batchNumber}... Total geocoded so far: ${totalGeocoded}, Failed: ${totalFailed}`,
        )

        const {
          data: { session },
        } = await supabase.auth.getSession()
        if (!session) throw new Error("User session not found. Please log in again.")

        const supabaseUrl = process.env.NEXT_PUBLIC_SUPABASE_URL
        const supabaseAnonKey = process.env.NEXT_PUBLIC_SUPABASE_ANON_KEY
        if (!supabaseUrl || !supabaseAnonKey) throw new Error("Supabase URL or Anon Key is not configured.")

        console.log("Making request to:", `${supabaseUrl}/functions/v1/geocode-properties`)

        const response = await fetch(`${supabaseUrl}/functions/v1/geocode-properties`, {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
            Authorization: `Bearer ${session.access_token}`,
            apikey: supabaseAnonKey,
          },
        })

        console.log("Response status:", response.status)
        console.log("Response headers:", Object.fromEntries(response.headers.entries()))

        const result = await response.json()
        console.log("Response body:", result)

        if (!response.ok) {
          throw new Error(result.error || result.message || `HTTP ${response.status}: ${response.statusText}`)
        }

        // Handle both string responses and object responses from the Edge Function
        let geocodedInBatch = 0
        let failedInBatch = 0
        let propertiesFound = 0

        if (typeof result === "string") {
          // Parse the string response to extract numbers - fix the regex patterns
          const processedMatch = result.match(/Processed:\s*(\d+)/)
          const geocodedMatch = result.match(/Geocoded:\s*(\d+)/)
          const failedMatch = result.match(/Failed:\s*(\d+)/)

          propertiesFound = processedMatch ? Number.parseInt(processedMatch[1], 10) : 0
          geocodedInBatch = geocodedMatch ? Number.parseInt(geocodedMatch[1], 10) : 0
          failedInBatch = failedMatch ? Number.parseInt(failedMatch[1], 10) : 0

          // Debug logging to verify parsing
          console.log("String parsing results:", {
            originalString: result,
            processedMatch,
            geocodedMatch,
            failedMatch,
            propertiesFound,
            geocodedInBatch,
            failedInBatch,
          })
        } else {
          // Handle object response format
          geocodedInBatch = result.geocodedCount || 0
          failedInBatch = result.failedCount || 0
          propertiesFound = result.propertiesFound || result.processedCount || 0
        }

        totalGeocoded += geocodedInBatch
        totalFailed += failedInBatch

        console.log(`Batch ${batchNumber} results:`, {
          geocodedInBatch,
          failedInBatch,
          propertiesFound,
          totalGeocoded,
          totalFailed,
        })

        // If the function found 0 properties, it means there are no more to process.
        // But if it found properties and geocoded them, we should continue to the next batch.
        if (propertiesFound === 0) {
          if (batchNumber === 1) {
            setGeocodingMessage(
              "No properties found that need geocoding. All properties may already have coordinates or are missing required address fields.",
            )
          }
          shouldContinue = false
        } else if (geocodedInBatch === 0 && propertiesFound > 0) {
          // If we found properties but couldn't geocode any of them, stop to avoid an infinite loop
          setGeocodingMessage(
            "Found properties without coordinates, but couldn't geocode any of them. Check address data quality.",
          )
          shouldContinue = false
        } else {
          batchNumber++
          // Add a small delay between batches to avoid rate limiting
          await new Promise((resolve) => setTimeout(resolve, 1000))
        }
      } catch (error: any) {
        console.error("Geocoding error:", error)
        const errorMessage = error.message || "An unknown error occurred."
        setGeocodingMessage(`Error: ${errorMessage}. Stopping process.`)
        toast({
          title: "Geocoding Error",
          description: errorMessage,
          variant: "destructive",
        })
        shouldContinue = false // Stop the loop on any error
      }
    }

    const finalMessage = `Geocoding complete. Total newly geocoded: ${totalGeocoded}. Total failed: ${totalFailed}.`
    setGeocodingMessage(finalMessage)
    toast({
      title: "Geocoding Process Finished",
      description: finalMessage,
    })
    setGeocodingLoading(false)
  }

  return (
    <div className="space-y-6">
      <Card>
        <CardHeader>
          <CardTitle className="text-base">AI Integrations</CardTitle>
          <CardDescription className="text-xs">Configure your OpenAI API for AI-powered features.</CardDescription>
        </CardHeader>
        <CardContent className="space-y-4">
          {isLoading ? (
            <div className="flex justify-center items-center h-24">
              <Loader2 className="h-6 w-6 animate-spin" />
            </div>
          ) : (
            <>
              <div className="space-y-2">
                <Label htmlFor="openai-api-key">OpenAI API Key</Label>
                <Input
                  id="openai-api-key"
                  type="password"
                  value={openaiApiKey}
                  onChange={(e) => setOpenaiApiKey(e.target.value)}
                  placeholder="sk-xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
                  className="attio-input"
                />
                <p className="text-xs text-muted-foreground">
                  Your API key is stored securely and only used for AI features within this application.
                </p>
              </div>
              <div className="space-y-2">
                <Label htmlFor="openai-model">OpenAI Model</Label>
                <ShadSelect value={openaiModel} onValueChange={setOpenaiModel}>
                  <ShadSelectTrigger id="openai-model" className="attio-input">
                    <ShadSelectValue placeholder="Select AI model" />
                  </ShadSelectTrigger>
                  <ShadSelectContent>
                    {availableModels.map((model) => (
                      <ShadSelectItem key={model.value} value={model.value}>
                        {model.label}
                      </ShadSelectItem>
                    ))}
                  </ShadSelectContent>
                </ShadSelect>
              </div>
            </>
          )}
        </CardContent>
        <CardFooter>
          <Button onClick={handleSaveOpenAISettings} disabled={isLoading || isSavingOpenAI}>
            {isSavingOpenAI ? <Loader2 className="mr-2 h-4 w-4 animate-spin" /> : "Save OpenAI Settings"}
          </Button>
        </CardFooter>
      </Card>

      <Card>
        <CardHeader>
          <CardTitle className="text-base flex items-center">
            <MapPin className="mr-2 h-5 w-5" /> Mapbox Integration
          </CardTitle>
          <CardDescription className="text-xs">
            Configure your Mapbox Access Token for map features. This token is stored in your user settings and used
            client-side.
          </CardDescription>
        </CardHeader>
        <CardContent className="space-y-4">
          {isLoading ? (
            <div className="flex justify-center items-center h-16">
              <Loader2 className="h-6 w-6 animate-spin" />
            </div>
          ) : (
            <div className="space-y-2">
              <Label htmlFor="mapbox-api-key">Mapbox Access Token (Client-side)</Label>
              <Input
                id="mapbox-api-key"
                type="password"
                value={mapboxApiKey}
                onChange={(e) => setMapboxApiKey(e.target.value)}
                placeholder="pk.xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
                className="attio-input"
              />
              <p className="text-xs text-muted-foreground">
                Your Mapbox Access Token for displaying maps. For server-side geocoding, a separate token is configured
                in your Edge Function settings.
              </p>
            </div>
          )}
        </CardContent>
        <CardFooter>
          <Button onClick={handleSaveMapboxSettings} disabled={isLoading || isSavingMapbox}>
            {isSavingMapbox ? <Loader2 className="mr-2 h-4 w-4 animate-spin" /> : "Save Mapbox Token"}
          </Button>
        </CardFooter>
      </Card>

      <Card>
        <CardHeader>
          <CardTitle className="text-base flex items-center">
            <DatabaseIcon className="mr-2 h-5 w-5" /> Data Management
          </CardTitle>
          <CardDescription className="text-xs">Tools for managing and enhancing your property data.</CardDescription>
        </CardHeader>
        <CardContent className="space-y-4">
          <div className="space-y-2">
            <Label htmlFor="geocode-properties">Server-Side Geocoding</Label>
            <p className="text-xs text-muted-foreground">
              Run a process to find all properties missing coordinates and geocode them. This will run continuously in
              batches until all properties are processed.
            </p>
            <Button onClick={handleGeocodeProperties} disabled={geocodingLoading || isLoading}>
              {geocodingLoading ? (
                <Loader2 className="mr-2 h-4 w-4 animate-spin" />
              ) : (
                <DatabaseIcon className="mr-2 h-4 w-4" />
              )}
              {geocodingLoading ? "Geocoding in Progress..." : "Start Full Geocoding Process"}
            </Button>
            {geocodingMessage && (
              <Alert
                className={`mt-2 text-xs ${
                  geocodingMessage.toLowerCase().startsWith("error:")
                    ? "border-red-500 text-red-700"
                    : "border-blue-500 text-blue-700"
                }`}
              >
                <AlertCircle className="h-4 w-4" />
                <AlertTitle>
                  {geocodingLoading
                    ? "Process Update"
                    : geocodingMessage.toLowerCase().startsWith("error:")
                      ? "Process Error"
                      : "Process Complete"}
                </AlertTitle>
                <AlertDescription>{geocodingMessage}</AlertDescription>
              </Alert>
            )}
          </div>
        </CardContent>
      </Card>
    </div>
  )
}

function DataStructureSettings() {
  const { user } = useAuth()
  const { toast } = useToast()
  const [selectedTable, setSelectedTable] = useState<"listings" | "builders">("listings")
  const [isLoading, setIsLoading] = useState(false)
  const [dbColumns, setDbColumns] = useState<(ListingFieldDefinition | BuilderFieldDefinition)[]>([])
  const [fieldMappings, setFieldMappings] = useState<Record<string, string[]>>({}) // dbColumnValue -> csvHeader[]

  useEffect(() => {
    if (selectedTable === "listings") {
      setDbColumns(listingTableColumns)
    } else {
      setDbColumns(builderTableColumns)
    }
    setFieldMappings({}) // Reset mappings when table changes
  }, [selectedTable])

  useEffect(() => {
    if (!user || dbColumns.length === 0) {
      if (dbColumns.length > 0) {
        setFieldMappings(
          dbColumns.reduce(
            (acc, col) => {
              acc[col.value] = []
              return acc
            },
            {} as Record<string, string[]>,
          ),
        )
      }
      return
    }

    async function fetchMappings() {
      setIsLoading(true)
      try {
        const { data, error } = await supabase
          .from("user_field_mappings")
          .select("target_database_column, source_csv_header")
          .eq("user_id", user!.id)
          .eq("target_table_name", selectedTable)

        if (error) throw error

        const newMappings: Record<string, string[]> = {}
        dbColumns.forEach((col) => (newMappings[col.value] = []))

        data?.forEach((mapping) => {
          if (newMappings[mapping.target_database_column]) {
            newMappings[mapping.target_database_column].push(mapping.source_csv_header)
          } else {
            newMappings[mapping.target_database_column] = [mapping.source_csv_header]
          }
        })
        setFieldMappings(newMappings)
      } catch (err: any) {
        toast({ title: "Error", description: `Failed to load field mappings: ${err.message}`, variant: "destructive" })
        setFieldMappings(
          dbColumns.reduce(
            (acc, col) => {
              acc[col.value] = []
              return acc
            },
            {} as Record<string, string[]>,
          ),
        )
      } finally {
        setIsLoading(false)
      }
    }
    fetchMappings()
  }, [user, selectedTable, dbColumns, toast, supabase])

  const handleMappingChange = async (dbColumnValue: string, newCsvHeaders: string[]) => {
    if (!user) return

    const oldCsvHeaders = fieldMappings[dbColumnValue] || []
    const normalizedNewCsvHeaders = newCsvHeaders.map(normalizeHeader).filter(Boolean) // Normalize and remove empty strings

    // Optimistically update UI with normalized headers
    setFieldMappings((prev) => ({ ...prev, [dbColumnValue]: normalizedNewCsvHeaders }))

    const added = normalizedNewCsvHeaders.filter((h) => !oldCsvHeaders.includes(h))
    const removed = oldCsvHeaders.filter((h) => !normalizedNewCsvHeaders.includes(h))

    try {
      // Handle added headers
      for (const normalizedCsv of added) {
        const { data: existingConflict, error: checkError } = await supabase
          .from("user_field_mappings")
          .select("id, target_database_column")
          .eq("user_id", user.id)
          .eq("target_table_name", selectedTable)
          .eq("source_csv_header", normalizedCsv)
          .neq("target_database_column", dbColumnValue) // Check if mapped to a *different* column
          .single()

        if (checkError && checkError.code !== "PGRST116") throw checkError

        if (existingConflict) {
          toast({
            title: "Mapping Conflict",
            description: `CSV header "${normalizedCsv}" is already mapped to "${existingConflict.target_database_column}". Please remove it from the other mapping first or use a different CSV header. Reverting changes for this field.`,
            variant: "destructive",
          })
          setFieldMappings((prev) => ({ ...prev, [dbColumnValue]: oldCsvHeaders })) // Revert
          return // Stop processing this field's changes
        }

        const { error: insertError } = await supabase.from("user_field_mappings").upsert(
          {
            user_id: user.id,
            target_table_name: selectedTable,
            target_database_column: dbColumnValue,
            source_csv_header: normalizedCsv,
          } as UserFieldMappingInsert,
          { onConflict: "user_id,target_table_name,source_csv_header" },
        )
        if (insertError) throw insertError
      }

      // Handle removed headers
      for (const csvHeaderToRemove of removed) {
        const { error: deleteError } = await supabase
          .from("user_field_mappings")
          .delete()
          .eq("user_id", user.id)
          .eq("target_table_name", selectedTable)
          .eq("target_database_column", dbColumnValue)
          .eq("source_csv_header", csvHeaderToRemove)
        if (deleteError) throw deleteError
      }

      if (added.length > 0 || removed.length > 0) {
        toast({ title: "Mappings Updated", description: `Mappings for ${dbColumnValue} saved.` })
      }
    } catch (err: any) {
      toast({ title: "Error", description: `Failed to update mappings: ${err.message}`, variant: "destructive" })
      setFieldMappings((prev) => ({ ...prev, [dbColumnValue]: oldCsvHeaders })) // Revert on error
    }
  }

  return (
    <Card>
      <CardHeader>
        <CardTitle className="text-base flex items-center">
          <DatabaseIcon className="mr-2 h-5 w-5" /> Custom Field Mappings
        </CardTitle>
        <CardDescription className="text-xs">
          Define default CSV headers that should map to your database columns for faster imports. These mappings are
          specific to your user account. Enter the exact CSV header text you expect.
        </CardDescription>
      </CardHeader>
      <CardContent className="space-y-6">
        <div className="space-y-2 max-w-sm">
          <Label htmlFor="table-select">Select Table</Label>
          <ShadSelect
            value={selectedTable}
            onValueChange={(value) => setSelectedTable(value as "listings" | "builders")}
          >
            <ShadSelectTrigger id="table-select" className="attio-input">
              <ShadSelectValue placeholder="Select a table" />
            </ShadSelectTrigger>
            <ShadSelectContent>
              <ShadSelectItem value="listings">Listings</ShadSelectItem>
              <ShadSelectItem value="builders">Builders</ShadSelectItem>
            </ShadSelectContent>
          </ShadSelect>
        </div>

        {isLoading && (
          <div className="flex items-center justify-center py-8">
            <Loader2 className="h-8 w-8 animate-spin text-primary" />
            <p className="ml-2">Loading mappings...</p>
          </div>
        )}

        {!isLoading && dbColumns.length > 0 && (
          <div className="space-y-4 max-h-[60vh] overflow-y-auto pr-2">
            {dbColumns.map((col) => (
              <div key={col.value} className="p-4 border rounded-md bg-muted/20">
                <Label htmlFor={`map-${col.value}`} className="font-semibold text-sm block mb-1">
                  {col.label} <span className="text-xs text-muted-foreground">({col.value})</span>
                </Label>
                <PillInput
                  value={fieldMappings[col.value] || []}
                  onChange={(newPills) => handleMappingChange(col.value, newPills)}
                  placeholder="Enter CSV header and press Enter..."
                  className="mt-1"
                />
                <p className="text-xs text-muted-foreground mt-1">
                  Enter the exact CSV header(s) that should map to this field. Headers are case-insensitive and spaces
                  are replaced with underscores.
                </p>
              </div>
            ))}
          </div>
        )}
        {!isLoading && dbColumns.length === 0 && selectedTable && (
          <p className="text-sm text-muted-foreground">No columns defined for the '{selectedTable}' table.</p>
        )}
      </CardContent>
      <CardFooter>
        <p className="text-xs text-muted-foreground">
          Changes are saved automatically. CSV headers are stored in a normalized format (uppercase, underscores).
        </p>
      </CardFooter>
    </Card>
  )
}
```

## File: dkl-microapp-2-main/app/(dashboard)/social/[postId]/page.tsx
```typescript
"use client"

import { cn } from "@/lib/utils"

import { useParams } from "next/navigation"
import { useEffect, useState, useCallback } from "react"
import { supabase } from "@/lib/supabase/client"
import type { Database } from "@/types/supabase" // Ensure this path is correct
import { Button } from "@/components/ui/button"
import { Badge } from "@/components/ui/badge"
import { toast } from "@/hooks/use-toast"
import Link from "next/link"
import { ArrowLeft, Loader2, ImageIcon } from "lucide-react"
import { EditableField } from "@/components/editable-field"
import { SocialPostPropertyItem } from "@/components/social-post-property-item"
import { SelectContent, SelectItem } from "@/components/ui/select"

type SocialPostFromDB = Database["public"]["Tables"]["social_posts"]["Row"]
type SocialPostPropertyFromDB = Database["public"]["Tables"]["social_post_properties"]["Row"]
type ListingFromDB = Database["public"]["Tables"]["listings"]["Row"]

interface SocialPostProperty extends SocialPostPropertyFromDB {
  properties: ListingFromDB | null
}

interface FullSocialPost extends SocialPostFromDB {
  social_post_properties: SocialPostProperty[]
  content_type: string | null // Added
  format_type: string | null // Added
}

export default function SocialPostDetailPage() {
  const params = useParams()
  const postId = params.postId as string
  const [post, setPost] = useState<FullSocialPost | null>(null)
  const [loading, setLoading] = useState(true)

  const fetchPostDetails = useCallback(async () => {
    if (!postId) {
      setLoading(false) // Stop loading if no postId
      return
    }
    setLoading(true)
    const { data, error } = await supabase
      .from("social_posts")
      .select(
        `
        *,
        social_post_properties (
          *,
          properties (
            id, mls_number, list_price, city, state, zip_code, street_number, street_direction, street_name, unit_number, status
          )
        )
      `,
      )
      .eq("id", postId)
      .single()

    if (error) {
      console.error("Error fetching post details:", error)
      toast({ title: "Error", description: "Failed to load post details. " + error.message, variant: "destructive" })
      setPost(null)
    } else {
      setPost(data as FullSocialPost)
    }
    setLoading(false)
  }, [postId])

  useEffect(() => {
    fetchPostDetails()
  }, [fetchPostDetails])

  const handleUpdatePostField = async (
    field: "title" | "description" | "content_type" | "format_type",
    value: string,
  ) => {
    if (!post) return
    const oldPost = { ...post }
    setPost((prev) => (prev ? { ...prev, [field]: value } : null))

    try {
      const { error } = await supabase
        .from("social_posts")
        .update({ [field]: value })
        .eq("id", post.id)
      if (error) throw error
      toast({ title: "Post Updated", description: `Post ${field} has been successfully updated.` })
    } catch (error: any) {
      toast({
        title: "Update Failed",
        description: `Failed to update post ${field}: ${error.message}`,
        variant: "destructive",
      })
      setPost(oldPost)
    }
  }

  const handlePropertyItemUpdate = (updatedPropertyItem: Partial<SocialPostProperty>) => {
    setPost((prevPost) => {
      if (!prevPost) return null
      return {
        ...prevPost,
        social_post_properties: prevPost.social_post_properties.map((p) =>
          p.id === updatedPropertyItem.id ? { ...p, ...updatedPropertyItem } : p,
        ),
      }
    })
  }

  const getStatusBadgeVariant = (status?: string | null): "default" | "secondary" | "outline" | "destructive" => {
    switch (status?.toLowerCase()) {
      case "posted":
        return "default"
      case "complete":
        return "secondary"
      case "draft":
        return "outline"
      default:
        return "outline"
    }
  }

  if (loading) {
    return (
      <div className="flex items-center justify-center min-h-screen bg-gray-100 dark:bg-gray-950">
        <Loader2 className="h-10 w-10 animate-spin text-blueishGreen-500" />
      </div>
    )
  }

  if (!post) {
    return (
      <div className="p-6 text-center min-h-screen flex flex-col items-center justify-center bg-gray-100 dark:bg-gray-950">
        <p className="text-xl text-muted-foreground mb-4">Post Not Found</p>
        <p className="text-sm text-muted-foreground mb-4">
          It might have been deleted or there was an issue loading it.
        </p>
        <Button variant="outline" asChild className="bg-white dark:bg-gray-800">
          <Link href="/social">
            <ArrowLeft className="mr-2 h-4 w-4" />
            Back to Social Posts
          </Link>
        </Button>
      </div>
    )
  }

  return (
    <div className="flex flex-col md:flex-row min-h-screen overflow-hidden bg-gray-100 dark:bg-gray-950">
      <main className="flex-1 p-4 md:p-6 space-y-4 overflow-y-auto">
        <div className="flex items-center justify-between mb-3">
          <Button
            variant="outline"
            size="sm"
            asChild
            className="bg-white dark:bg-gray-800 hover:bg-gray-50 dark:hover:bg-gray-700"
          >
            <Link href="/social">
              <ArrowLeft className="mr-2 h-4 w-4" />
              Back to Posts
            </Link>
          </Button>
        </div>

        <h2 className="text-sm font-medium uppercase text-gray-500 dark:text-gray-400 tracking-wider mb-3">
          Listings ({post.social_post_properties?.length || 0})
        </h2>

        {post.social_post_properties && post.social_post_properties.length > 0 ? (
          <div className="space-y-3">
            {post.social_post_properties.map((spp) => (
              <SocialPostPropertyItem key={spp.id} item={spp} postId={post.id} onUpdate={handlePropertyItemUpdate} />
            ))}
          </div>
        ) : (
          <div className="text-center py-12 border-2 border-dashed border-gray-200 dark:border-gray-700 rounded-lg bg-white dark:bg-gray-800/30">
            <ImageIcon className="mx-auto h-12 w-12 text-gray-300 dark:text-gray-600" />
            <p className="mt-2 text-sm text-muted-foreground">No listings associated with this post.</p>
            <p className="text-xs text-muted-foreground mt-1">You can add listings from the main Social Posts page.</p>
          </div>
        )}
      </main>

      <aside className="w-full md:w-[360px] lg:w-[400px] bg-white dark:bg-gray-900 border-l border-gray-200 dark:border-gray-700 p-4 md:p-6 space-y-5 overflow-y-auto">
        <div className="pb-4 border-b border-gray-200 dark:border-gray-700">
          <label className="text-xs font-medium text-gray-500 dark:text-gray-400 block mb-0.5">Post Title</label>
          <EditableField
            initialValue={post.title}
            onSave={(newTitle) => handleUpdatePostField("title", newTitle)}
            label="Post Title"
            inputClassName="text-lg font-semibold !h-9"
            textClassName="text-lg font-semibold py-1"
            placeholder="Enter post title"
          />
        </div>

        <div className="pb-4 border-b border-gray-200 dark:border-gray-700">
          <label className="text-xs font-medium text-gray-500 dark:text-gray-400 block mb-0.5">Description</label>
          <EditableField
            initialValue={post.description || ""}
            onSave={(newDesc) => handleUpdatePostField("description", newDesc)}
            label="Post Description"
            as="textarea"
            inputClassName="min-h-[100px] text-sm"
            textClassName="py-1 leading-relaxed text-sm min-h-[40px]" // min-h for text view
            placeholder="Add a description..."
          />
        </div>

        <div className="pb-4 border-b border-gray-200 dark:border-gray-700">
          <label className="text-xs font-medium text-gray-500 dark:text-gray-400 block mb-0.5">Content Type</label>
          <EditableField
            initialValue={post.content_type || ""}
            onSave={(newContentType) => handleUpdatePostField("content_type", newContentType)}
            label="Content Type"
            as="select"
            inputClassName="!h-9"
            textClassName="py-1 text-sm"
            placeholder="Select content type"
          >
            <SelectContent>
              <SelectItem value="Single Property">Single Property</SelectItem>
              <SelectItem value="Multi Property">Multi Property</SelectItem>
            </SelectContent>
          </EditableField>
        </div>

        <div className="pb-4 border-b border-gray-200 dark:border-gray-700">
          <label className="text-xs font-medium text-gray-500 dark:text-gray-400 block mb-0.5">Format Type</label>
          <EditableField
            initialValue={post.format_type || ""}
            onSave={(newFormatType) => handleUpdatePostField("format_type", newFormatType)}
            label="Format Type"
            as="select"
            inputClassName="!h-9"
            textClassName="py-1 text-sm"
            placeholder="Select format type"
          >
            <SelectContent>
              <SelectItem value="Carousel">Carousel</SelectItem>
              <SelectItem value="Post">Post</SelectItem>
              <SelectItem value="Reel">Reel</SelectItem>
              <SelectItem value="Story">Story</SelectItem>
            </SelectContent>
          </EditableField>
        </div>

        <div className="space-y-3 text-sm pt-1">
          <div>
            <p className="text-xs font-medium text-gray-500 dark:text-gray-400">Status</p>
            <Badge
              variant={getStatusBadgeVariant(post.status)}
              className={cn(
                "text-xs capitalize px-2.5 py-0.5",
                getStatusBadgeVariant(post.status) === "default" &&
                  "bg-blueishGreen-500 hover:bg-blueishGreen-600 text-blueishGreen-foreground",
              )}
            >
              {post.status || "Unknown"}
            </Badge>
          </div>
          <div>
            <p className="text-xs font-medium text-gray-500 dark:text-gray-400">Created</p>
            <p className="text-gray-700 dark:text-gray-300">{new Date(post.created_at).toLocaleDateString()}</p>
          </div>
          {post.post_url && (
            <div>
              <p className="text-xs font-medium text-gray-500 dark:text-gray-400">Post URL</p>
              <a
                href={post.post_url}
                target="_blank"
                rel="noopener noreferrer"
                className="text-blueishGreen-600 hover:text-blueishGreen-500 hover:underline break-all dark:text-blueishGreen-400 dark:hover:text-blueishGreen-300"
              >
                {post.post_url}
              </a>
            </div>
          )}
        </div>
      </aside>
    </div>
  )
}
```

## File: dkl-microapp-2-main/app/(dashboard)/social/loading.tsx
```typescript
import { Loader2 } from "lucide-react"

export default function Loading() {
  return (
    <div className="flex h-full items-center justify-center">
      <Loader2 className="h-6 w-6 animate-spin text-gray-400" />
    </div>
  )
}
```

## File: dkl-microapp-2-main/app/(dashboard)/social/page.tsx
```typescript
"use client"

import React from "react"
import { supabase } from "@/lib/supabase/client"
import { useAuth } from "@/contexts/auth-context"
import { Button } from "@/components/ui/button"
import {
  Dialog,
  DialogContent,
  DialogDescription,
  DialogFooter,
  DialogHeader,
  DialogTitle,
  DialogTrigger,
} from "@/components/ui/dialog"
import { Input } from "@/components/ui/input"
import { Label } from "@/components/ui/label"
import { Progress } from "@/components/ui/progress"
import { Checkbox } from "@/components/ui/checkbox"
import { useToast } from "@/hooks/use-toast"
import { DataTable } from "@/components/ui/data-table"
import { DataTableColumnHeader } from "@/components/ui/data-table-column-header"
import {
  PlusCircle,
  ChevronDown,
  ChevronRight,
  Edit3,
  Trash2,
  Loader2,
  AlertCircle,
  ExternalLink,
  MoreHorizontal,
  PackagePlus,
  CheckCircle2,
  XCircle,
  ListPlus,
} from "lucide-react"
import Link from "next/link"
import { Alert, AlertDescription, AlertTitle } from "@/components/ui/alert"
import type { Database } from "@/types/supabase"
import type { ColumnDef, Row } from "@tanstack/react-table"
import {
  DropdownMenu,
  DropdownMenuContent,
  DropdownMenuItem,
  DropdownMenuLabel,
  DropdownMenuSeparator,
  DropdownMenuTrigger,
} from "@/components/ui/dropdown-menu"
import { Badge } from "@/components/ui/badge"
import { Select, SelectContent, SelectItem, SelectTrigger, SelectValue } from "@/components/ui/select"

type ListingRow = Database["public"]["Tables"]["listings"]["Row"]
type SocialPostRow = Database["public"]["Tables"]["social_posts"]["Row"]
type SocialPostPropertyJunctionRow = Database["public"]["Tables"]["social_post_properties"]["Row"]

interface EnrichedSocialPostPropertyForMainTable extends SocialPostPropertyJunctionRow {
  properties: Partial<ListingRow> | null
}
interface EnrichedSocialPost extends SocialPostRow {
  social_post_properties: EnrichedSocialPostPropertyForMainTable[]
  content_type: string | null
  format_type: string | null
}

interface AllLinkedPropertyItem extends SocialPostPropertyJunctionRow {
  properties: Pick<
    ListingRow,
    | "id"
    | "mls_number"
    | "street_number"
    | "street_direction"
    | "street_name"
    | "unit_number"
    | "city"
    | "state"
    | "zip_code"
  > | null
  social_posts: Pick<SocialPostRow, "id" | "title"> | null
}

const getFullAddress = (
  property:
    | Partial<ListingRow>
    | Pick<
        ListingRow,
        | "id"
        | "mls_number"
        | "street_number"
        | "street_direction"
        | "street_name"
        | "unit_number"
        | "city"
        | "state"
        | "zip_code"
      >
    | null,
): string => {
  if (!property) return "N/A"
  return (
    `${property.street_number || ""} ${property.street_direction || ""} ${property.street_name || ""}${property.unit_number ? ` #${property.unit_number}` : ""}, ${property.city || ""}, ${property.state || ""} ${
      property.zip_code || ""
    }`
      .replace(/\s,/g, ",")
      .replace(/, $/, "")
      .replace(/^,/, "")
      .trim() || "Address not available"
  )
}

const formatCurrency = (amount: number | null | undefined) => {
  if (amount == null) return "N/A"
  return new Intl.NumberFormat("en-US", { style: "currency", currency: "USD", minimumFractionDigits: 0 }).format(amount)
}

export default function SocialPostsPage() {
  const { user } = useAuth()
  const { toast } = useToast()
  const [socialPosts, setSocialPosts] = React.useState<EnrichedSocialPost[]>([])
  const [allLinkedProperties, setAllLinkedProperties] = React.useState<AllLinkedPropertyItem[]>([])
  const [propertiesAvailableForQueue, setPropertiesAvailableForQueue] = React.useState<ListingRow[]>([])

  const [isLoadingPosts, setIsLoadingPosts] = React.useState(true)
  const [isLoadingLinkedItems, setIsLoadingLinkedItems] = React.useState(true)
  const [isLoadingAvailableProps, setIsLoadingAvailableProps] = React.useState(true)
  const [error, setError] = React.useState<string | null>(null)

  const [isCreatePostDialogOpen, setIsCreatePostDialogOpen] = React.useState(false)
  const [newPostName, setNewPostName] = React.useState("")
  const [newPostContentType, setNewPostContentType] = React.useState<string | undefined>(undefined)
  const [newPostFormatType, setNewPostFormatType] = React.useState<string | undefined>(undefined)
  const [selectedPropertiesForDialog, setSelectedPropertiesForDialog] = React.useState<string[]>([])
  const [isCreatingPost, setIsCreatingPost] = React.useState(false)

  const fetchData = React.useCallback(async () => {
    if (!user) return
    setIsLoadingPosts(true)
    setIsLoadingLinkedItems(true)
    setIsLoadingAvailableProps(true)
    setError(null)

    try {
      // 1. Fetch Social Posts (for main table)
      const { data: postsData, error: postsError } = await supabase
        .from("social_posts")
        .select(
          `*, social_post_properties (*, properties (id, mls_number, street_number, street_direction, street_name, unit_number, city, state, zip_code, list_price, status))`,
        )
        .eq("user_id", user.id)
        .order("created_at", { ascending: false })
      if (postsError) throw postsError
      setSocialPosts((postsData as EnrichedSocialPost[]) || [])
      setIsLoadingPosts(false)

      // 2. Fetch All Linked Property Items (for second table)
      const { data: linkedItemsData, error: linkedItemsError } = await supabase
        .from("social_post_properties")
        .select(
          `*, properties (id, mls_number, street_number, street_direction, street_name, unit_number, city, state, zip_code), social_posts (id, title)`,
        )
        .eq("social_posts.user_id", user.id)
        .order("created_at", { ascending: false })
      if (linkedItemsError) throw linkedItemsError
      setAllLinkedProperties((linkedItemsData as AllLinkedPropertyItem[]) || [])
      setIsLoadingLinkedItems(false)

      // 3. Fetch Properties Available for Queue/New Post
      // This assumes NO `in_social_queue` field on properties table.
      // We find properties NOT in social_post_properties for this user.
      const { data: allUserProperties, error: allPropsError } = await supabase.from("listings").select("id")
      // Add .eq('user_id', user.id) if properties are user-specific
      if (allPropsError) throw allPropsError

      const propertyIdsInUserPosts = new Set(
        (linkedItemsData?.map((item) => item.property_id).filter(Boolean) as string[]) || [],
      )

      const { data: allPropertiesFullData, error: allPropertiesFullDataError } = await supabase
        .from("listings")
        .select("*")
        // Add .eq('user_id', user.id) if properties are user-specific
        .order("created_at", { ascending: false })

      if (allPropertiesFullDataError) throw allPropertiesFullDataError

      const availableProperties = allPropertiesFullData?.filter((p) => !propertyIdsInUserPosts.has(p.id)) || []
      setPropertiesAvailableForQueue(availableProperties)
      setIsLoadingAvailableProps(false)
    } catch (err: any) {
      console.error("Error fetching social page data:", err)
      setError(err.message || "Failed to fetch data.")
      toast({ title: "Error", description: "Could not fetch all social page data.", variant: "destructive" })
      setIsLoadingPosts(false)
      setIsLoadingLinkedItems(false)
      setIsLoadingAvailableProps(false)
    }
  }, [user, toast])

  React.useEffect(() => {
    fetchData()
  }, [fetchData])

  // ... (handleCreatePostAction, calculateProgress, handlePropertySelectionInDialog, handleDeletePost remain largely the same)
  const handleCreatePostAction = async () => {
    if (!user) {
      toast({ title: "Error", description: "You must be logged in.", variant: "destructive" })
      return
    }
    if (!newPostName.trim()) {
      toast({ title: "Error", description: "Post name cannot be empty.", variant: "destructive" })
      return
    }
    if (selectedPropertiesForDialog.length === 0) {
      toast({ title: "Error", description: "Please select at least one listing.", variant: "destructive" })
      return
    }

    setIsCreatingPost(true)

    const { data: newPost, error: postError } = await supabase
      .from("social_posts")
      .insert({
        user_id: user.id,
        title: newPostName,
        status: "draft",
        content_type: newPostContentType,
        format_type: newPostFormatType,
      })
      .select()
      .single()

    if (postError || !newPost) {
      setIsCreatingPost(false)
      toast({
        title: "Error Creating Post",
        description: postError?.message || "Failed to create post.",
        variant: "destructive",
      })
      return
    }

    const postPropertiesToInsert = selectedPropertiesForDialog.map((propertyId) => ({
      social_post_id: newPost.id,
      property_id: propertyId,
      image_complete: false,
      description_complete: false,
      contacted_complete: false,
    }))

    const { error: propertiesError } = await supabase.from("social_post_properties").insert(postPropertiesToInsert)

    if (propertiesError) {
      setIsCreatingPost(false)
      // Attempt to delete the post if linking properties failed
      await supabase.from("social_posts").delete().eq("id", newPost.id)
      toast({
        title: "Error Linking Properties",
        description: propertiesError.message || "Failed to link properties. Post creation rolled back.",
        variant: "destructive",
      })
      return
    }

    // If you were using an `in_social_queue` flag, you'd update it here.
    // Since you said it's not present, linking to social_post_properties effectively "queues" it.

    toast({ title: "Success", description: `Social post "${newPostName}" created.` })
    setIsCreatingPost(false)
    setIsCreatePostDialogOpen(false)
    setNewPostName("")
    setSelectedPropertiesForDialog([])
    setNewPostContentType(undefined) // Add this
    setNewPostFormatType(undefined) // Add this
    fetchData() // Refresh all data
  }

  const calculateProgress = (post: EnrichedSocialPost) => {
    if (!post.social_post_properties || post.social_post_properties.length === 0) return 0
    let totalCompletedTasks = 0
    const totalPossibleTasks = post.social_post_properties.length * 3
    post.social_post_properties.forEach((spp) => {
      if (spp.image_complete) totalCompletedTasks++
      if (spp.description_complete) totalCompletedTasks++
      if (spp.contacted_complete) totalCompletedTasks++
    })
    return totalPossibleTasks > 0 ? (totalCompletedTasks / totalPossibleTasks) * 100 : 0
  }

  const handlePropertySelectionInDialog = (propertyId: string) => {
    setSelectedPropertiesForDialog((prev) =>
      prev.includes(propertyId) ? prev.filter((id) => id !== propertyId) : [...prev, propertyId],
    )
  }

  const handleDeletePost = async (postId: string, postTitle: string) => {
    if (
      !confirm(
        `Are you sure you want to delete the post "${postTitle}"? This will also remove its linked properties from this post.`,
      )
    )
      return
    try {
      // No need to update `in_social_queue` if it doesn't exist.
      // Deleting from social_post_properties makes them available again by our new logic.
      await supabase.from("social_post_properties").delete().eq("social_post_id", postId)
      await supabase.from("social_posts").delete().eq("id", postId)

      toast({ title: "Success", description: `Post "${postTitle}" and its property links deleted.` })
      fetchData() // Refresh all data
    } catch (err: any) {
      toast({ title: "Error", description: `Failed to delete post: ${err.message}`, variant: "destructive" })
    }
  }

  // Columns for Main Social Posts Table (remains the same)
  const socialPostColumns = React.useMemo<ColumnDef<EnrichedSocialPost>[]>(
    () => [
      {
        id: "expander",
        header: () => null,
        cell: ({ row }) =>
          row.getCanExpand() ? (
            <Button variant="ghost" size="sm" onClick={row.getToggleExpandedHandler()} className="p-1 h-auto">
              {row.getIsExpanded() ? <ChevronDown size={18} /> : <ChevronRight size={18} />}
            </Button>
          ) : null,
        enableSorting: false,
        enableHiding: false,
      },
      {
        accessorKey: "title",
        header: ({ column }) => <DataTableColumnHeader column={column} title="Post Name" />,
        cell: ({ row }) => (
          <Link href={`/social/${row.original.id}`} className="font-medium text-primary hover:underline">
            {row.original.title}
          </Link>
        ),
      },
      {
        accessorKey: "status",
        header: ({ column }) => <DataTableColumnHeader column={column} title="Status" />,
        cell: ({ row }) => (
          <Badge variant={row.original.status === "published" ? "default" : "outline"}>{row.original.status}</Badge>
        ),
      },
      {
        id: "propertiesCount",
        header: ({ column }) => <DataTableColumnHeader column={column} title="Listings" />,
        cell: ({ row }) => row.original.social_post_properties?.length || 0,
      },
      {
        id: "progress",
        header: ({ column }) => <DataTableColumnHeader column={column} title="Progress" />,
        cell: ({ row }) => {
          const progress = calculateProgress(row.original)
          return (
            <div className="flex items-center">
              <Progress value={progress} className="w-24 h-2 mr-2" />
              <span className="text-xs">{Math.round(progress)}%</span>
            </div>
          )
        },
      },
      {
        accessorKey: "content_type",
        header: ({ column }) => <DataTableColumnHeader column={column} title="Content Type" />,
        cell: ({ row }) => row.original.content_type || "N/A",
        filterFn: (row, id, value) => {
          return value.includes(row.getValue(id))
        },
      },
      {
        accessorKey: "format_type",
        header: ({ column }) => <DataTableColumnHeader column={column} title="Format Type" />,
        cell: ({ row }) => row.original.format_type || "N/A",
        filterFn: (row, id, value) => {
          return value.includes(row.getValue(id))
        },
      },
      {
        accessorKey: "created_at",
        header: ({ column }) => <DataTableColumnHeader column={column} title="Created At" />,
        cell: ({ row }) => new Date(row.original.created_at).toLocaleDateString(),
      },
      {
        id: "actions",
        cell: ({ row }) => (
          <DropdownMenu>
            <DropdownMenuTrigger asChild>
              <Button variant="ghost" className="h-7 w-7 p-0">
                <span className="sr-only">Open menu</span>
                <MoreHorizontal className="h-4 w-4" />
              </Button>
            </DropdownMenuTrigger>
            <DropdownMenuContent align="end" className="w-[160px]">
              <DropdownMenuLabel className="text-xs">Actions</DropdownMenuLabel>
              <DropdownMenuItem className="text-xs" asChild>
                <Link href={`/social/${row.original.id}`}>
                  <Edit3 className="mr-2 h-3.5 w-3.5" />
                  View/Edit Details
                </Link>
              </DropdownMenuItem>
              <DropdownMenuSeparator />
              <DropdownMenuItem
                className="text-xs text-red-600 focus:text-red-600 focus:bg-red-50"
                onClick={() => handleDeletePost(row.original.id, row.original.title || "Untitled Post")}
              >
                <Trash2 className="mr-2 h-3.5 w-3.5" />
                Delete Post
              </DropdownMenuItem>
            </DropdownMenuContent>
          </DropdownMenu>
        ),
      },
    ],
    [fetchData],
  )

  // Sub-component for main social posts table (remains the same)
  const renderSocialPostSubComponent = ({ row }: { row: Row<EnrichedSocialPost> }) => {
    const postProperties = row.original.social_post_properties
    if (!postProperties || postProperties.length === 0) {
      return <div className="p-4 text-sm text-muted-foreground bg-muted/30">No listings linked to this post.</div>
    }
    return (
      <div className="p-2 pl-10 bg-muted/30">
        <h4 className="text-xs font-semibold mb-1 text-muted-foreground">Linked Listings:</h4>
        <ul className="space-y-1">
          {postProperties.map((spp) => (
            <li
              key={spp.property_id}
              className="text-xs flex items-center justify-between p-1 rounded hover:bg-background"
            >
              <span>{getFullAddress(spp.properties)}</span>
              <div className="flex items-center space-x-2">
                <Checkbox id={`img-${spp.id}`} checked={spp.image_complete ?? false} disabled className="h-3 w-3" />
                <Checkbox
                  id={`desc-${spp.id}`}
                  checked={spp.description_complete ?? false}
                  disabled
                  className="h-3 w-3"
                />
                <Checkbox
                  id={`contact-${spp.id}`}
                  checked={spp.contacted_complete ?? false}
                  disabled
                  className="h-3 w-3"
                />
                {spp.properties && spp.properties.id && (
                  <Link href={`/properties/${spp.properties.id}`} target="_blank" rel="noopener noreferrer">
                    <ExternalLink className="h-3 w-3 text-muted-foreground hover:text-primary" />
                  </Link>
                )}
              </div>
            </li>
          ))}
        </ul>
      </div>
    )
  }

  // Columns for "All Linked Properties" Table (remains the same)
  const linkedPropertyItemsColumns = React.useMemo<ColumnDef<AllLinkedPropertyItem>[]>(
    () => [
      {
        id: "propertyAddress",
        header: ({ column }) => <DataTableColumnHeader column={column} title="Property Address" />,
        cell: ({ row }) => (
          <Link href={`/properties/${row.original.properties?.id}`} className="hover:underline text-primary">
            {getFullAddress(row.original.properties)}
          </Link>
        ),
        accessorFn: (row) => getFullAddress(row.properties),
      },
      {
        id: "socialPostTitle",
        header: ({ column }) => <DataTableColumnHeader column={column} title="Social Post" />,
        cell: ({ row }) => (
          <Link href={`/social/${row.original.social_posts?.id}`} className="hover:underline">
            {row.original.social_posts?.title || "N/A"}
          </Link>
        ),
        accessorFn: (row) => row.social_posts?.title,
      },
      {
        accessorKey: "image_complete",
        header: ({ column }) => <DataTableColumnHeader column={column} title="Image" />,
        cell: ({ row }) =>
          row.original.image_complete ? (
            <CheckCircle2 className="h-4 w-4 text-green-500" />
          ) : (
            <XCircle className="h-4 w-4 text-muted-foreground" />
          ),
      },
      {
        accessorKey: "description_complete",
        header: ({ column }) => <DataTableColumnHeader column={column} title="Description" />,
        cell: ({ row }) =>
          row.original.description_complete ? (
            <CheckCircle2 className="h-4 w-4 text-green-500" />
          ) : (
            <XCircle className="h-4 w-4 text-muted-foreground" />
          ),
      },
      {
        accessorKey: "contacted_complete",
        header: ({ column }) => <DataTableColumnHeader column={column} title="Contacted" />,
        cell: ({ row }) =>
          row.original.contacted_complete ? (
            <CheckCircle2 className="h-4 w-4 text-green-500" />
          ) : (
            <XCircle className="h-4 w-4 text-muted-foreground" />
          ),
      },
      {
        accessorKey: "created_at",
        header: ({ column }) => <DataTableColumnHeader column={column} title="Date Linked" />,
        cell: ({ row }) => new Date(row.original.created_at).toLocaleDateString(),
      },
    ],
    [],
  )

  // Columns for "Properties Available for Social Queue" Table (NEW/REVISED)
  const availablePropertiesColumns = React.useMemo<ColumnDef<ListingRow>[]>(
    () => [
      {
        id: "select",
        header: ({ table }) => (
          <Checkbox
            checked={
              table.getIsAllPageRowsSelected() ||
              (selectedPropertiesForDialog.length > 0 &&
                propertiesAvailableForQueue.every((p) => selectedPropertiesForDialog.includes(p.id)))
            }
            onCheckedChange={(value) => {
              const allCurrentPageIds = table.getFilteredRowModel().rows.map((row) => row.original.id)
              if (!!value) {
                setSelectedPropertiesForDialog((prev) => Array.from(new Set([...prev, ...allCurrentPageIds])))
              } else {
                setSelectedPropertiesForDialog((prev) => prev.filter((id) => !allCurrentPageIds.includes(id)))
              }
              table.toggleAllPageRowsSelected(!!value)
            }}
            aria-label="Select all on current page"
          />
        ),
        cell: ({ row }) => (
          <Checkbox
            checked={selectedPropertiesForDialog.includes(row.original.id)}
            onCheckedChange={() => handlePropertySelectionInDialog(row.original.id)}
            aria-label="Select row"
          />
        ),
        enableSorting: false,
        enableHiding: false,
      },
      {
        accessorKey: "mls_number",
        header: ({ column }) => <DataTableColumnHeader column={column} title="MLS#" />,
      },
      {
        id: "address",
        header: ({ column }) => <DataTableColumnHeader column={column} title="Address" />,
        cell: ({ row }) => getFullAddress(row.original),
        accessorFn: (row) => getFullAddress(row),
      },
      {
        accessorKey: "status",
        header: ({ column }) => <DataTableColumnHeader column={column} title="Status" />,
        cell: ({ row }) => <Badge variant="outline">{row.original.status}</Badge>,
      },
      {
        accessorKey: "list_price",
        header: ({ column }) => <DataTableColumnHeader column={column} title="List Price" />,
        cell: ({ row }) => formatCurrency(row.original.list_price),
      },
    ],
    [selectedPropertiesForDialog, propertiesAvailableForQueue], // Ensure re-render on selection change
  )

  if (error && !isLoadingPosts && !isLoadingLinkedItems && !isLoadingAvailableProps) {
    return (
      <Alert variant="destructive">
        <AlertCircle className="h-4 w-4" />
        <AlertTitle>Error</AlertTitle>
        <AlertDescription>{error} Please try refreshing the page.</AlertDescription>
      </Alert>
    )
  }

  return (
    <div className="space-y-8">
      {/* Section 1: Social Media Posts Table */}
      <section>
        <div className="flex justify-between items-center mb-4">
          <h1 className="text-2xl font-semibold">Social Media Posts</h1>
          {/* "Create Post" Dialog Trigger - now uses propertiesAvailableForQueue */}
          <Dialog open={isCreatePostDialogOpen} onOpenChange={setIsCreatePostDialogOpen}>
            <DialogTrigger asChild>
              <Button
                onClick={() => {
                  /* setSelectedPropertiesForDialog([]); // Clear previous selections if opening fresh */
                  setIsCreatePostDialogOpen(true)
                }}
              >
                <PlusCircle className="mr-2 h-4 w-4" /> Create New Post
              </Button>
            </DialogTrigger>
            <DialogContent className="sm:max-w-[600px]">
              <DialogHeader>
                <DialogTitle>Create New Social Post</DialogTitle>
                <DialogDescription>
                  Name your post and select listings from the list of available listings below.
                </DialogDescription>
              </DialogHeader>
              <div className="grid gap-4 py-4">
                <div className="grid grid-cols-4 items-center gap-4">
                  <Label htmlFor="post-name-input" className="text-right">
                    Post Name
                  </Label>
                  <Input
                    id="post-name-input"
                    value={newPostName}
                    onChange={(e) => setNewPostName(e.target.value)}
                    className="col-span-3"
                    placeholder="e.g., Spring Listings Showcase"
                  />
                </div>
                <div className="grid grid-cols-4 items-center gap-4">
                  <Label htmlFor="post-content-type" className="text-right">
                    Content Type
                  </Label>
                  <Select value={newPostContentType} onValueChange={setNewPostContentType}>
                    <SelectTrigger id="post-content-type" className="col-span-3">
                      <SelectValue placeholder="Select content type" />
                    </SelectTrigger>
                    <SelectContent>
                      <SelectItem value="Single Property">Single Property</SelectItem>
                      <SelectItem value="Multi Property">Multi Property</SelectItem>
                    </SelectContent>
                  </Select>
                </div>
                <div className="grid grid-cols-4 items-center gap-4">
                  <Label htmlFor="post-format-type" className="text-right">
                    Format Type
                  </Label>
                  <Select value={newPostFormatType} onValueChange={setNewPostFormatType}>
                    <SelectTrigger id="post-format-type" className="col-span-3">
                      <SelectValue placeholder="Select format type" />
                    </SelectTrigger>
                    <SelectContent>
                      <SelectItem value="Carousel">Carousel</SelectItem>
                      <SelectItem value="Post">Post</SelectItem>
                      <SelectItem value="Reel">Reel</SelectItem>
                      <SelectItem value="Story">Story</SelectItem>
                    </SelectContent>
                  </Select>
                </div>
                <div className="space-y-2">
                  <Label>Available Listings ({propertiesAvailableForQueue.length} not in any of your posts)</Label>
                  {isLoadingAvailableProps ? (
                    <Loader2 className="h-5 w-5 animate-spin text-muted-foreground mx-auto my-4" />
                  ) : propertiesAvailableForQueue.length === 0 ? (
                    <p className="text-sm text-muted-foreground p-4 border rounded-md text-center">
                      No listings available to add to a new post.
                    </p>
                  ) : (
                    <div className="max-h-60 overflow-y-auto border rounded-md p-2 space-y-1">
                      {propertiesAvailableForQueue.map((prop) => (
                        <div
                          key={prop.id}
                          className="flex items-center justify-between p-2 rounded hover:bg-muted/50 cursor-pointer"
                          onClick={() => handlePropertySelectionInDialog(prop.id)}
                        >
                          <div className="flex items-center space-x-2">
                            <Checkbox
                              checked={selectedPropertiesForDialog.includes(prop.id)}
                              onCheckedChange={() => handlePropertySelectionInDialog(prop.id)}
                              id={`dialog-prop-select-${prop.id}`}
                              aria-labelledby={`dialog-prop-label-${prop.id}`}
                            />
                            <Label
                              htmlFor={`dialog-prop-select-${prop.id}`}
                              id={`dialog-prop-label-${prop.id}`}
                              className="text-sm font-normal cursor-pointer"
                            >
                              {getFullAddress(prop)}
                            </Label>
                          </div>
                          <span className="text-xs text-muted-foreground">{prop.mls_number}</span>
                        </div>
                      ))}
                    </div>
                  )}
                </div>
                {selectedPropertiesForDialog.length > 0 && (
                  <p className="text-sm text-muted-foreground">
                    {selectedPropertiesForDialog.length} listing{selectedPropertiesForDialog.length === 1 ? "" : "s"}{" "}
                    selected.
                  </p>
                )}
              </div>
              <DialogFooter>
                <Button
                  variant="outline"
                  onClick={() => {
                    setIsCreatePostDialogOpen(false) /* setSelectedPropertiesForDialog([]); */
                  }}
                >
                  Cancel
                </Button>
                <Button
                  onClick={handleCreatePostAction}
                  disabled={
                    isCreatingPost ||
                    !newPostName.trim() ||
                    selectedPropertiesForDialog.length === 0 ||
                    !newPostContentType ||
                    !newPostFormatType
                  }
                >
                  {isCreatingPost ? <Loader2 className="mr-2 h-4 w-4 animate-spin" /> : "Create Post"}
                </Button>
              </DialogFooter>
            </DialogContent>
          </Dialog>
        </div>
        <DataTable
          columns={socialPostColumns}
          data={socialPosts}
          loading={isLoadingPosts}
          renderSubComponent={renderSocialPostSubComponent}
          searchColumn="title"
        />
        {socialPosts.length === 0 && !isLoadingPosts && !error && (
          <div className="text-center py-10 border-2 border-dashed rounded-lg">
            <PackagePlus className="mx-auto h-12 w-12 text-muted-foreground" />
            <h3 className="mt-2 text-lg font-medium text-muted-foreground">No Social Posts Yet</h3>
            <p className="text-sm text-muted-foreground mt-1">Click "Create Post" to get started.</p>
          </div>
        )}
      </section>

      {/* Section 2: All Properties Currently Linked in User's Social Posts */}
      <section className="mt-12">
        <div className="flex justify-between items-center mb-4">
          <h2 className="text-xl font-semibold">All Listings Currently Linked in Your Social Posts</h2>
        </div>
        <DataTable
          columns={linkedPropertyItemsColumns}
          data={allLinkedProperties}
          loading={isLoadingLinkedItems}
          searchColumn="propertyAddress"
        />
        {allLinkedProperties.length === 0 && !isLoadingLinkedItems && !error && (
          <div className="text-center py-10 border-2 border-dashed rounded-lg">
            <ListPlus className="mx-auto h-12 w-12 text-muted-foreground" />
            <h3 className="mt-2 text-lg font-medium text-muted-foreground">No Properties Linked to Your Posts</h3>
            <p className="text-sm text-muted-foreground mt-1">
              Create posts and link properties; they will appear here.
            </p>
          </div>
        )}
      </section>

      {/* Section 3: Properties Available for Social Queue (NEW/REVISED) */}
      <section className="mt-12">
        <div className="flex justify-between items-center mb-4">
          <h2 className="text-xl font-semibold">Listings Available for Social Posts</h2>
          {selectedPropertiesForDialog.length > 0 && (
            <Button onClick={() => setIsCreatePostDialogOpen(true)}>
              <PlusCircle className="mr-2 h-4 w-4" /> Create Post with {selectedPropertiesForDialog.length} Selected
            </Button>
          )}
        </div>
        <DataTable
          columns={availablePropertiesColumns}
          data={propertiesAvailableForQueue}
          loading={isLoadingAvailableProps}
          searchColumn="address" // Search by address
        />
        {propertiesAvailableForQueue.length === 0 && !isLoadingAvailableProps && !error && (
          <div className="text-center py-10 border-2 border-dashed rounded-lg">
            <ListPlus className="mx-auto h-12 w-12 text-muted-foreground" />
            <h3 className="mt-2 text-lg font-medium text-muted-foreground">No Listings Available for New Posts</h3>
            <p className="text-sm text-muted-foreground mt-1">
              All properties might be in existing posts, or no properties are available.
            </p>
          </div>
        )}
      </section>
    </div>
  )
}
```

## File: dkl-microapp-2-main/app/(dashboard)/layout.tsx
```typescript
"use client"

import type React from "react"
import { useState, useEffect, useCallback } from "react"
import { useAuth } from "@/contexts/auth-context"
import { Sidebar } from "@/components/layout/sidebar"
import { Header } from "@/components/layout/header"
import { redirect, usePathname } from "next/navigation"
import { Loader2 } from "lucide-react"
import { supabase } from "@/lib/supabase/client"
import { hexToHsl } from "@/lib/color-utils"

// Default HSL values from globals.css (light mode)
const DEFAULT_PRIMARY_HSL = "240 5.9% 10%"
const DEFAULT_PRIMARY_FOREGROUND_HSL = "0 0% 98%"

export default function DashboardLayout({ children }: { children: React.ReactNode }) {
  const { user, loading: authLoading, session } = useAuth()
  const [themeLoading, setThemeLoading] = useState(true)
  const pathname = usePathname()

  const applyThemeToDocument = useCallback((primaryHsl: string, foregroundHsl: string) => {
    if (typeof document !== "undefined") {
      document.documentElement.style.setProperty("--primary", primaryHsl)
      document.documentElement.style.setProperty("--primary-foreground", foregroundHsl)
    }
  }, [])

  useEffect(() => {
    const fetchAndApplyTheme = async () => {
      if (authLoading) {
        setThemeLoading(true)
        return
      }

      setThemeLoading(true)

      if (user && session) {
        try {
          const { data, error } = await supabase
            .from("user_settings")
            .select("primary_color_hex, primary_foreground_color_hex")
            .eq("user_id", user.id)
            .single()

          if (error && error.code !== "PGRST116") {
            console.error("Error fetching theme settings:", error)
            applyThemeToDocument(DEFAULT_PRIMARY_HSL, DEFAULT_PRIMARY_FOREGROUND_HSL)
          } else if (data) {
            const primaryHsl = data.primary_color_hex ? hexToHsl(data.primary_color_hex) : null
            const foregroundHsl = data.primary_foreground_color_hex ? hexToHsl(data.primary_foreground_color_hex) : null

            applyThemeToDocument(primaryHsl || DEFAULT_PRIMARY_HSL, foregroundHsl || DEFAULT_PRIMARY_FOREGROUND_HSL)
          } else {
            applyThemeToDocument(DEFAULT_PRIMARY_HSL, DEFAULT_PRIMARY_FOREGROUND_HSL)
          }
        } catch (e) {
          console.error("Exception during theme settings fetch:", e)
          applyThemeToDocument(DEFAULT_PRIMARY_HSL, DEFAULT_PRIMARY_FOREGROUND_HSL)
        } finally {
          setThemeLoading(false)
        }
      } else {
        applyThemeToDocument(DEFAULT_PRIMARY_HSL, DEFAULT_PRIMARY_FOREGROUND_HSL)
        setThemeLoading(false)
      }
    }

    fetchAndApplyTheme()
  }, [user, session, authLoading, applyThemeToDocument, pathname])

  if (authLoading || themeLoading) {
    return (
      <div className="flex h-screen items-center justify-center">
        <Loader2 className="h-8 w-8 animate-spin text-primary" />
        <p className="ml-2 text-sm text-muted-foreground">Initializing...</p>
      </div>
    )
  }

  if (!user && !session && (pathname.startsWith("/dashboard") || pathname === "/")) {
    redirect("/login")
    return null
  }

  if (!user && (pathname === "/login" || pathname === "/register")) {
    return <>{children}</>
  }

  if (user && (pathname === "/login" || pathname === "/register")) {
    redirect("/dashboard")
    return null
  }

  if (!user && !pathname.startsWith("/login") && !pathname.startsWith("/register")) {
    redirect("/login")
    return null
  }

  return (
    <div className="flex h-screen">
      <Sidebar />
      <div className="flex flex-1 flex-col">
        <Header />
        <main className="flex-1 overflow-auto bg-gray-50/30 p-4">{children}</main>
      </div>
    </div>
  )
}
```

## File: dkl-microapp-2-main/app/actions/ai-actions.ts
```typescript
"use server"

import { createServerClient } from "@/lib/supabase/server"
import { openai } from "@ai-sdk/openai" // Use Vercel AI SDK
import { generateText, type CoreMessage } from "ai" // Use Vercel AI SDK

export async function generateDescriptionWithAI(
  actionType: "rewrite" | "prompt",
  text: string, // For "rewrite", this is the text to rewrite. For "prompt", this is the custom prompt.
  contextText?: string, // For "prompt", this is the existing description to provide as context.
): Promise<{ generatedText: string | null; error: string | null }> {
  console.log(
    `AI Action: Started - Type: ${actionType}, Text Length: ${text.length}, Context Length: ${contextText?.length || 0}`,
  )

  const supabase = await createServerClient() // Correctly instantiate server client
  const {
    data: { user },
    error: userError,
  } = await supabase.auth.getUser()

  if (userError || !user) {
    console.error("AI Action: User not authenticated.", userError)
    return { generatedText: null, error: "User not authenticated. Please log in." }
  }
  console.log("AI Action: User authenticated:", user.id)

  const { data: userSettings, error: settingsError } = await supabase
    .from("user_settings") // Corrected table name from previous iterations
    .select("openai_api_key, openai_model")
    .eq("user_id", user.id)
    .single()

  if (settingsError) {
    console.error("AI Action: Error fetching user settings.", settingsError)
    if (settingsError.code === "PGRST116") {
      // No row found
      return {
        generatedText: null,
        error: "AI settings not found. Please configure your OpenAI API key and model in the Integrations settings.",
      }
    }
    return { generatedText: null, error: `Could not load AI settings: ${settingsError.message}` }
  }

  if (!userSettings) {
    // Should be caught by PGRST116, but as a safeguard
    console.error("AI Action: User settings are unexpectedly null after query.")
    return {
      generatedText: null,
      error: "AI settings not found. Please configure your OpenAI API key and model in the Integrations settings.",
    }
  }

  console.log(
    "AI Action: User settings fetched. Has API Key:",
    !!userSettings.openai_api_key,
    "Model:",
    userSettings.openai_model,
  )

  if (!userSettings.openai_api_key) {
    console.warn("AI Action: OpenAI API key not configured for user:", user.id)
    return { generatedText: null, error: "OpenAI API key not configured. Please add it in the Integrations settings." }
  }

  const openAIModel = userSettings.openai_model || "gpt-3.5-turbo" // Default model if not set

  try {
    let systemPromptMessage = ""
    const messages: CoreMessage[] = []

    if (actionType === "rewrite") {
      systemPromptMessage =
        "You are an expert real estate copywriter. Rewrite the following property description to be more engaging, concise, or as instructed by the user. Retain key details and the original intent unless specified otherwise. Focus on clarity and appeal for potential buyers or renters."
      messages.push({ role: "user", content: `Rewrite this listing description: "${text}"` })
    } else if (actionType === "prompt") {
      systemPromptMessage =
        "You are an expert real estate copywriter. Generate a property description based on the user's prompt. If context (current description) is provided, use it to inform your response, either by enhancing, replacing, or building upon it as per the user's prompt. Aim for compelling and accurate real estate copy."
      let userPromptContent = `User Prompt: "${text}"`
      if (contextText && contextText.trim() !== "") {
        userPromptContent += `\n\nFor context, here is the current description (you can choose to ignore, enhance, or replace it based on my prompt): "${contextText}"`
      }
      messages.push({ role: "user", content: userPromptContent })
    }

    console.log(
      `AI Action: Calling OpenAI. Model: ${openAIModel}. System Prompt: ${systemPromptMessage.substring(0, 100)}... Messages:`,
      messages.map((m) => ({ role: m.role, content: (m.content as string)?.substring(0, 100) + "..." })),
    )

    const {
      text: resultText,
      finishReason,
      usage,
    } = await generateText({
      model: openai(openAIModel, { apiKey: userSettings.openai_api_key }), // Pass API key here
      system: systemPromptMessage,
      messages: messages,
      // temperature: 0.7, // Optional: Adjust creativity
    })

    console.log(
      "AI Action: OpenAI response received. Finish Reason:",
      finishReason,
      "Usage:",
      usage,
      "Generated Text Length:",
      resultText?.length,
    )

    if (!resultText && finishReason !== "stop" && finishReason !== "length") {
      console.error("AI Action: OpenAI generation failed or returned empty text. Finish Reason:", finishReason)
      return { generatedText: null, error: `AI generation failed. Reason: ${finishReason || "unknown"}` }
    }

    console.log("AI Action: Successfully generated text.")
    return { generatedText: resultText || "", error: null } // Ensure generatedText is at least an empty string if null
  } catch (error: any) {
    console.error("AI Action: OpenAI API call error.", error)
    let errorMessage = "An error occurred while generating text with AI."
    if (error.message) {
      errorMessage = error.message
    }
    // Specific error checks for OpenAI
    if (error.status === 401) errorMessage = "Invalid OpenAI API key. Please check your key in settings."
    if (error.status === 429)
      errorMessage = "OpenAI API rate limit exceeded or quota finished. Please check your OpenAI account."
    if (error.name === "AbortError") errorMessage = "The AI request timed out."

    return { generatedText: null, error: errorMessage }
  }
}
```

## File: dkl-microapp-2-main/app/globals.css
```css
@tailwind base;
@tailwind components;
@tailwind utilities;

@layer base {
  :root {
    --background: 0 0% 100%;
    --foreground: 222.2 84% 4.9%;
    --card: 0 0% 100%;
    --card-foreground: 222.2 84% 4.9%;
    --popover: 0 0% 100%;
    --popover-foreground: 222.2 84% 4.9%;
    --primary: 222.2 47.4% 11.2%;
    --primary-foreground: 210 40% 98%;
    --secondary: 210 40% 96.1%;
    --secondary-foreground: 222.2 47.4% 11.2%;
    --muted: 210 40% 96.1%;
    --muted-foreground: 215.4 16.3% 46.9%;
    --accent: 210 40% 96.1%;
    --accent-foreground: 222.2 47.4% 11.2%;
    --destructive: 0 84.2% 60.2%;
    --destructive-foreground: 210 40% 98%;
    --border: 214.3 31.8% 91.4%;
    --input: 214.3 31.8% 91.4%;
    --ring: 222.2 84% 4.9%;
    --radius: 0.3rem;
  }
}

@layer base {
  * {
    @apply border-border;
  }
  body {
    @apply bg-background text-foreground text-xs;
    font-family: var(--font-inter);
  }
}

/* Dense Attio-like styles */
.dense-table {
  font-size: 11px;
  line-height: 1.25;
}

.dense-table th {
  padding: 0.375rem 0.5rem;
  font-weight: 500;
}

.dense-table td {
  padding: 0.25rem 0.5rem;
}

.compact-card {
  padding: 0.75rem;
}

.compact-input {
  height: 1.75rem;
  font-size: 0.75rem;
  padding-left: 0.5rem;
  padding-right: 0.5rem;
}

.compact-button {
  height: 1.75rem;
  font-size: 0.75rem;
  padding-left: 0.75rem;
  padding-right: 0.75rem;
}

.compact-select {
  height: 1.75rem;
  font-size: 0.75rem;
}

/* Scrollbar styling */
::-webkit-scrollbar {
  width: 0.5rem;
  height: 0.5rem;
}

::-webkit-scrollbar-track {
  background-color: #f3f4f6;
}

::-webkit-scrollbar-thumb {
  background-color: #d1d5db;
  border-radius: 0.25rem;
}

::-webkit-scrollbar-thumb:hover {
  background-color: #9ca3af;
}

.mapboxgl-ctrl-logo {
  display: none !important;
}

.mapboxgl-ctrl-attrib {
  display: none !important;
}
```

## File: dkl-microapp-2-main/app/layout.tsx
```typescript
import type React from "react"
import type { Metadata } from "next"
import { Inter } from "next/font/google"
import "./globals.css"
import { Toaster } from "@/components/ui/toaster"
import { AuthProvider } from "@/contexts/auth-context"
import { ThemeProvider } from "@/components/theme-provider" // Assuming you have this

const inter = Inter({ subsets: ["latin"], variable: "--font-inter" })

export const metadata: Metadata = {
  title: "Real Estate Platform",
  description: "Manage and analyze real estate properties and builders.",
    generator: 'v0.dev'
}

export default function RootLayout({
  children,
}: Readonly<{
  children: React.ReactNode
}>) {
  return (
    <html lang="en" suppressHydrationWarning>
      <head>
        <link href="https://api.mapbox.com/mapbox-gl-js/v3.4.0/mapbox-gl.css" rel="stylesheet" />
      </head>
      <body className={inter.variable}>
        <AuthProvider>
          <ThemeProvider attribute="class" defaultTheme="system" enableSystem disableTransitionOnChange>
            {children}
            <Toaster />
          </ThemeProvider>
        </AuthProvider>
      </body>
    </html>
  )
}
```

## File: dkl-microapp-2-main/app/page.tsx
```typescript
import { redirect } from "next/navigation"

export default function HomePage() {
  // This component should ideally check auth status before redirecting,
  // or rely on the layout to handle it.
  // For simplicity, Next.js middleware or the root layout is often
  // a better place for initial auth checks and redirects.
  // Given our current structure, the redirect in app/(dashboard)/layout.tsx
  // will handle unauthenticated users trying to access dashboard routes.
  // This page itself might briefly render before that layout kicks in if not careful.
  // However, since it's just a redirect, it's usually fine.
  redirect("/dashboard")
  // return null; // Or a loading indicator if preferred
}
```

## File: dkl-microapp-2-main/components/layout/header.tsx
```typescript
"use client"

import { useAuth } from "@/contexts/auth-context"
import { Button } from "@/components/ui/button"
import { Input } from "@/components/ui/input"
import {
  DropdownMenu,
  DropdownMenuContent,
  DropdownMenuItem,
  DropdownMenuLabel,
  DropdownMenuSeparator,
  DropdownMenuTrigger,
} from "@/components/ui/dropdown-menu"
import { User, LogOut, Settings, Search } from "lucide-react"
import Link from "next/link"

export function Header() {
  const { user, signOut } = useAuth()

  return (
    <header className="flex h-12 items-center justify-between border-b bg-white px-4">
      <div className="flex items-center gap-x-4">
        <div className="relative">
          <Search className="absolute left-2.5 top-1/2 h-3.5 w-3.5 -translate-y-1/2 text-muted-foreground" />
          <Input
            type="search"
            placeholder="Search properties, builders..."
            className="h-7 w-64 rounded pl-8 text-xs attio-input" // Using attio-input for consistency if defined elsewhere, or remove for default shadcn
          />
        </div>
      </div>

      <div className="flex items-center gap-x-2">
        <DropdownMenu>
          <DropdownMenuTrigger asChild>
            <Button variant="ghost" size="sm" className="h-7 gap-x-1 px-2">
              <User className="h-3.5 w-3.5" />
              <span className="text-xs">{user?.email}</span>
            </Button>
          </DropdownMenuTrigger>
          <DropdownMenuContent align="end" className="w-48">
            <DropdownMenuLabel className="text-xs">My Account</DropdownMenuLabel>
            <DropdownMenuSeparator />
            <DropdownMenuItem asChild>
              <Link href="/settings" className="text-xs">
                <Settings className="mr-2 h-3.5 w-3.5" />
                Settings
              </Link>
            </DropdownMenuItem>
            <DropdownMenuItem onClick={() => signOut()} className="text-xs">
              <LogOut className="mr-2 h-3.5 w-3.5" />
              Sign out
            </DropdownMenuItem>
          </DropdownMenuContent>
        </DropdownMenu>
      </div>
    </header>
  )
}
```

## File: dkl-microapp-2-main/components/layout/sidebar.tsx
```typescript
"use client"

import Link from "next/link"
import { usePathname } from "next/navigation"
import { cn } from "@/lib/utils"
import {
  LayoutDashboard,
  Building2,
  Users,
  TrendingUp,
  Upload,
  Settings,
  BarChart3,
  FileText,
  Share2,
} from "lucide-react"

const navigation = [
  { name: "Dashboard", href: "/dashboard", icon: LayoutDashboard },
  { name: "Listings", href: "/listings", icon: Building2 },
  { name: "Builders", href: "/builders", icon: Users },
  { name: "Social Posts", href: "/social", icon: Share2 },
  { name: "Market Insights", href: "/insights", icon: TrendingUp },
  { name: "Reports", href: "/reports", icon: FileText },
  { name: "Analytics", href: "/analytics", icon: BarChart3 },
  { name: "Import Data", href: "/import", icon: Upload },
  { name: "Settings", href: "/settings", icon: Settings },
]

export function Sidebar() {
  const pathname = usePathname()

  return (
    <div className="flex h-full w-48 flex-col border-r bg-gray-50/50">
      <div className="flex h-12 items-center border-b px-4">
        <Link href="/dashboard" aria-label="Go to dashboard">
          <svg
            width="105.13"
            height="36"
            viewBox="0 0 1577 541"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
            className="h-auto"
            style={{ height: "20px" }}
          >
            <rect x="76.2188" y="76.436" width="178.273" height="178.273" fill="currentColor" />
            <path
              d="M296.199 76.436C321.646 76.436 346.844 81.4483 370.354 91.1868C393.864 100.925 415.225 115.199 433.219 133.193C451.213 151.188 465.486 172.55 475.224 196.061C484.963 219.571 489.975 244.77 489.975 270.218C489.975 295.666 484.963 320.864 475.224 344.375C465.486 367.885 451.213 389.248 433.219 407.242C415.225 425.236 393.864 439.51 370.354 449.249C346.844 458.987 321.646 463.999 296.199 463.999L296.199 76.436Z"
              fill="currentColor"
            />
            <circle cx="165.355" cy="374.863" r="89.1367" fill="currentColor" />
            <path
              d="M1401.56 186.084C1421.34 186.084 1438.65 189.606 1453.49 196.651C1468.33 203.697 1479.88 213.515 1488.12 226.106C1496.51 238.698 1500.71 253.462 1500.71 270.401C1500.71 287.189 1496.51 301.954 1488.12 314.695C1479.88 327.287 1468.33 337.105 1453.49 344.15C1438.65 351.195 1421.34 354.718 1401.56 354.718H1319.26V186.084H1401.56ZM1361.53 337.405L1340.85 317.169H1404.7C1415.5 317.169 1424.86 315.22 1432.81 311.323C1440.75 307.425 1446.9 302.029 1451.25 295.134C1455.59 288.089 1457.77 279.844 1457.77 270.401C1457.77 260.807 1455.59 252.563 1451.25 245.668C1446.9 238.773 1440.75 233.376 1432.81 229.479C1424.86 225.582 1415.5 223.633 1404.7 223.633H1340.85L1361.53 203.397V337.405Z"
              fill="currentColor"
            />
            <path
              d="M1126.16 260.283H1189.34C1197.28 260.283 1203.58 258.484 1208.23 254.886C1212.87 251.139 1215.2 245.968 1215.2 239.372C1215.2 232.777 1212.87 227.68 1208.23 224.083C1203.58 220.335 1197.28 218.461 1189.34 218.461H1120.09L1139.2 197.551V354.718H1096.7V186.084H1194.96C1207.55 186.084 1218.57 188.332 1228.01 192.829C1237.46 197.326 1244.8 203.547 1250.05 211.491C1255.29 219.436 1257.92 228.729 1257.92 239.372C1257.92 249.865 1255.29 259.084 1250.05 267.028C1244.8 274.973 1237.46 281.193 1228.01 285.69C1218.57 290.037 1207.55 292.211 1194.96 292.211H1126.16V260.283ZM1153.36 275.797H1201.26L1263.31 354.718H1214.07L1153.36 275.797Z"
              fill="currentColor"
            />
            <path
              d="M935.3 186.084V335.831L916.189 317.169H1042.55V354.718H892.805V186.084H935.3Z"
              fill="currentColor"
            />
            <path
              d="M734.969 186.084C754.756 186.084 772.069 189.606 786.908 196.651C801.748 203.697 813.29 213.515 821.535 226.106C829.929 238.698 834.126 253.462 834.126 270.401C834.126 287.189 829.929 301.954 821.535 314.695C813.29 327.287 801.748 337.105 786.908 344.15C772.069 351.195 754.756 354.718 734.969 354.718H652.676V186.084H734.969ZM694.947 337.405L674.261 317.169H738.117C748.91 317.169 758.278 315.22 766.223 311.323C774.167 307.425 780.313 302.029 784.66 295.134C789.007 288.089 791.181 279.844 791.181 270.401C791.181 260.807 789.007 252.563 784.66 245.668C780.313 238.773 774.167 233.376 766.223 229.479C758.278 225.582 748.91 223.633 738.117 223.633H674.261L694.947 203.397V337.405Z"
              fill="currentColor"
            />
          </svg>
        </Link>
      </div>
      <nav className="flex-1 space-y-0.5 p-2">
        {navigation.map((item) => {
          const isActive = pathname === item.href || (item.href !== "/dashboard" && pathname.startsWith(item.href))
          return (
            <Link
              key={item.name}
              href={item.href}
              className={cn(
                "flex items-center gap-x-2 rounded px-2 py-1.5 text-xs font-medium transition-colors",
                isActive
                  ? "bg-primary text-primary-foreground"
                  : "text-muted-foreground hover:bg-accent hover:text-accent-foreground",
              )}
            >
              <item.icon className="h-3.5 w-3.5" />
              {item.name}
            </Link>
          )
        })}
      </nav>
    </div>
  )
}
```

## File: dkl-microapp-2-main/components/ui/alert-dialog.tsx
```typescript
"use client"

import * as React from "react"
import * as AlertDialogPrimitive from "@radix-ui/react-alert-dialog"

import { cn } from "@/lib/utils"
import { buttonVariants } from "@/components/ui/button"

const AlertDialog = AlertDialogPrimitive.Root

const AlertDialogTrigger = AlertDialogPrimitive.Trigger

const AlertDialogPortal = AlertDialogPrimitive.Portal

const AlertDialogOverlay = React.forwardRef<
  React.ElementRef<typeof AlertDialogPrimitive.Overlay>,
  React.ComponentPropsWithoutRef<typeof AlertDialogPrimitive.Overlay>
>(({ className, ...props }, ref) => (
  <AlertDialogPrimitive.Overlay
    className={cn(
      "fixed inset-0 z-50 bg-black/80  data-[state=open]:animate-in data-[state=closed]:animate-out data-[state=closed]:fade-out-0 data-[state=open]:fade-in-0",
      className
    )}
    {...props}
    ref={ref}
  />
))
AlertDialogOverlay.displayName = AlertDialogPrimitive.Overlay.displayName

const AlertDialogContent = React.forwardRef<
  React.ElementRef<typeof AlertDialogPrimitive.Content>,
  React.ComponentPropsWithoutRef<typeof AlertDialogPrimitive.Content>
>(({ className, ...props }, ref) => (
  <AlertDialogPortal>
    <AlertDialogOverlay />
    <AlertDialogPrimitive.Content
      ref={ref}
      className={cn(
        "fixed left-[50%] top-[50%] z-50 grid w-full max-w-lg translate-x-[-50%] translate-y-[-50%] gap-4 border bg-background p-6 shadow-lg duration-200 data-[state=open]:animate-in data-[state=closed]:animate-out data-[state=closed]:fade-out-0 data-[state=open]:fade-in-0 data-[state=closed]:zoom-out-95 data-[state=open]:zoom-in-95 data-[state=closed]:slide-out-to-left-1/2 data-[state=closed]:slide-out-to-top-[48%] data-[state=open]:slide-in-from-left-1/2 data-[state=open]:slide-in-from-top-[48%] sm:rounded-lg",
        className
      )}
      {...props}
    />
  </AlertDialogPortal>
))
AlertDialogContent.displayName = AlertDialogPrimitive.Content.displayName

const AlertDialogHeader = ({
  className,
  ...props
}: React.HTMLAttributes<HTMLDivElement>) => (
  <div
    className={cn(
      "flex flex-col space-y-2 text-center sm:text-left",
      className
    )}
    {...props}
  />
)
AlertDialogHeader.displayName = "AlertDialogHeader"

const AlertDialogFooter = ({
  className,
  ...props
}: React.HTMLAttributes<HTMLDivElement>) => (
  <div
    className={cn(
      "flex flex-col-reverse sm:flex-row sm:justify-end sm:space-x-2",
      className
    )}
    {...props}
  />
)
AlertDialogFooter.displayName = "AlertDialogFooter"

const AlertDialogTitle = React.forwardRef<
  React.ElementRef<typeof AlertDialogPrimitive.Title>,
  React.ComponentPropsWithoutRef<typeof AlertDialogPrimitive.Title>
>(({ className, ...props }, ref) => (
  <AlertDialogPrimitive.Title
    ref={ref}
    className={cn("text-lg font-semibold", className)}
    {...props}
  />
))
AlertDialogTitle.displayName = AlertDialogPrimitive.Title.displayName

const AlertDialogDescription = React.forwardRef<
  React.ElementRef<typeof AlertDialogPrimitive.Description>,
  React.ComponentPropsWithoutRef<typeof AlertDialogPrimitive.Description>
>(({ className, ...props }, ref) => (
  <AlertDialogPrimitive.Description
    ref={ref}
    className={cn("text-sm text-muted-foreground", className)}
    {...props}
  />
))
AlertDialogDescription.displayName =
  AlertDialogPrimitive.Description.displayName

const AlertDialogAction = React.forwardRef<
  React.ElementRef<typeof AlertDialogPrimitive.Action>,
  React.ComponentPropsWithoutRef<typeof AlertDialogPrimitive.Action>
>(({ className, ...props }, ref) => (
  <AlertDialogPrimitive.Action
    ref={ref}
    className={cn(buttonVariants(), className)}
    {...props}
  />
))
AlertDialogAction.displayName = AlertDialogPrimitive.Action.displayName

const AlertDialogCancel = React.forwardRef<
  React.ElementRef<typeof AlertDialogPrimitive.Cancel>,
  React.ComponentPropsWithoutRef<typeof AlertDialogPrimitive.Cancel>
>(({ className, ...props }, ref) => (
  <AlertDialogPrimitive.Cancel
    ref={ref}
    className={cn(
      buttonVariants({ variant: "outline" }),
      "mt-2 sm:mt-0",
      className
    )}
    {...props}
  />
))
AlertDialogCancel.displayName = AlertDialogPrimitive.Cancel.displayName

export {
  AlertDialog,
  AlertDialogPortal,
  AlertDialogOverlay,
  AlertDialogTrigger,
  AlertDialogContent,
  AlertDialogHeader,
  AlertDialogFooter,
  AlertDialogTitle,
  AlertDialogDescription,
  AlertDialogAction,
  AlertDialogCancel,
}
```

## File: dkl-microapp-2-main/components/ui/alert.tsx
```typescript
import * as React from "react"
import { cva, type VariantProps } from "class-variance-authority"

import { cn } from "@/lib/utils"

const alertVariants = cva(
  "relative w-full rounded-lg border p-4 [&>svg~*]:pl-7 [&>svg+div]:translate-y-[-3px] [&>svg]:absolute [&>svg]:left-4 [&>svg]:top-4 [&>svg]:text-foreground",
  {
    variants: {
      variant: {
        default: "bg-background text-foreground",
        destructive:
          "border-destructive/50 text-destructive dark:border-destructive [&>svg]:text-destructive",
      },
    },
    defaultVariants: {
      variant: "default",
    },
  }
)

const Alert = React.forwardRef<
  HTMLDivElement,
  React.HTMLAttributes<HTMLDivElement> & VariantProps<typeof alertVariants>
>(({ className, variant, ...props }, ref) => (
  <div
    ref={ref}
    role="alert"
    className={cn(alertVariants({ variant }), className)}
    {...props}
  />
))
Alert.displayName = "Alert"

const AlertTitle = React.forwardRef<
  HTMLParagraphElement,
  React.HTMLAttributes<HTMLHeadingElement>
>(({ className, ...props }, ref) => (
  <h5
    ref={ref}
    className={cn("mb-1 font-medium leading-none tracking-tight", className)}
    {...props}
  />
))
AlertTitle.displayName = "AlertTitle"

const AlertDescription = React.forwardRef<
  HTMLParagraphElement,
  React.HTMLAttributes<HTMLParagraphElement>
>(({ className, ...props }, ref) => (
  <div
    ref={ref}
    className={cn("text-sm [&_p]:leading-relaxed", className)}
    {...props}
  />
))
AlertDescription.displayName = "AlertDescription"

export { Alert, AlertTitle, AlertDescription }
```

## File: dkl-microapp-2-main/components/ui/badge.tsx
```typescript
import type * as React from "react"
import { cva, type VariantProps } from "class-variance-authority"
import { cn } from "@/lib/utils"

const badgeVariants = cva(
  "inline-flex items-center rounded-full border px-2.5 py-0.5 text-xs font-semibold transition-colors focus:outline-none focus:ring-2 focus:ring-ring focus:ring-offset-2",
  {
    variants: {
      variant: {
        default: "border-transparent bg-primary text-primary-foreground hover:bg-primary/80",
        secondary: "border-transparent bg-secondary text-secondary-foreground hover:bg-secondary/80",
        destructive: "border-transparent bg-destructive text-destructive-foreground hover:bg-destructive/80",
        outline: "text-foreground",
      },
    },
    defaultVariants: {
      variant: "default",
    },
  },
)

export interface BadgeProps extends React.HTMLAttributes<HTMLDivElement>, VariantProps<typeof badgeVariants> {}

function Badge({ className, variant, ...props }: BadgeProps) {
  return <div className={cn(badgeVariants({ variant }), className)} {...props} />
}

export { Badge, badgeVariants }
```

## File: dkl-microapp-2-main/components/ui/button.tsx
```typescript
import * as React from "react"
import { Slot } from "@radix-ui/react-slot"
import { cva, type VariantProps } from "class-variance-authority"

import { cn } from "@/lib/utils"

const buttonVariants = cva(
  "inline-flex items-center justify-center gap-2 whitespace-nowrap rounded-md text-sm font-medium ring-offset-background transition-colors focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2 disabled:pointer-events-none disabled:opacity-50 [&_svg]:pointer-events-none [&_svg]:size-4 [&_svg]:shrink-0",
  {
    variants: {
      variant: {
        default: "bg-primary text-primary-foreground hover:bg-primary/90",
        destructive:
          "bg-destructive text-destructive-foreground hover:bg-destructive/90",
        outline:
          "border border-input bg-background hover:bg-accent hover:text-accent-foreground",
        secondary:
          "bg-secondary text-secondary-foreground hover:bg-secondary/80",
        ghost: "hover:bg-accent hover:text-accent-foreground",
        link: "text-primary underline-offset-4 hover:underline",
      },
      size: {
        default: "h-10 px-4 py-2",
        sm: "h-9 rounded-md px-3",
        lg: "h-11 rounded-md px-8",
        icon: "h-10 w-10",
      },
    },
    defaultVariants: {
      variant: "default",
      size: "default",
    },
  }
)

export interface ButtonProps
  extends React.ButtonHTMLAttributes<HTMLButtonElement>,
    VariantProps<typeof buttonVariants> {
  asChild?: boolean
}

const Button = React.forwardRef<HTMLButtonElement, ButtonProps>(
  ({ className, variant, size, asChild = false, ...props }, ref) => {
    const Comp = asChild ? Slot : "button"
    return (
      <Comp
        className={cn(buttonVariants({ variant, size, className }))}
        ref={ref}
        {...props}
      />
    )
  }
)
Button.displayName = "Button"

export { Button, buttonVariants }
```

## File: dkl-microapp-2-main/components/ui/card.tsx
```typescript
import * as React from "react"

import { cn } from "@/lib/utils"

const Card = React.forwardRef<
  HTMLDivElement,
  React.HTMLAttributes<HTMLDivElement>
>(({ className, ...props }, ref) => (
  <div
    ref={ref}
    className={cn(
      "rounded-lg border bg-card text-card-foreground shadow-sm",
      className
    )}
    {...props}
  />
))
Card.displayName = "Card"

const CardHeader = React.forwardRef<
  HTMLDivElement,
  React.HTMLAttributes<HTMLDivElement>
>(({ className, ...props }, ref) => (
  <div
    ref={ref}
    className={cn("flex flex-col space-y-1.5 p-6", className)}
    {...props}
  />
))
CardHeader.displayName = "CardHeader"

const CardTitle = React.forwardRef<
  HTMLDivElement,
  React.HTMLAttributes<HTMLDivElement>
>(({ className, ...props }, ref) => (
  <div
    ref={ref}
    className={cn(
      "text-2xl font-semibold leading-none tracking-tight",
      className
    )}
    {...props}
  />
))
CardTitle.displayName = "CardTitle"

const CardDescription = React.forwardRef<
  HTMLDivElement,
  React.HTMLAttributes<HTMLDivElement>
>(({ className, ...props }, ref) => (
  <div
    ref={ref}
    className={cn("text-sm text-muted-foreground", className)}
    {...props}
  />
))
CardDescription.displayName = "CardDescription"

const CardContent = React.forwardRef<
  HTMLDivElement,
  React.HTMLAttributes<HTMLDivElement>
>(({ className, ...props }, ref) => (
  <div ref={ref} className={cn("p-6 pt-0", className)} {...props} />
))
CardContent.displayName = "CardContent"

const CardFooter = React.forwardRef<
  HTMLDivElement,
  React.HTMLAttributes<HTMLDivElement>
>(({ className, ...props }, ref) => (
  <div
    ref={ref}
    className={cn("flex items-center p-6 pt-0", className)}
    {...props}
  />
))
CardFooter.displayName = "CardFooter"

export { Card, CardHeader, CardFooter, CardTitle, CardDescription, CardContent }
```

## File: dkl-microapp-2-main/components/ui/chart.tsx
```typescript
"use client"

import * as React from "react"
import * as RechartsPrimitive from "recharts"

import { cn } from "@/lib/utils"

// Format: { THEME_NAME: CSS_SELECTOR }
const THEMES = { light: "", dark: ".dark" } as const

export type ChartConfig = {
  [k in string]: {
    label?: React.ReactNode
    icon?: React.ComponentType
  } & (
    | { color?: string; theme?: never }
    | { color?: never; theme: Record<keyof typeof THEMES, string> }
  )
}

type ChartContextProps = {
  config: ChartConfig
}

const ChartContext = React.createContext<ChartContextProps | null>(null)

function useChart() {
  const context = React.useContext(ChartContext)

  if (!context) {
    throw new Error("useChart must be used within a <ChartContainer />")
  }

  return context
}

const ChartContainer = React.forwardRef<
  HTMLDivElement,
  React.ComponentProps<"div"> & {
    config: ChartConfig
    children: React.ComponentProps<
      typeof RechartsPrimitive.ResponsiveContainer
    >["children"]
  }
>(({ id, className, children, config, ...props }, ref) => {
  const uniqueId = React.useId()
  const chartId = `chart-${id || uniqueId.replace(/:/g, "")}`

  return (
    <ChartContext.Provider value={{ config }}>
      <div
        data-chart={chartId}
        ref={ref}
        className={cn(
          "flex aspect-video justify-center text-xs [&_.recharts-cartesian-axis-tick_text]:fill-muted-foreground [&_.recharts-cartesian-grid_line[stroke='#ccc']]:stroke-border/50 [&_.recharts-curve.recharts-tooltip-cursor]:stroke-border [&_.recharts-dot[stroke='#fff']]:stroke-transparent [&_.recharts-layer]:outline-none [&_.recharts-polar-grid_[stroke='#ccc']]:stroke-border [&_.recharts-radial-bar-background-sector]:fill-muted [&_.recharts-rectangle.recharts-tooltip-cursor]:fill-muted [&_.recharts-reference-line_[stroke='#ccc']]:stroke-border [&_.recharts-sector[stroke='#fff']]:stroke-transparent [&_.recharts-sector]:outline-none [&_.recharts-surface]:outline-none",
          className
        )}
        {...props}
      >
        <ChartStyle id={chartId} config={config} />
        <RechartsPrimitive.ResponsiveContainer>
          {children}
        </RechartsPrimitive.ResponsiveContainer>
      </div>
    </ChartContext.Provider>
  )
})
ChartContainer.displayName = "Chart"

const ChartStyle = ({ id, config }: { id: string; config: ChartConfig }) => {
  const colorConfig = Object.entries(config).filter(
    ([_, config]) => config.theme || config.color
  )

  if (!colorConfig.length) {
    return null
  }

  return (
    <style
      dangerouslySetInnerHTML={{
        __html: Object.entries(THEMES)
          .map(
            ([theme, prefix]) => `
${prefix} [data-chart=${id}] {
${colorConfig
  .map(([key, itemConfig]) => {
    const color =
      itemConfig.theme?.[theme as keyof typeof itemConfig.theme] ||
      itemConfig.color
    return color ? `  --color-${key}: ${color};` : null
  })
  .join("\n")}
}
`
          )
          .join("\n"),
      }}
    />
  )
}

const ChartTooltip = RechartsPrimitive.Tooltip

const ChartTooltipContent = React.forwardRef<
  HTMLDivElement,
  React.ComponentProps<typeof RechartsPrimitive.Tooltip> &
    React.ComponentProps<"div"> & {
      hideLabel?: boolean
      hideIndicator?: boolean
      indicator?: "line" | "dot" | "dashed"
      nameKey?: string
      labelKey?: string
    }
>(
  (
    {
      active,
      payload,
      className,
      indicator = "dot",
      hideLabel = false,
      hideIndicator = false,
      label,
      labelFormatter,
      labelClassName,
      formatter,
      color,
      nameKey,
      labelKey,
    },
    ref
  ) => {
    const { config } = useChart()

    const tooltipLabel = React.useMemo(() => {
      if (hideLabel || !payload?.length) {
        return null
      }

      const [item] = payload
      const key = `${labelKey || item.dataKey || item.name || "value"}`
      const itemConfig = getPayloadConfigFromPayload(config, item, key)
      const value =
        !labelKey && typeof label === "string"
          ? config[label as keyof typeof config]?.label || label
          : itemConfig?.label

      if (labelFormatter) {
        return (
          <div className={cn("font-medium", labelClassName)}>
            {labelFormatter(value, payload)}
          </div>
        )
      }

      if (!value) {
        return null
      }

      return <div className={cn("font-medium", labelClassName)}>{value}</div>
    }, [
      label,
      labelFormatter,
      payload,
      hideLabel,
      labelClassName,
      config,
      labelKey,
    ])

    if (!active || !payload?.length) {
      return null
    }

    const nestLabel = payload.length === 1 && indicator !== "dot"

    return (
      <div
        ref={ref}
        className={cn(
          "grid min-w-[8rem] items-start gap-1.5 rounded-lg border border-border/50 bg-background px-2.5 py-1.5 text-xs shadow-xl",
          className
        )}
      >
        {!nestLabel ? tooltipLabel : null}
        <div className="grid gap-1.5">
          {payload.map((item, index) => {
            const key = `${nameKey || item.name || item.dataKey || "value"}`
            const itemConfig = getPayloadConfigFromPayload(config, item, key)
            const indicatorColor = color || item.payload.fill || item.color

            return (
              <div
                key={item.dataKey}
                className={cn(
                  "flex w-full flex-wrap items-stretch gap-2 [&>svg]:h-2.5 [&>svg]:w-2.5 [&>svg]:text-muted-foreground",
                  indicator === "dot" && "items-center"
                )}
              >
                {formatter && item?.value !== undefined && item.name ? (
                  formatter(item.value, item.name, item, index, item.payload)
                ) : (
                  <>
                    {itemConfig?.icon ? (
                      <itemConfig.icon />
                    ) : (
                      !hideIndicator && (
                        <div
                          className={cn(
                            "shrink-0 rounded-[2px] border-[--color-border] bg-[--color-bg]",
                            {
                              "h-2.5 w-2.5": indicator === "dot",
                              "w-1": indicator === "line",
                              "w-0 border-[1.5px] border-dashed bg-transparent":
                                indicator === "dashed",
                              "my-0.5": nestLabel && indicator === "dashed",
                            }
                          )}
                          style={
                            {
                              "--color-bg": indicatorColor,
                              "--color-border": indicatorColor,
                            } as React.CSSProperties
                          }
                        />
                      )
                    )}
                    <div
                      className={cn(
                        "flex flex-1 justify-between leading-none",
                        nestLabel ? "items-end" : "items-center"
                      )}
                    >
                      <div className="grid gap-1.5">
                        {nestLabel ? tooltipLabel : null}
                        <span className="text-muted-foreground">
                          {itemConfig?.label || item.name}
                        </span>
                      </div>
                      {item.value && (
                        <span className="font-mono font-medium tabular-nums text-foreground">
                          {item.value.toLocaleString()}
                        </span>
                      )}
                    </div>
                  </>
                )}
              </div>
            )
          })}
        </div>
      </div>
    )
  }
)
ChartTooltipContent.displayName = "ChartTooltip"

const ChartLegend = RechartsPrimitive.Legend

const ChartLegendContent = React.forwardRef<
  HTMLDivElement,
  React.ComponentProps<"div"> &
    Pick<RechartsPrimitive.LegendProps, "payload" | "verticalAlign"> & {
      hideIcon?: boolean
      nameKey?: string
    }
>(
  (
    { className, hideIcon = false, payload, verticalAlign = "bottom", nameKey },
    ref
  ) => {
    const { config } = useChart()

    if (!payload?.length) {
      return null
    }

    return (
      <div
        ref={ref}
        className={cn(
          "flex items-center justify-center gap-4",
          verticalAlign === "top" ? "pb-3" : "pt-3",
          className
        )}
      >
        {payload.map((item) => {
          const key = `${nameKey || item.dataKey || "value"}`
          const itemConfig = getPayloadConfigFromPayload(config, item, key)

          return (
            <div
              key={item.value}
              className={cn(
                "flex items-center gap-1.5 [&>svg]:h-3 [&>svg]:w-3 [&>svg]:text-muted-foreground"
              )}
            >
              {itemConfig?.icon && !hideIcon ? (
                <itemConfig.icon />
              ) : (
                <div
                  className="h-2 w-2 shrink-0 rounded-[2px]"
                  style={{
                    backgroundColor: item.color,
                  }}
                />
              )}
              {itemConfig?.label}
            </div>
          )
        })}
      </div>
    )
  }
)
ChartLegendContent.displayName = "ChartLegend"

// Helper to extract item config from a payload.
function getPayloadConfigFromPayload(
  config: ChartConfig,
  payload: unknown,
  key: string
) {
  if (typeof payload !== "object" || payload === null) {
    return undefined
  }

  const payloadPayload =
    "payload" in payload &&
    typeof payload.payload === "object" &&
    payload.payload !== null
      ? payload.payload
      : undefined

  let configLabelKey: string = key

  if (
    key in payload &&
    typeof payload[key as keyof typeof payload] === "string"
  ) {
    configLabelKey = payload[key as keyof typeof payload] as string
  } else if (
    payloadPayload &&
    key in payloadPayload &&
    typeof payloadPayload[key as keyof typeof payloadPayload] === "string"
  ) {
    configLabelKey = payloadPayload[
      key as keyof typeof payloadPayload
    ] as string
  }

  return configLabelKey in config
    ? config[configLabelKey]
    : config[key as keyof typeof config]
}

export {
  ChartContainer,
  ChartTooltip,
  ChartTooltipContent,
  ChartLegend,
  ChartLegendContent,
  ChartStyle,
}
```

## File: dkl-microapp-2-main/components/ui/checkbox.tsx
```typescript
"use client"

import * as React from "react"
import * as CheckboxPrimitive from "@radix-ui/react-checkbox"
import { Check } from "lucide-react"

import { cn } from "@/lib/utils"

const Checkbox = React.forwardRef<
  React.ElementRef<typeof CheckboxPrimitive.Root>,
  React.ComponentPropsWithoutRef<typeof CheckboxPrimitive.Root>
>(({ className, ...props }, ref) => (
  <CheckboxPrimitive.Root
    ref={ref}
    className={cn(
      "peer h-4 w-4 shrink-0 rounded-sm border border-primary ring-offset-background focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2 disabled:cursor-not-allowed disabled:opacity-50",
      "data-[state=checked]:bg-primary data-[state=checked]:text-primary-foreground",
      className,
    )}
    {...props}
  >
    <CheckboxPrimitive.Indicator className={cn("flex items-center justify-center text-current")}>
      <Check className="h-4 w-4" />
    </CheckboxPrimitive.Indicator>
  </CheckboxPrimitive.Root>
))
Checkbox.displayName = CheckboxPrimitive.Root.displayName

export { Checkbox }
```

## File: dkl-microapp-2-main/components/ui/command.tsx
```typescript
"use client"

import * as React from "react"
import { type DialogProps } from "@radix-ui/react-dialog"
import { Command as CommandPrimitive } from "cmdk"
import { Search } from "lucide-react"

import { cn } from "@/lib/utils"
import { Dialog, DialogContent } from "@/components/ui/dialog"

const Command = React.forwardRef<
  React.ElementRef<typeof CommandPrimitive>,
  React.ComponentPropsWithoutRef<typeof CommandPrimitive>
>(({ className, ...props }, ref) => (
  <CommandPrimitive
    ref={ref}
    className={cn(
      "flex h-full w-full flex-col overflow-hidden rounded-md bg-popover text-popover-foreground",
      className
    )}
    {...props}
  />
))
Command.displayName = CommandPrimitive.displayName

const CommandDialog = ({ children, ...props }: DialogProps) => {
  return (
    <Dialog {...props}>
      <DialogContent className="overflow-hidden p-0 shadow-lg">
        <Command className="[&_[cmdk-group-heading]]:px-2 [&_[cmdk-group-heading]]:font-medium [&_[cmdk-group-heading]]:text-muted-foreground [&_[cmdk-group]:not([hidden])_~[cmdk-group]]:pt-0 [&_[cmdk-group]]:px-2 [&_[cmdk-input-wrapper]_svg]:h-5 [&_[cmdk-input-wrapper]_svg]:w-5 [&_[cmdk-input]]:h-12 [&_[cmdk-item]]:px-2 [&_[cmdk-item]]:py-3 [&_[cmdk-item]_svg]:h-5 [&_[cmdk-item]_svg]:w-5">
          {children}
        </Command>
      </DialogContent>
    </Dialog>
  )
}

const CommandInput = React.forwardRef<
  React.ElementRef<typeof CommandPrimitive.Input>,
  React.ComponentPropsWithoutRef<typeof CommandPrimitive.Input>
>(({ className, ...props }, ref) => (
  <div className="flex items-center border-b px-3" cmdk-input-wrapper="">
    <Search className="mr-2 h-4 w-4 shrink-0 opacity-50" />
    <CommandPrimitive.Input
      ref={ref}
      className={cn(
        "flex h-11 w-full rounded-md bg-transparent py-3 text-sm outline-none placeholder:text-muted-foreground disabled:cursor-not-allowed disabled:opacity-50",
        className
      )}
      {...props}
    />
  </div>
))

CommandInput.displayName = CommandPrimitive.Input.displayName

const CommandList = React.forwardRef<
  React.ElementRef<typeof CommandPrimitive.List>,
  React.ComponentPropsWithoutRef<typeof CommandPrimitive.List>
>(({ className, ...props }, ref) => (
  <CommandPrimitive.List
    ref={ref}
    className={cn("max-h-[300px] overflow-y-auto overflow-x-hidden", className)}
    {...props}
  />
))

CommandList.displayName = CommandPrimitive.List.displayName

const CommandEmpty = React.forwardRef<
  React.ElementRef<typeof CommandPrimitive.Empty>,
  React.ComponentPropsWithoutRef<typeof CommandPrimitive.Empty>
>((props, ref) => (
  <CommandPrimitive.Empty
    ref={ref}
    className="py-6 text-center text-sm"
    {...props}
  />
))

CommandEmpty.displayName = CommandPrimitive.Empty.displayName

const CommandGroup = React.forwardRef<
  React.ElementRef<typeof CommandPrimitive.Group>,
  React.ComponentPropsWithoutRef<typeof CommandPrimitive.Group>
>(({ className, ...props }, ref) => (
  <CommandPrimitive.Group
    ref={ref}
    className={cn(
      "overflow-hidden p-1 text-foreground [&_[cmdk-group-heading]]:px-2 [&_[cmdk-group-heading]]:py-1.5 [&_[cmdk-group-heading]]:text-xs [&_[cmdk-group-heading]]:font-medium [&_[cmdk-group-heading]]:text-muted-foreground",
      className
    )}
    {...props}
  />
))

CommandGroup.displayName = CommandPrimitive.Group.displayName

const CommandSeparator = React.forwardRef<
  React.ElementRef<typeof CommandPrimitive.Separator>,
  React.ComponentPropsWithoutRef<typeof CommandPrimitive.Separator>
>(({ className, ...props }, ref) => (
  <CommandPrimitive.Separator
    ref={ref}
    className={cn("-mx-1 h-px bg-border", className)}
    {...props}
  />
))
CommandSeparator.displayName = CommandPrimitive.Separator.displayName

const CommandItem = React.forwardRef<
  React.ElementRef<typeof CommandPrimitive.Item>,
  React.ComponentPropsWithoutRef<typeof CommandPrimitive.Item>
>(({ className, ...props }, ref) => (
  <CommandPrimitive.Item
    ref={ref}
    className={cn(
      "relative flex cursor-default gap-2 select-none items-center rounded-sm px-2 py-1.5 text-sm outline-none data-[disabled=true]:pointer-events-none data-[selected='true']:bg-accent data-[selected=true]:text-accent-foreground data-[disabled=true]:opacity-50 [&_svg]:pointer-events-none [&_svg]:size-4 [&_svg]:shrink-0",
      className
    )}
    {...props}
  />
))

CommandItem.displayName = CommandPrimitive.Item.displayName

const CommandShortcut = ({
  className,
  ...props
}: React.HTMLAttributes<HTMLSpanElement>) => {
  return (
    <span
      className={cn(
        "ml-auto text-xs tracking-widest text-muted-foreground",
        className
      )}
      {...props}
    />
  )
}
CommandShortcut.displayName = "CommandShortcut"

export {
  Command,
  CommandDialog,
  CommandInput,
  CommandList,
  CommandEmpty,
  CommandGroup,
  CommandItem,
  CommandShortcut,
  CommandSeparator,
}
```

## File: dkl-microapp-2-main/components/ui/data-table-column-header.tsx
```typescript
"use client"

import type React from "react"

import type { Column } from "@tanstack/react-table"
import { cn } from "@/lib/utils"
import { Button } from "@/components/ui/button"
import {
  DropdownMenu,
  DropdownMenuContent,
  DropdownMenuItem,
  DropdownMenuSeparator,
  DropdownMenuTrigger,
} from "@/components/ui/dropdown-menu"
import { ArrowDown, ArrowUp, ChevronsUpDown, EyeOff } from "lucide-react"

interface DataTableColumnHeaderProps<TData, TValue> extends React.HTMLAttributes<HTMLDivElement> {
  column: Column<TData, TValue>
  title: string
}

export function DataTableColumnHeader<TData, TValue>({
  column,
  title,
  className,
}: DataTableColumnHeaderProps<TData, TValue>) {
  if (!column.getCanSort() && !column.getCanHide()) {
    return <div className={cn(className)}>{title}</div>
  }

  return (
    <div className={cn("flex items-center space-x-2", className)}>
      <DropdownMenu>
        <DropdownMenuTrigger asChild>
          <Button variant="ghost" size="sm" className="-ml-3 h-8 data-[state=open]:bg-accent text-xs">
            <span>{title}</span>
            {column.getCanSort() && column.getIsSorted() === "desc" ? (
              <ArrowDown className="ml-2 h-3 w-3" />
            ) : column.getIsSorted() === "asc" ? (
              <ArrowUp className="ml-2 h-3 w-3" />
            ) : (
              <ChevronsUpDown className="ml-2 h-3 w-3" />
            )}
          </Button>
        </DropdownMenuTrigger>
        <DropdownMenuContent align="start">
          {column.getCanSort() && (
            <>
              <DropdownMenuItem onClick={() => column.toggleSorting(false)}>
                <ArrowUp className="mr-2 h-3.5 w-3.5 text-muted-foreground/70" />
                Asc
              </DropdownMenuItem>
              <DropdownMenuItem onClick={() => column.toggleSorting(true)}>
                <ArrowDown className="mr-2 h-3.5 w-3.5 text-muted-foreground/70" />
                Desc
              </DropdownMenuItem>
            </>
          )}
          {column.getCanSort() && column.getCanHide() && <DropdownMenuSeparator />}
          {column.getCanHide() && (
            <DropdownMenuItem onClick={() => column.toggleVisibility(false)}>
              <EyeOff className="mr-2 h-3.5 w-3.5 text-muted-foreground/70" />
              Hide
            </DropdownMenuItem>
          )}
        </DropdownMenuContent>
      </DropdownMenu>
    </div>
  )
}
```

## File: dkl-microapp-2-main/components/ui/data-table-pagination.tsx
```typescript
"use client"

import type { Table } from "@tanstack/react-table"
import { Button } from "@/components/ui/button"
import { Select, SelectContent, SelectItem, SelectTrigger, SelectValue } from "@/components/ui/select"
import { ChevronLeft, ChevronRight, ChevronsLeft, ChevronsRight } from "lucide-react"

interface DataTablePaginationProps<TData> {
  table: Table<TData>
}

export function DataTablePagination<TData>({ table }: DataTablePaginationProps<TData>) {
  return (
    <div className="flex items-center justify-between px-2 py-2 border-t">
      <div className="flex-1 text-sm text-muted-foreground">
        {table.getFilteredSelectedRowModel().rows.length} of {table.getFilteredRowModel().rows.length} row(s) selected.
      </div>
      <div className="flex items-center space-x-6 lg:space-x-8">
        <div className="flex items-center space-x-2">
          <p className="text-sm font-medium">Rows per page</p>
          <Select
            value={`${table.getState().pagination.pageSize}`}
            onValueChange={(value) => {
              table.setPageSize(Number(value))
            }}
          >
            <SelectTrigger className="h-8 w-[70px]">
              <SelectValue placeholder={table.getState().pagination.pageSize} />
            </SelectTrigger>
            <SelectContent side="top">
              {[10, 20, 30, 40, 50, 100].map((pageSize) => (
                <SelectItem key={pageSize} value={`${pageSize}`}>
                  {pageSize}
                </SelectItem>
              ))}
            </SelectContent>
          </Select>
        </div>
        <div className="flex w-[100px] items-center justify-center text-sm font-medium">
          Page {table.getState().pagination.pageIndex + 1} of {table.getPageCount()}
        </div>
        <div className="flex items-center space-x-2">
          <Button
            variant="outline"
            className="hidden h-8 w-8 p-0 lg:flex"
            onClick={() => table.setPageIndex(0)}
            disabled={!table.getCanPreviousPage()}
          >
            <span className="sr-only">Go to first page</span>
            <ChevronsLeft className="h-4 w-4" />
          </Button>
          <Button
            variant="outline"
            className="h-8 w-8 p-0"
            onClick={() => table.previousPage()}
            disabled={!table.getCanPreviousPage()}
          >
            <span className="sr-only">Go to previous page</span>
            <ChevronLeft className="h-4 w-4" />
          </Button>
          <Button
            variant="outline"
            className="h-8 w-8 p-0"
            onClick={() => table.nextPage()}
            disabled={!table.getCanNextPage()}
          >
            <span className="sr-only">Go to next page</span>
            <ChevronRight className="h-4 w-4" />
          </Button>
          <Button
            variant="outline"
            className="hidden h-8 w-8 p-0 lg:flex"
            onClick={() => table.setPageIndex(table.getPageCount() - 1)}
            disabled={!table.getCanNextPage()}
          >
            <span className="sr-only">Go to last page</span>
            <ChevronsRight className="h-4 w-4" />
          </Button>
        </div>
      </div>
    </div>
  )
}
```

## File: dkl-microapp-2-main/components/ui/data-table-toolbar.tsx
```typescript
"use client"

import type { Table } from "@tanstack/react-table"
import { Input } from "@/components/ui/input"
import { Button } from "@/components/ui/button"
import {
  DropdownMenu,
  DropdownMenuCheckboxItem,
  DropdownMenuContent,
  DropdownMenuLabel,
  DropdownMenuSeparator,
  DropdownMenuTrigger,
} from "@/components/ui/dropdown-menu"
import { SlidersHorizontal, X } from "lucide-react"

interface DataTableToolbarProps<TData> {
  table: Table<TData>
  globalFilter?: string
  setGlobalFilter?: (value: string) => void
  // Add props for faceted filters if needed, e.g., filterComponents?: React.ReactNode[]
}

export function DataTableToolbar<TData>({ table, globalFilter, setGlobalFilter }: DataTableToolbarProps<TData>) {
  const isFiltered = table.getState().columnFilters.length > 0

  return (
    <div className="flex items-center justify-between py-2">
      <div className="flex flex-1 items-center space-x-2">
        {setGlobalFilter && (
          <Input
            placeholder="Search all columns..."
            value={globalFilter ?? ""}
            onChange={(event) => setGlobalFilter(event.target.value)}
            className="h-8 w-[150px] lg:w-[250px]"
          />
        )}
        {/* Placeholder for Faceted Filter Buttons */}
        {/* {table.getAllColumns().map(column => {
          if (column.getCanFilter()) {
            // Render faceted filter UIs here based on column meta or type
          }
          return null;
        })} */}
        {isFiltered && (
          <Button variant="ghost" onClick={() => table.resetColumnFilters()} className="h-8 px-2 lg:px-3">
            Reset
            <X className="ml-2 h-4 w-4" />
          </Button>
        )}
      </div>
      <div className="flex items-center space-x-2">
        {/* Placeholder for Advanced/Command Filters */}
        {/* <Button variant="outline" size="sm" className="h-8">Advanced Filters</Button> */}
        <DropdownMenu>
          <DropdownMenuTrigger asChild>
            <Button variant="outline" size="sm" className="ml-auto hidden h-8 lg:flex">
              <SlidersHorizontal className="mr-2 h-4 w-4" />
              View
            </Button>
          </DropdownMenuTrigger>
          <DropdownMenuContent align="end" className="w-[150px]">
            <DropdownMenuLabel>Toggle columns</DropdownMenuLabel>
            <DropdownMenuSeparator />
            {table
              .getAllColumns()
              .filter((column) => typeof column.accessorFn !== "undefined" && column.getCanHide())
              .map((column) => {
                return (
                  <DropdownMenuCheckboxItem
                    key={column.id}
                    className="capitalize"
                    checked={column.getIsVisible()}
                    onCheckedChange={(value) => column.toggleVisibility(!!value)}
                  >
                    {column.id}
                  </DropdownMenuCheckboxItem>
                )
              })}
          </DropdownMenuContent>
        </DropdownMenu>
      </div>
    </div>
  )
}
```

## File: dkl-microapp-2-main/components/ui/data-table.tsx
```typescript
"use client"

import * as React from "react"
import {
  type ColumnDef,
  type ColumnFiltersState,
  type SortingState,
  type VisibilityState,
  type RowSelectionState,
  flexRender,
  getCoreRowModel,
  getFacetedRowModel,
  getFacetedUniqueValues,
  getFilteredRowModel,
  getPaginationRowModel,
  getSortedRowModel,
  useReactTable,
} from "@tanstack/react-table"

import { Table, TableBody, TableCell, TableHead, TableHeader, TableRow } from "@/components/ui/table"
import { DataTablePagination } from "./data-table-pagination"
import { DataTableToolbar } from "./data-table-toolbar" // We'll create this

interface DataTableProps<TData, TValue> {
  columns: ColumnDef<TData, TValue>[]
  data: TData[]
  loading?: boolean
  // Add props for bulk actions if needed
  renderBulkActions?: (selectedRows: TData[]) => React.ReactNode
}

export function DataTable<TData, TValue>({
  columns,
  data,
  loading = false,
  renderBulkActions,
}: DataTableProps<TData, TValue>) {
  const [rowSelection, setRowSelection] = React.useState<RowSelectionState>({})
  const [columnVisibility, setColumnVisibility] = React.useState<VisibilityState>({})
  const [columnFilters, setColumnFilters] = React.useState<ColumnFiltersState>([])
  const [sorting, setSorting] = React.useState<SortingState>([])
  const [globalFilter, setGlobalFilter] = React.useState("")

  const table = useReactTable({
    data,
    columns,
    state: {
      sorting,
      columnVisibility,
      rowSelection,
      columnFilters,
      globalFilter,
    },
    enableRowSelection: true,
    onRowSelectionChange: setRowSelection,
    onSortingChange: setSorting,
    onColumnFiltersChange: setColumnFilters,
    onColumnVisibilityChange: setColumnVisibility,
    onGlobalFilterChange: setGlobalFilter,
    getCoreRowModel: getCoreRowModel(),
    getFilteredRowModel: getFilteredRowModel(),
    getPaginationRowModel: getPaginationRowModel(),
    getSortedRowModel: getSortedRowModel(),
    getFacetedRowModel: getFacetedRowModel(),
    getFacetedUniqueValues: getFacetedUniqueValues(),
    manualPagination: false, // Set to true if using server-side pagination
  })

  const selectedRowsData = table.getFilteredSelectedRowModel().rows.map((row) => row.original)

  return (
    <div className="space-y-2">
      <DataTableToolbar table={table} globalFilter={globalFilter} setGlobalFilter={setGlobalFilter} />
      <div className="rounded-md border bg-card">
        <Table>
          <TableHeader>
            {table.getHeaderGroups().map((headerGroup) => (
              <TableRow key={headerGroup.id}>
                {headerGroup.headers.map((header) => {
                  return (
                    <TableHead key={header.id} colSpan={header.colSpan} className="text-xs">
                      {header.isPlaceholder ? null : flexRender(header.column.columnDef.header, header.getContext())}
                    </TableHead>
                  )
                })}
              </TableRow>
            ))}
          </TableHeader>
          <TableBody>
            {loading ? (
              <TableRow>
                <TableCell colSpan={columns.length} className="h-24 text-center text-xs">
                  Loading...
                </TableCell>
              </TableRow>
            ) : table.getRowModel().rows?.length ? (
              table.getRowModel().rows.map((row) => (
                <TableRow key={row.id} data-state={row.getIsSelected() && "selected"}>
                  {row.getVisibleCells().map((cell) => (
                    <TableCell key={cell.id} className="text-xs py-2">
                      {flexRender(cell.column.columnDef.cell, cell.getContext())}
                    </TableCell>
                  ))}
                </TableRow>
              ))
            ) : (
              <TableRow>
                <TableCell colSpan={columns.length} className="h-24 text-center text-xs">
                  No results.
                </TableCell>
              </TableRow>
            )}
          </TableBody>
        </Table>
      </div>
      <DataTablePagination table={table} />
      {renderBulkActions && selectedRowsData.length > 0 && (
        <div className="fixed bottom-4 left-1/2 -translate-x-1/2 z-50">
          <div className="bg-card border shadow-lg rounded-md p-2 flex items-center space-x-2">
            <span className="text-sm font-medium px-2">{selectedRowsData.length} selected</span>
            {renderBulkActions(selectedRowsData)}
          </div>
        </div>
      )}
    </div>
  )
}
```

## File: dkl-microapp-2-main/components/ui/dialog.tsx
```typescript
"use client"

import * as React from "react"
import * as DialogPrimitive from "@radix-ui/react-dialog"
import { X } from "lucide-react"

import { cn } from "@/lib/utils"

const Dialog = DialogPrimitive.Root

const DialogTrigger = DialogPrimitive.Trigger

const DialogPortal = DialogPrimitive.Portal

const DialogClose = DialogPrimitive.Close

const DialogOverlay = React.forwardRef<
  React.ElementRef<typeof DialogPrimitive.Overlay>,
  React.ComponentPropsWithoutRef<typeof DialogPrimitive.Overlay>
>(({ className, ...props }, ref) => (
  <DialogPrimitive.Overlay
    ref={ref}
    className={cn(
      "fixed inset-0 z-50 bg-black/80 data-[state=open]:animate-in data-[state=closed]:animate-out data-[state=closed]:fade-out-0 data-[state=open]:fade-in-0",
      className,
    )}
    {...props}
  />
))
DialogOverlay.displayName = DialogPrimitive.Overlay.displayName

const DialogContent = React.forwardRef<
  React.ElementRef<typeof DialogPrimitive.Content>,
  React.ComponentPropsWithoutRef<typeof DialogPrimitive.Content>
>(({ className, children, ...props }, ref) => (
  <DialogPortal>
    <DialogOverlay />
    <DialogPrimitive.Content
      ref={ref}
      className={cn(
        "fixed left-[50%] top-[50%] z-50 grid w-full max-w-lg translate-x-[-50%] translate-y-[-50%] gap-4 border bg-background p-6 shadow-lg duration-200 data-[state=open]:animate-in data-[state=closed]:animate-out data-[state=closed]:fade-out-0 data-[state=open]:fade-in-0 data-[state=closed]:zoom-out-95 data-[state=open]:zoom-in-95 data-[state=closed]:slide-out-to-left-1/2 data-[state=closed]:slide-out-to-top-[48%] data-[state=open]:slide-in-from-left-1/2 data-[state=open]:slide-in-from-top-[48%] sm:rounded-lg",
        className,
      )}
      {...props}
    >
      {children}
      <DialogPrimitive.Close className="absolute right-4 top-4 rounded-sm opacity-70 ring-offset-background transition-opacity hover:opacity-100 focus:outline-none focus:ring-2 focus:ring-ring focus:ring-offset-2 disabled:pointer-events-none data-[state=open]:bg-accent data-[state=open]:text-muted-foreground">
        <X className="h-4 w-4" />
        <span className="sr-only">Close</span>
      </DialogPrimitive.Close>
    </DialogPrimitive.Content>
  </DialogPortal>
))
DialogContent.displayName = DialogPrimitive.Content.displayName

const DialogHeader = ({ className, ...props }: React.HTMLAttributes<HTMLDivElement>) => (
  <div className={cn("flex flex-col space-y-1.5 text-center sm:text-left", className)} {...props} />
)
DialogHeader.displayName = "DialogHeader"

const DialogFooter = ({ className, ...props }: React.HTMLAttributes<HTMLDivElement>) => (
  <div className={cn("flex flex-col-reverse sm:flex-row sm:justify-end sm:space-x-2", className)} {...props} />
)
DialogFooter.displayName = "DialogFooter"

const DialogTitle = React.forwardRef<
  React.ElementRef<typeof DialogPrimitive.Title>,
  React.ComponentPropsWithoutRef<typeof DialogPrimitive.Title>
>(({ className, ...props }, ref) => (
  <DialogPrimitive.Title
    ref={ref}
    className={cn("text-lg font-semibold leading-none tracking-tight", className)}
    {...props}
  />
))
DialogTitle.displayName = DialogPrimitive.Title.displayName

const DialogDescription = React.forwardRef<
  React.ElementRef<typeof DialogPrimitive.Description>,
  React.ComponentPropsWithoutRef<typeof DialogPrimitive.Description>
>(({ className, ...props }, ref) => (
  <DialogPrimitive.Description ref={ref} className={cn("text-sm text-muted-foreground", className)} {...props} />
))
DialogDescription.displayName = DialogPrimitive.Description.displayName

export {
  Dialog,
  DialogPortal,
  DialogOverlay,
  DialogClose,
  DialogTrigger,
  DialogContent,
  DialogHeader,
  DialogFooter,
  DialogTitle,
  DialogDescription,
}
```

## File: dkl-microapp-2-main/components/ui/dropdown-menu.tsx
```typescript
"use client"

import * as React from "react"
import * as DropdownMenuPrimitive from "@radix-ui/react-dropdown-menu"
import { Check, ChevronRight, Circle } from "lucide-react"

import { cn } from "@/lib/utils"

const DropdownMenu = DropdownMenuPrimitive.Root

const DropdownMenuTrigger = DropdownMenuPrimitive.Trigger

const DropdownMenuGroup = DropdownMenuPrimitive.Group

const DropdownMenuPortal = DropdownMenuPrimitive.Portal

const DropdownMenuSub = DropdownMenuPrimitive.Sub

const DropdownMenuRadioGroup = DropdownMenuPrimitive.RadioGroup

const DropdownMenuSubTrigger = React.forwardRef<
  React.ElementRef<typeof DropdownMenuPrimitive.SubTrigger>,
  React.ComponentPropsWithoutRef<typeof DropdownMenuPrimitive.SubTrigger> & {
    inset?: boolean
  }
>(({ className, inset, children, ...props }, ref) => (
  <DropdownMenuPrimitive.SubTrigger
    ref={ref}
    className={cn(
      "flex cursor-default gap-2 select-none items-center rounded-sm px-2 py-1.5 text-sm outline-none focus:bg-accent data-[state=open]:bg-accent [&_svg]:pointer-events-none [&_svg]:size-4 [&_svg]:shrink-0",
      inset && "pl-8",
      className
    )}
    {...props}
  >
    {children}
    <ChevronRight className="ml-auto" />
  </DropdownMenuPrimitive.SubTrigger>
))
DropdownMenuSubTrigger.displayName =
  DropdownMenuPrimitive.SubTrigger.displayName

const DropdownMenuSubContent = React.forwardRef<
  React.ElementRef<typeof DropdownMenuPrimitive.SubContent>,
  React.ComponentPropsWithoutRef<typeof DropdownMenuPrimitive.SubContent>
>(({ className, ...props }, ref) => (
  <DropdownMenuPrimitive.SubContent
    ref={ref}
    className={cn(
      "z-50 min-w-[8rem] overflow-hidden rounded-md border bg-popover p-1 text-popover-foreground shadow-lg data-[state=open]:animate-in data-[state=closed]:animate-out data-[state=closed]:fade-out-0 data-[state=open]:fade-in-0 data-[state=closed]:zoom-out-95 data-[state=open]:zoom-in-95 data-[side=bottom]:slide-in-from-top-2 data-[side=left]:slide-in-from-right-2 data-[side=right]:slide-in-from-left-2 data-[side=top]:slide-in-from-bottom-2",
      className
    )}
    {...props}
  />
))
DropdownMenuSubContent.displayName =
  DropdownMenuPrimitive.SubContent.displayName

const DropdownMenuContent = React.forwardRef<
  React.ElementRef<typeof DropdownMenuPrimitive.Content>,
  React.ComponentPropsWithoutRef<typeof DropdownMenuPrimitive.Content>
>(({ className, sideOffset = 4, ...props }, ref) => (
  <DropdownMenuPrimitive.Portal>
    <DropdownMenuPrimitive.Content
      ref={ref}
      sideOffset={sideOffset}
      className={cn(
        "z-50 min-w-[8rem] overflow-hidden rounded-md border bg-popover p-1 text-popover-foreground shadow-md data-[state=open]:animate-in data-[state=closed]:animate-out data-[state=closed]:fade-out-0 data-[state=open]:fade-in-0 data-[state=closed]:zoom-out-95 data-[state=open]:zoom-in-95 data-[side=bottom]:slide-in-from-top-2 data-[side=left]:slide-in-from-right-2 data-[side=right]:slide-in-from-left-2 data-[side=top]:slide-in-from-bottom-2",
        className
      )}
      {...props}
    />
  </DropdownMenuPrimitive.Portal>
))
DropdownMenuContent.displayName = DropdownMenuPrimitive.Content.displayName

const DropdownMenuItem = React.forwardRef<
  React.ElementRef<typeof DropdownMenuPrimitive.Item>,
  React.ComponentPropsWithoutRef<typeof DropdownMenuPrimitive.Item> & {
    inset?: boolean
  }
>(({ className, inset, ...props }, ref) => (
  <DropdownMenuPrimitive.Item
    ref={ref}
    className={cn(
      "relative flex cursor-default select-none items-center gap-2 rounded-sm px-2 py-1.5 text-sm outline-none transition-colors focus:bg-accent focus:text-accent-foreground data-[disabled]:pointer-events-none data-[disabled]:opacity-50 [&_svg]:pointer-events-none [&_svg]:size-4 [&_svg]:shrink-0",
      inset && "pl-8",
      className
    )}
    {...props}
  />
))
DropdownMenuItem.displayName = DropdownMenuPrimitive.Item.displayName

const DropdownMenuCheckboxItem = React.forwardRef<
  React.ElementRef<typeof DropdownMenuPrimitive.CheckboxItem>,
  React.ComponentPropsWithoutRef<typeof DropdownMenuPrimitive.CheckboxItem>
>(({ className, children, checked, ...props }, ref) => (
  <DropdownMenuPrimitive.CheckboxItem
    ref={ref}
    className={cn(
      "relative flex cursor-default select-none items-center rounded-sm py-1.5 pl-8 pr-2 text-sm outline-none transition-colors focus:bg-accent focus:text-accent-foreground data-[disabled]:pointer-events-none data-[disabled]:opacity-50",
      className
    )}
    checked={checked}
    {...props}
  >
    <span className="absolute left-2 flex h-3.5 w-3.5 items-center justify-center">
      <DropdownMenuPrimitive.ItemIndicator>
        <Check className="h-4 w-4" />
      </DropdownMenuPrimitive.ItemIndicator>
    </span>
    {children}
  </DropdownMenuPrimitive.CheckboxItem>
))
DropdownMenuCheckboxItem.displayName =
  DropdownMenuPrimitive.CheckboxItem.displayName

const DropdownMenuRadioItem = React.forwardRef<
  React.ElementRef<typeof DropdownMenuPrimitive.RadioItem>,
  React.ComponentPropsWithoutRef<typeof DropdownMenuPrimitive.RadioItem>
>(({ className, children, ...props }, ref) => (
  <DropdownMenuPrimitive.RadioItem
    ref={ref}
    className={cn(
      "relative flex cursor-default select-none items-center rounded-sm py-1.5 pl-8 pr-2 text-sm outline-none transition-colors focus:bg-accent focus:text-accent-foreground data-[disabled]:pointer-events-none data-[disabled]:opacity-50",
      className
    )}
    {...props}
  >
    <span className="absolute left-2 flex h-3.5 w-3.5 items-center justify-center">
      <DropdownMenuPrimitive.ItemIndicator>
        <Circle className="h-2 w-2 fill-current" />
      </DropdownMenuPrimitive.ItemIndicator>
    </span>
    {children}
  </DropdownMenuPrimitive.RadioItem>
))
DropdownMenuRadioItem.displayName = DropdownMenuPrimitive.RadioItem.displayName

const DropdownMenuLabel = React.forwardRef<
  React.ElementRef<typeof DropdownMenuPrimitive.Label>,
  React.ComponentPropsWithoutRef<typeof DropdownMenuPrimitive.Label> & {
    inset?: boolean
  }
>(({ className, inset, ...props }, ref) => (
  <DropdownMenuPrimitive.Label
    ref={ref}
    className={cn(
      "px-2 py-1.5 text-sm font-semibold",
      inset && "pl-8",
      className
    )}
    {...props}
  />
))
DropdownMenuLabel.displayName = DropdownMenuPrimitive.Label.displayName

const DropdownMenuSeparator = React.forwardRef<
  React.ElementRef<typeof DropdownMenuPrimitive.Separator>,
  React.ComponentPropsWithoutRef<typeof DropdownMenuPrimitive.Separator>
>(({ className, ...props }, ref) => (
  <DropdownMenuPrimitive.Separator
    ref={ref}
    className={cn("-mx-1 my-1 h-px bg-muted", className)}
    {...props}
  />
))
DropdownMenuSeparator.displayName = DropdownMenuPrimitive.Separator.displayName

const DropdownMenuShortcut = ({
  className,
  ...props
}: React.HTMLAttributes<HTMLSpanElement>) => {
  return (
    <span
      className={cn("ml-auto text-xs tracking-widest opacity-60", className)}
      {...props}
    />
  )
}
DropdownMenuShortcut.displayName = "DropdownMenuShortcut"

export {
  DropdownMenu,
  DropdownMenuTrigger,
  DropdownMenuContent,
  DropdownMenuItem,
  DropdownMenuCheckboxItem,
  DropdownMenuRadioItem,
  DropdownMenuLabel,
  DropdownMenuSeparator,
  DropdownMenuShortcut,
  DropdownMenuGroup,
  DropdownMenuPortal,
  DropdownMenuSub,
  DropdownMenuSubContent,
  DropdownMenuSubTrigger,
  DropdownMenuRadioGroup,
}
```

## File: dkl-microapp-2-main/components/ui/input.tsx
```typescript
import * as React from "react"

import { cn } from "@/lib/utils"

const Input = React.forwardRef<HTMLInputElement, React.ComponentProps<"input">>(
  ({ className, type, ...props }, ref) => {
    return (
      <input
        type={type}
        className={cn(
          "flex h-10 w-full rounded-md border border-input bg-background px-3 py-2 text-base ring-offset-background file:border-0 file:bg-transparent file:text-sm file:font-medium file:text-foreground placeholder:text-muted-foreground focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2 disabled:cursor-not-allowed disabled:opacity-50 md:text-sm",
          className
        )}
        ref={ref}
        {...props}
      />
    )
  }
)
Input.displayName = "Input"

export { Input }
```

## File: dkl-microapp-2-main/components/ui/label.tsx
```typescript
"use client"

import * as React from "react"
import * as LabelPrimitive from "@radix-ui/react-label"
import { cva, type VariantProps } from "class-variance-authority"

import { cn } from "@/lib/utils"

const labelVariants = cva(
  "text-sm font-medium leading-none peer-disabled:cursor-not-allowed peer-disabled:opacity-70"
)

const Label = React.forwardRef<
  React.ElementRef<typeof LabelPrimitive.Root>,
  React.ComponentPropsWithoutRef<typeof LabelPrimitive.Root> &
    VariantProps<typeof labelVariants>
>(({ className, ...props }, ref) => (
  <LabelPrimitive.Root
    ref={ref}
    className={cn(labelVariants(), className)}
    {...props}
  />
))
Label.displayName = LabelPrimitive.Root.displayName

export { Label }
```

## File: dkl-microapp-2-main/components/ui/popover.tsx
```typescript
"use client"

import * as React from "react"
import * as PopoverPrimitive from "@radix-ui/react-popover"

import { cn } from "@/lib/utils"

const Popover = PopoverPrimitive.Root

const PopoverTrigger = PopoverPrimitive.Trigger

const PopoverContent = React.forwardRef<
  React.ElementRef<typeof PopoverPrimitive.Content>,
  React.ComponentPropsWithoutRef<typeof PopoverPrimitive.Content>
>(({ className, align = "center", sideOffset = 4, ...props }, ref) => (
  <PopoverPrimitive.Portal>
    <PopoverPrimitive.Content
      ref={ref}
      align={align}
      sideOffset={sideOffset}
      className={cn(
        "z-50 w-72 rounded-md border bg-popover p-4 text-popover-foreground shadow-md outline-none data-[state=open]:animate-in data-[state=closed]:animate-out data-[state=closed]:fade-out-0 data-[state=open]:fade-in-0 data-[state=closed]:zoom-out-95 data-[state=open]:zoom-in-95 data-[side=bottom]:slide-in-from-top-2 data-[side=left]:slide-in-from-right-2 data-[side=right]:slide-in-from-left-2 data-[side=top]:slide-in-from-bottom-2",
        className
      )}
      {...props}
    />
  </PopoverPrimitive.Portal>
))
PopoverContent.displayName = PopoverPrimitive.Content.displayName

export { Popover, PopoverTrigger, PopoverContent }
```

## File: dkl-microapp-2-main/components/ui/progress.tsx
```typescript
"use client"

import * as React from "react"
import * as ProgressPrimitive from "@radix-ui/react-progress"

import { cn } from "@/lib/utils"

const Progress = React.forwardRef<
  React.ElementRef<typeof ProgressPrimitive.Root>,
  React.ComponentPropsWithoutRef<typeof ProgressPrimitive.Root>
>(({ className, value, ...props }, ref) => (
  <ProgressPrimitive.Root
    ref={ref}
    className={cn("relative h-4 w-full overflow-hidden rounded-full bg-secondary", className)}
    {...props}
  >
    <ProgressPrimitive.Indicator
      className="h-full w-full flex-1 bg-primary transition-all"
      style={{ transform: `translateX(-${100 - (value || 0)}%)` }}
    />
  </ProgressPrimitive.Root>
))
Progress.displayName = ProgressPrimitive.Root.displayName

export { Progress }
```

## File: dkl-microapp-2-main/components/ui/radio-group.tsx
```typescript
"use client"

import * as React from "react"
import * as RadioGroupPrimitive from "@radix-ui/react-radio-group"
import { Circle } from "lucide-react"

import { cn } from "@/lib/utils"

const RadioGroup = React.forwardRef<
  React.ElementRef<typeof RadioGroupPrimitive.Root>,
  React.ComponentPropsWithoutRef<typeof RadioGroupPrimitive.Root>
>(({ className, ...props }, ref) => {
  return (
    <RadioGroupPrimitive.Root
      className={cn("grid gap-2", className)}
      {...props}
      ref={ref}
    />
  )
})
RadioGroup.displayName = RadioGroupPrimitive.Root.displayName

const RadioGroupItem = React.forwardRef<
  React.ElementRef<typeof RadioGroupPrimitive.Item>,
  React.ComponentPropsWithoutRef<typeof RadioGroupPrimitive.Item>
>(({ className, ...props }, ref) => {
  return (
    <RadioGroupPrimitive.Item
      ref={ref}
      className={cn(
        "aspect-square h-4 w-4 rounded-full border border-primary text-primary ring-offset-background focus:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2 disabled:cursor-not-allowed disabled:opacity-50",
        className
      )}
      {...props}
    >
      <RadioGroupPrimitive.Indicator className="flex items-center justify-center">
        <Circle className="h-2.5 w-2.5 fill-current text-current" />
      </RadioGroupPrimitive.Indicator>
    </RadioGroupPrimitive.Item>
  )
})
RadioGroupItem.displayName = RadioGroupPrimitive.Item.displayName

export { RadioGroup, RadioGroupItem }
```

## File: dkl-microapp-2-main/components/ui/scroll-area.tsx
```typescript
"use client"

import * as React from "react"
import * as ScrollAreaPrimitive from "@radix-ui/react-scroll-area"

import { cn } from "@/lib/utils"

const ScrollArea = React.forwardRef<
  React.ElementRef<typeof ScrollAreaPrimitive.Root>,
  React.ComponentPropsWithoutRef<typeof ScrollAreaPrimitive.Root>
>(({ className, children, ...props }, ref) => (
  <ScrollAreaPrimitive.Root
    ref={ref}
    className={cn("relative overflow-hidden", className)}
    {...props}
  >
    <ScrollAreaPrimitive.Viewport className="h-full w-full rounded-[inherit]">
      {children}
    </ScrollAreaPrimitive.Viewport>
    <ScrollBar />
    <ScrollAreaPrimitive.Corner />
  </ScrollAreaPrimitive.Root>
))
ScrollArea.displayName = ScrollAreaPrimitive.Root.displayName

const ScrollBar = React.forwardRef<
  React.ElementRef<typeof ScrollAreaPrimitive.ScrollAreaScrollbar>,
  React.ComponentPropsWithoutRef<typeof ScrollAreaPrimitive.ScrollAreaScrollbar>
>(({ className, orientation = "vertical", ...props }, ref) => (
  <ScrollAreaPrimitive.ScrollAreaScrollbar
    ref={ref}
    orientation={orientation}
    className={cn(
      "flex touch-none select-none transition-colors",
      orientation === "vertical" &&
        "h-full w-2.5 border-l border-l-transparent p-[1px]",
      orientation === "horizontal" &&
        "h-2.5 flex-col border-t border-t-transparent p-[1px]",
      className
    )}
    {...props}
  >
    <ScrollAreaPrimitive.ScrollAreaThumb className="relative flex-1 rounded-full bg-border" />
  </ScrollAreaPrimitive.ScrollAreaScrollbar>
))
ScrollBar.displayName = ScrollAreaPrimitive.ScrollAreaScrollbar.displayName

export { ScrollArea, ScrollBar }
```

## File: dkl-microapp-2-main/components/ui/select.tsx
```typescript
"use client"

import * as React from "react"
import * as SelectPrimitive from "@radix-ui/react-select"
import { Check, ChevronDown, ChevronUp } from "lucide-react"

import { cn } from "@/lib/utils"

const Select = SelectPrimitive.Root

const SelectGroup = SelectPrimitive.Group

const SelectValue = SelectPrimitive.Value

const SelectTrigger = React.forwardRef<
  React.ElementRef<typeof SelectPrimitive.Trigger>,
  React.ComponentPropsWithoutRef<typeof SelectPrimitive.Trigger>
>(({ className, children, ...props }, ref) => (
  <SelectPrimitive.Trigger
    ref={ref}
    className={cn(
      "flex h-10 w-full items-center justify-between rounded-md border border-input bg-background px-3 py-2 text-sm ring-offset-background placeholder:text-muted-foreground focus:outline-none focus:ring-2 focus:ring-ring focus:ring-offset-2 disabled:cursor-not-allowed disabled:opacity-50 [&>span]:line-clamp-1",
      className,
    )}
    {...props}
  >
    {children}
    <SelectPrimitive.Icon asChild>
      <ChevronDown className="h-4 w-4 opacity-50" />
    </SelectPrimitive.Icon>
  </SelectPrimitive.Trigger>
))
SelectTrigger.displayName = SelectPrimitive.Trigger.displayName

const SelectScrollUpButton = React.forwardRef<
  React.ElementRef<typeof SelectPrimitive.ScrollUpButton>,
  React.ComponentPropsWithoutRef<typeof SelectPrimitive.ScrollUpButton>
>(({ className, ...props }, ref) => (
  <SelectPrimitive.ScrollUpButton
    ref={ref}
    className={cn("flex cursor-default items-center justify-center py-1", className)}
    {...props}
  >
    <ChevronUp className="h-4 w-4" />
  </SelectPrimitive.ScrollUpButton>
))
SelectScrollUpButton.displayName = SelectPrimitive.ScrollUpButton.displayName

const SelectScrollDownButton = React.forwardRef<
  React.ElementRef<typeof SelectPrimitive.ScrollDownButton>,
  React.ComponentPropsWithoutRef<typeof SelectPrimitive.ScrollDownButton>
>(({ className, ...props }, ref) => (
  <SelectPrimitive.ScrollDownButton
    ref={ref}
    className={cn("flex cursor-default items-center justify-center py-1", className)}
    {...props}
  >
    <ChevronDown className="h-4 w-4" />
  </SelectPrimitive.ScrollDownButton>
))
SelectScrollDownButton.displayName = SelectPrimitive.ScrollDownButton.displayName

const SelectContent = React.forwardRef<
  React.ElementRef<typeof SelectPrimitive.Content>,
  React.ComponentPropsWithoutRef<typeof SelectPrimitive.Content>
>(({ className, children, position = "popper", ...props }, ref) => (
  <SelectPrimitive.Portal>
    <SelectPrimitive.Content
      ref={ref}
      className={cn(
        "relative z-50 max-h-96 min-w-[8rem] overflow-hidden rounded-md border bg-popover text-popover-foreground shadow-md data-[state=open]:animate-in data-[state=closed]:animate-out data-[state=closed]:fade-out-0 data-[state=open]:fade-in-0 data-[state=closed]:zoom-out-95 data-[state=open]:zoom-in-95 data-[side=bottom]:slide-in-from-top-2 data-[side=left]:slide-in-from-right-2 data-[side=right]:slide-in-from-left-2 data-[side=top]:slide-in-from-bottom-2",
        position === "popper" &&
          "data-[side=bottom]:translate-y-1 data-[side=left]:-translate-x-1 data-[side=right]:translate-x-1 data-[side=top]:-translate-y-1",
        className,
      )}
      position={position}
      {...props}
    >
      <SelectScrollUpButton />
      <SelectPrimitive.Viewport
        className={cn(
          "p-1",
          position === "popper" &&
            "h-[var(--radix-select-trigger-height)] w-full min-w-[var(--radix-select-trigger-width)]",
        )}
      >
        {children}
      </SelectPrimitive.Viewport>
      <SelectScrollDownButton />
    </SelectPrimitive.Content>
  </SelectPrimitive.Portal>
))
SelectContent.displayName = SelectPrimitive.Content.displayName

const SelectLabel = React.forwardRef<
  React.ElementRef<typeof SelectPrimitive.Label>,
  React.ComponentPropsWithoutRef<typeof SelectPrimitive.Label>
>(({ className, ...props }, ref) => (
  <SelectPrimitive.Label ref={ref} className={cn("py-1.5 pl-8 pr-2 text-sm font-semibold", className)} {...props} />
))
SelectLabel.displayName = SelectPrimitive.Label.displayName

const SelectItem = React.forwardRef<
  React.ElementRef<typeof SelectPrimitive.Item>,
  React.ComponentPropsWithoutRef<typeof SelectPrimitive.Item>
>(({ className, children, ...props }, ref) => (
  <SelectPrimitive.Item
    ref={ref}
    className={cn(
      "relative flex w-full cursor-default select-none items-center rounded-sm py-1.5 pl-8 pr-2 text-sm outline-none focus:bg-accent focus:text-accent-foreground data-[disabled]:pointer-events-none data-[disabled]:opacity-50",
      className,
    )}
    {...props}
  >
    <span className="absolute left-2 flex h-3.5 w-3.5 items-center justify-center">
      <SelectPrimitive.ItemIndicator>
        <Check className="h-4 w-4" />
      </SelectPrimitive.ItemIndicator>
    </span>

    <SelectPrimitive.ItemText>{children}</SelectPrimitive.ItemText>
  </SelectPrimitive.Item>
))
SelectItem.displayName = SelectPrimitive.Item.displayName

const SelectSeparator = React.forwardRef<
  React.ElementRef<typeof SelectPrimitive.Separator>,
  React.ComponentPropsWithoutRef<typeof SelectPrimitive.Separator>
>(({ className, ...props }, ref) => (
  <SelectPrimitive.Separator ref={ref} className={cn("-mx-1 my-1 h-px bg-muted", className)} {...props} />
))
SelectSeparator.displayName = SelectPrimitive.Separator.displayName

export {
  Select,
  SelectGroup,
  SelectValue,
  SelectTrigger,
  SelectContent,
  SelectLabel,
  SelectItem,
  SelectSeparator,
  SelectScrollUpButton,
  SelectScrollDownButton,
}
```

## File: dkl-microapp-2-main/components/ui/separator.tsx
```typescript
"use client"

import * as React from "react"
import * as SeparatorPrimitive from "@radix-ui/react-separator"

import { cn } from "@/lib/utils"

const Separator = React.forwardRef<
  React.ElementRef<typeof SeparatorPrimitive.Root>,
  React.ComponentPropsWithoutRef<typeof SeparatorPrimitive.Root>
>(
  (
    { className, orientation = "horizontal", decorative = true, ...props },
    ref
  ) => (
    <SeparatorPrimitive.Root
      ref={ref}
      decorative={decorative}
      orientation={orientation}
      className={cn(
        "shrink-0 bg-border",
        orientation === "horizontal" ? "h-[1px] w-full" : "h-full w-[1px]",
        className
      )}
      {...props}
    />
  )
)
Separator.displayName = SeparatorPrimitive.Root.displayName

export { Separator }
```

## File: dkl-microapp-2-main/components/ui/sheet.tsx
```typescript
"use client"

import * as React from "react"
import * as SheetPrimitive from "@radix-ui/react-dialog"
import { cva, type VariantProps } from "class-variance-authority"
import { X } from "lucide-react"

import { cn } from "@/lib/utils"

const Sheet = SheetPrimitive.Root

const SheetTrigger = SheetPrimitive.Trigger

const SheetClose = SheetPrimitive.Close

const SheetPortal = SheetPrimitive.Portal

const SheetOverlay = React.forwardRef<
  React.ElementRef<typeof SheetPrimitive.Overlay>,
  React.ComponentPropsWithoutRef<typeof SheetPrimitive.Overlay>
>(({ className, ...props }, ref) => (
  <SheetPrimitive.Overlay
    className={cn(
      "fixed inset-0 z-50 bg-black/80  data-[state=open]:animate-in data-[state=closed]:animate-out data-[state=closed]:fade-out-0 data-[state=open]:fade-in-0",
      className
    )}
    {...props}
    ref={ref}
  />
))
SheetOverlay.displayName = SheetPrimitive.Overlay.displayName

const sheetVariants = cva(
  "fixed z-50 gap-4 bg-background p-6 shadow-lg transition ease-in-out data-[state=open]:animate-in data-[state=closed]:animate-out data-[state=closed]:duration-300 data-[state=open]:duration-500",
  {
    variants: {
      side: {
        top: "inset-x-0 top-0 border-b data-[state=closed]:slide-out-to-top data-[state=open]:slide-in-from-top",
        bottom:
          "inset-x-0 bottom-0 border-t data-[state=closed]:slide-out-to-bottom data-[state=open]:slide-in-from-bottom",
        left: "inset-y-0 left-0 h-full w-3/4 border-r data-[state=closed]:slide-out-to-left data-[state=open]:slide-in-from-left sm:max-w-sm",
        right:
          "inset-y-0 right-0 h-full w-3/4  border-l data-[state=closed]:slide-out-to-right data-[state=open]:slide-in-from-right sm:max-w-sm",
      },
    },
    defaultVariants: {
      side: "right",
    },
  }
)

interface SheetContentProps
  extends React.ComponentPropsWithoutRef<typeof SheetPrimitive.Content>,
    VariantProps<typeof sheetVariants> {}

const SheetContent = React.forwardRef<
  React.ElementRef<typeof SheetPrimitive.Content>,
  SheetContentProps
>(({ side = "right", className, children, ...props }, ref) => (
  <SheetPortal>
    <SheetOverlay />
    <SheetPrimitive.Content
      ref={ref}
      className={cn(sheetVariants({ side }), className)}
      {...props}
    >
      {children}
      <SheetPrimitive.Close className="absolute right-4 top-4 rounded-sm opacity-70 ring-offset-background transition-opacity hover:opacity-100 focus:outline-none focus:ring-2 focus:ring-ring focus:ring-offset-2 disabled:pointer-events-none data-[state=open]:bg-secondary">
        <X className="h-4 w-4" />
        <span className="sr-only">Close</span>
      </SheetPrimitive.Close>
    </SheetPrimitive.Content>
  </SheetPortal>
))
SheetContent.displayName = SheetPrimitive.Content.displayName

const SheetHeader = ({
  className,
  ...props
}: React.HTMLAttributes<HTMLDivElement>) => (
  <div
    className={cn(
      "flex flex-col space-y-2 text-center sm:text-left",
      className
    )}
    {...props}
  />
)
SheetHeader.displayName = "SheetHeader"

const SheetFooter = ({
  className,
  ...props
}: React.HTMLAttributes<HTMLDivElement>) => (
  <div
    className={cn(
      "flex flex-col-reverse sm:flex-row sm:justify-end sm:space-x-2",
      className
    )}
    {...props}
  />
)
SheetFooter.displayName = "SheetFooter"

const SheetTitle = React.forwardRef<
  React.ElementRef<typeof SheetPrimitive.Title>,
  React.ComponentPropsWithoutRef<typeof SheetPrimitive.Title>
>(({ className, ...props }, ref) => (
  <SheetPrimitive.Title
    ref={ref}
    className={cn("text-lg font-semibold text-foreground", className)}
    {...props}
  />
))
SheetTitle.displayName = SheetPrimitive.Title.displayName

const SheetDescription = React.forwardRef<
  React.ElementRef<typeof SheetPrimitive.Description>,
  React.ComponentPropsWithoutRef<typeof SheetPrimitive.Description>
>(({ className, ...props }, ref) => (
  <SheetPrimitive.Description
    ref={ref}
    className={cn("text-sm text-muted-foreground", className)}
    {...props}
  />
))
SheetDescription.displayName = SheetPrimitive.Description.displayName

export {
  Sheet,
  SheetPortal,
  SheetOverlay,
  SheetTrigger,
  SheetClose,
  SheetContent,
  SheetHeader,
  SheetFooter,
  SheetTitle,
  SheetDescription,
}
```

## File: dkl-microapp-2-main/components/ui/switch.tsx
```typescript
"use client"

import * as React from "react"
import * as SwitchPrimitives from "@radix-ui/react-switch"

import { cn } from "@/lib/utils"

const Switch = React.forwardRef<
  React.ElementRef<typeof SwitchPrimitives.Root>,
  React.ComponentPropsWithoutRef<typeof SwitchPrimitives.Root>
>(({ className, ...props }, ref) => (
  <SwitchPrimitives.Root
    className={cn(
      "peer inline-flex h-6 w-11 shrink-0 cursor-pointer items-center rounded-full border-2 border-transparent transition-colors focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2 focus-visible:ring-offset-background disabled:cursor-not-allowed disabled:opacity-50 data-[state=checked]:bg-primary data-[state=unchecked]:bg-input",
      className,
    )}
    {...props}
    ref={ref}
  >
    <SwitchPrimitives.Thumb
      className={cn(
        "pointer-events-none block h-5 w-5 rounded-full bg-background shadow-lg ring-0 transition-transform data-[state=checked]:translate-x-5 data-[state=unchecked]:translate-x-0",
      )}
    />
  </SwitchPrimitives.Root>
))
Switch.displayName = SwitchPrimitives.Root.displayName

export { Switch }
```

## File: dkl-microapp-2-main/components/ui/table.tsx
```typescript
import * as React from "react"

import { cn } from "@/lib/utils"

const Table = React.forwardRef<HTMLTableElement, React.HTMLAttributes<HTMLTableElement>>(
  ({ className, ...props }, ref) => (
    <div className="relative w-full overflow-auto">
      <table ref={ref} className={cn("w-full caption-bottom text-sm", className)} {...props} />
    </div>
  ),
)
Table.displayName = "Table"

const TableHeader = React.forwardRef<HTMLTableSectionElement, React.HTMLAttributes<HTMLTableSectionElement>>(
  ({ className, ...props }, ref) => <thead ref={ref} className={cn("[&_tr]:border-b", className)} {...props} />,
)
TableHeader.displayName = "TableHeader"

const TableBody = React.forwardRef<HTMLTableSectionElement, React.HTMLAttributes<HTMLTableSectionElement>>(
  ({ className, ...props }, ref) => (
    <tbody ref={ref} className={cn("[&_tr:last-child]:border-0", className)} {...props} />
  ),
)
TableBody.displayName = "TableBody"

const TableFooter = React.forwardRef<HTMLTableSectionElement, React.HTMLAttributes<HTMLTableSectionElement>>(
  ({ className, ...props }, ref) => (
    <tfoot ref={ref} className={cn("bg-primary font-medium text-primary-foreground", className)} {...props} />
  ),
)
TableFooter.displayName = "TableFooter"

const TableRow = React.forwardRef<HTMLTableRowElement, React.HTMLAttributes<HTMLTableRowElement>>(
  ({ className, ...props }, ref) => (
    <tr
      ref={ref}
      className={cn("border-b transition-colors hover:bg-muted/50 data-[state=selected]:bg-muted", className)}
      {...props}
    />
  ),
)
TableRow.displayName = "TableRow"

const TableHead = React.forwardRef<HTMLTableCellElement, React.ThHTMLAttributes<HTMLTableCellElement>>(
  ({ className, ...props }, ref) => (
    <th
      ref={ref}
      className={cn(
        "h-10 px-2 text-left align-middle font-medium text-muted-foreground [&:has([role=checkbox])]:pr-0 [&>[role=checkbox]]:translate-y-[2px]",
        className,
      )}
      {...props}
    />
  ),
)
TableHead.displayName = "TableHead"

const TableCell = React.forwardRef<HTMLTableCellElement, React.TdHTMLAttributes<HTMLTableCellElement>>(
  ({ className, ...props }, ref) => (
    <td
      ref={ref}
      className={cn("p-2 align-middle [&:has([role=checkbox])]:pr-0 [&>[role=checkbox]]:translate-y-[2px]", className)}
      {...props}
    />
  ),
)
TableCell.displayName = "TableCell"

const TableCaption = React.forwardRef<HTMLTableCaptionElement, React.HTMLAttributes<HTMLTableCaptionElement>>(
  ({ className, ...props }, ref) => (
    <caption ref={ref} className={cn("mt-4 text-sm text-muted-foreground", className)} {...props} />
  ),
)
TableCaption.displayName = "TableCaption"

export { Table, TableHeader, TableBody, TableFooter, TableHead, TableRow, TableCell, TableCaption }
```

## File: dkl-microapp-2-main/components/ui/tabs.tsx
```typescript
"use client"

import * as React from "react"
import * as TabsPrimitive from "@radix-ui/react-tabs"

import { cn } from "@/lib/utils"

const Tabs = TabsPrimitive.Root

const TabsList = React.forwardRef<
  React.ElementRef<typeof TabsPrimitive.List>,
  React.ComponentPropsWithoutRef<typeof TabsPrimitive.List>
>(({ className, ...props }, ref) => (
  <TabsPrimitive.List
    ref={ref}
    className={cn(
      "inline-flex h-10 items-center justify-center rounded-md bg-muted p-1 text-muted-foreground",
      className,
    )}
    {...props}
  />
))
TabsList.displayName = TabsPrimitive.List.displayName

const TabsTrigger = React.forwardRef<
  React.ElementRef<typeof TabsPrimitive.Trigger>,
  React.ComponentPropsWithoutRef<typeof TabsPrimitive.Trigger>
>(({ className, ...props }, ref) => (
  <TabsPrimitive.Trigger
    ref={ref}
    className={cn(
      "inline-flex items-center justify-center whitespace-nowrap rounded-sm px-3 py-1.5 text-sm font-medium ring-offset-background transition-all focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2 disabled:pointer-events-none disabled:opacity-50 data-[state=active]:bg-background data-[state=active]:text-foreground data-[state=active]:shadow-sm",
      className,
    )}
    {...props}
  />
))
TabsTrigger.displayName = TabsPrimitive.Trigger.displayName

const TabsContent = React.forwardRef<
  React.ElementRef<typeof TabsPrimitive.Content>,
  React.ComponentPropsWithoutRef<typeof TabsPrimitive.Content>
>(({ className, ...props }, ref) => (
  <TabsPrimitive.Content
    ref={ref}
    className={cn(
      "mt-2 ring-offset-background focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2",
      className,
    )}
    {...props}
  />
))
TabsContent.displayName = TabsPrimitive.Content.displayName

export { Tabs, TabsList, TabsTrigger, TabsContent }
```

## File: dkl-microapp-2-main/components/ui/textarea.tsx
```typescript
import * as React from "react"

import { cn } from "@/lib/utils"

export interface TextareaProps extends React.TextareaHTMLAttributes<HTMLTextAreaElement> {}

const Textarea = React.forwardRef<HTMLTextAreaElement, TextareaProps>(({ className, ...props }, ref) => {
  return (
    <textarea
      className={cn(
        "flex min-h-[80px] w-full rounded-md border border-input bg-background px-3 py-2 text-sm ring-offset-background placeholder:text-muted-foreground focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2 disabled:cursor-not-allowed disabled:opacity-50",
        className,
      )}
      ref={ref}
      {...props}
    />
  )
})
Textarea.displayName = "Textarea"

export { Textarea }
```

## File: dkl-microapp-2-main/components/ui/toast.tsx
```typescript
"use client"

import * as React from "react"
import * as ToastPrimitives from "@radix-ui/react-toast"
import { cva, type VariantProps } from "class-variance-authority"
import { X } from "lucide-react"

import { cn } from "@/lib/utils"

const ToastProvider = ToastPrimitives.Provider

const ToastViewport = React.forwardRef<
  React.ElementRef<typeof ToastPrimitives.Viewport>,
  React.ComponentPropsWithoutRef<typeof ToastPrimitives.Viewport>
>(({ className, ...props }, ref) => (
  <ToastPrimitives.Viewport
    ref={ref}
    className={cn(
      "fixed top-0 z-[100] flex max-h-screen w-full flex-col-reverse p-4 sm:bottom-0 sm:right-0 sm:top-auto sm:flex-col md:max-w-[420px]",
      className,
    )}
    {...props}
  />
))
ToastViewport.displayName = ToastPrimitives.Viewport.displayName

const toastVariants = cva(
  "group pointer-events-auto relative flex w-full items-center justify-between space-x-4 overflow-hidden rounded-md border p-6 pr-8 shadow-lg transition-all data-[swipe=cancel]:translate-x-0 data-[swipe=end]:translate-x-[var(--radix-toast-swipe-end-x)] data-[swipe=move]:translate-x-[var(--radix-toast-swipe-move-x)] data-[swipe=move]:transition-none data-[state=open]:animate-in data-[state=closed]:animate-out data-[swipe=end]:animate-out data-[state=closed]:fade-out-80 data-[state=closed]:slide-out-to-right-full data-[state=open]:slide-in-from-top-full data-[state=open]:sm:slide-in-from-bottom-full",
  {
    variants: {
      variant: {
        default: "border bg-background text-foreground",
        destructive: "destructive group border-destructive bg-destructive text-destructive-foreground",
      },
    },
    defaultVariants: {
      variant: "default",
    },
  },
)

const Toast = React.forwardRef<
  React.ElementRef<typeof ToastPrimitives.Root>,
  React.ComponentPropsWithoutRef<typeof ToastPrimitives.Root> & VariantProps<typeof toastVariants>
>(({ className, variant, ...props }, ref) => {
  return <ToastPrimitives.Root ref={ref} className={cn(toastVariants({ variant }), className)} {...props} />
})
Toast.displayName = ToastPrimitives.Root.displayName

const ToastAction = React.forwardRef<
  React.ElementRef<typeof ToastPrimitives.Action>,
  React.ComponentPropsWithoutRef<typeof ToastPrimitives.Action>
>(({ className, ...props }, ref) => (
  <ToastPrimitives.Action
    ref={ref}
    className={cn(
      "inline-flex h-8 shrink-0 items-center justify-center rounded-md border bg-transparent px-3 text-sm font-medium ring-offset-background transition-colors hover:bg-secondary focus:outline-none focus:ring-2 focus:ring-ring focus:ring-offset-2 disabled:pointer-events-none disabled:opacity-50 group-[.destructive]:border-muted/40 group-[.destructive]:hover:border-destructive/30 group-[.destructive]:hover:bg-destructive group-[.destructive]:hover:text-destructive-foreground group-[.destructive]:focus:ring-destructive",
      className,
    )}
    {...props}
  />
))
ToastAction.displayName = ToastPrimitives.Action.displayName

const ToastClose = React.forwardRef<
  React.ElementRef<typeof ToastPrimitives.Close>,
  React.ComponentPropsWithoutRef<typeof ToastPrimitives.Close>
>(({ className, ...props }, ref) => (
  <ToastPrimitives.Close
    ref={ref}
    className={cn(
      "absolute right-2 top-2 rounded-md p-1 text-foreground/50 opacity-0 transition-opacity hover:text-foreground focus:opacity-100 focus:outline-none focus:ring-2 group-hover:opacity-100 group-[.destructive]:text-red-300 group-[.destructive]:hover:text-red-50 group-[.destructive]:focus:ring-red-400 group-[.destructive]:focus:ring-offset-red-600",
      className,
    )}
    toast-close=""
    {...props}
  >
    <X className="h-4 w-4" />
  </ToastPrimitives.Close>
))
ToastClose.displayName = ToastPrimitives.Close.displayName

const ToastTitle = React.forwardRef<
  React.ElementRef<typeof ToastPrimitives.Title>,
  React.ComponentPropsWithoutRef<typeof ToastPrimitives.Title>
>(({ className, ...props }, ref) => (
  <ToastPrimitives.Title ref={ref} className={cn("text-sm font-semibold", className)} {...props} />
))
ToastTitle.displayName = ToastPrimitives.Title.displayName

const ToastDescription = React.forwardRef<
  React.ElementRef<typeof ToastPrimitives.Description>,
  React.ComponentPropsWithoutRef<typeof ToastPrimitives.Description>
>(({ className, ...props }, ref) => (
  <ToastPrimitives.Description ref={ref} className={cn("text-sm opacity-90", className)} {...props} />
))
ToastDescription.displayName = ToastPrimitives.Description.displayName

type ToastProps = React.ComponentPropsWithoutRef<typeof Toast>

type ToastActionElement = React.ReactElement<typeof ToastAction>

export {
  type ToastProps,
  type ToastActionElement,
  ToastProvider,
  ToastViewport,
  Toast,
  ToastTitle,
  ToastDescription,
  ToastClose,
  ToastAction,
}
```

## File: dkl-microapp-2-main/components/ui/toaster.tsx
```typescript
"use client"

import { Toast, ToastClose, ToastDescription, ToastProvider, ToastTitle, ToastViewport } from "@/components/ui/toast"
import { useToast } from "@/hooks/use-toast"

export function Toaster() {
  const { toasts } = useToast()

  return (
    <ToastProvider>
      {toasts.map(({ id, title, description, action, ...props }) => (
        <Toast key={id} {...props}>
          <div className="grid gap-1">
            {title && <ToastTitle>{title}</ToastTitle>}
            {description && <ToastDescription>{description}</ToastDescription>}
          </div>
          {action}
          <ToastClose />
        </Toast>
      ))}
      <ToastViewport />
    </ToastProvider>
  )
}
```

## File: dkl-microapp-2-main/components/ui/toggle.tsx
```typescript
"use client"

import * as React from "react"
import * as TogglePrimitive from "@radix-ui/react-toggle"
import { cva, type VariantProps } from "class-variance-authority"

import { cn } from "@/lib/utils"

const toggleVariants = cva(
  "inline-flex items-center justify-center rounded-md text-sm font-medium ring-offset-background transition-colors hover:bg-muted hover:text-muted-foreground focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2 disabled:pointer-events-none disabled:opacity-50 data-[state=on]:bg-accent data-[state=on]:text-accent-foreground [&_svg]:pointer-events-none [&_svg]:size-4 [&_svg]:shrink-0 gap-2",
  {
    variants: {
      variant: {
        default: "bg-transparent",
        outline:
          "border border-input bg-transparent hover:bg-accent hover:text-accent-foreground",
      },
      size: {
        default: "h-10 px-3 min-w-10",
        sm: "h-9 px-2.5 min-w-9",
        lg: "h-11 px-5 min-w-11",
      },
    },
    defaultVariants: {
      variant: "default",
      size: "default",
    },
  }
)

const Toggle = React.forwardRef<
  React.ElementRef<typeof TogglePrimitive.Root>,
  React.ComponentPropsWithoutRef<typeof TogglePrimitive.Root> &
    VariantProps<typeof toggleVariants>
>(({ className, variant, size, ...props }, ref) => (
  <TogglePrimitive.Root
    ref={ref}
    className={cn(toggleVariants({ variant, size, className }))}
    {...props}
  />
))

Toggle.displayName = TogglePrimitive.Root.displayName

export { Toggle, toggleVariants }
```

## File: dkl-microapp-2-main/components/builder-assignment-dialog.tsx
```typescript
"use client"

import * as React from "react"
import {
  AlertDialog,
  AlertDialogAction,
  AlertDialogCancel,
  AlertDialogContent,
  AlertDialogDescription,
  AlertDialogFooter,
  AlertDialogHeader,
  AlertDialogTitle,
} from "@/components/ui/alert-dialog"
import { Button } from "@/components/ui/button"
import { Command, CommandEmpty, CommandGroup, CommandInput, CommandItem, CommandList } from "@/components/ui/command"
import { Popover, PopoverContent, PopoverTrigger } from "@/components/ui/popover"
import { useToast } from "@/hooks/use-toast"
import { supabase } from "@/lib/supabase/client"
import type { Database } from "@/types/supabase"
import { ChevronsUpDown, Check } from "lucide-react"
import { cn } from "@/lib/utils"

type Builder = Database["public"]["Tables"]["builders"]["Row"]

interface BuilderAssignmentDialogProps {
  open: boolean
  onOpenChange: (open: boolean) => void
  selectedPropertyIds: string[]
  onAssignmentComplete: () => void
}

export function BuilderAssignmentDialog({
  open,
  onOpenChange,
  selectedPropertyIds,
  onAssignmentComplete,
}: BuilderAssignmentDialogProps) {
  const [builders, setBuilders] = React.useState<Builder[]>([])
  const [selectedBuilderId, setSelectedBuilderId] = React.useState<string | null>(null)
  const [isLoadingBuilders, setIsLoadingBuilders] = React.useState(false)
  const [isAssigning, setIsAssigning] = React.useState(false)
  const [popoverOpen, setPopoverOpen] = React.useState(false)

  const { toast } = useToast()

  React.useEffect(() => {
    if (open) {
      const fetchBuilders = async () => {
        setIsLoadingBuilders(true)
        // Fetch only essential fields for the dropdown
        const { data, error } = await supabase.from("builders").select("id, name, company_name").order("name")

        if (error) {
          toast({
            title: "Error fetching builders",
            description: error.message,
            variant: "destructive",
          })
          setBuilders([])
        } else {
          setBuilders(data || [])
        }
        setIsLoadingBuilders(false)
      }
      fetchBuilders()
      setSelectedBuilderId(null) // Reset selected builder when dialog opens
    }
  }, [open, toast])

  const handleAssignBuilder = async () => {
    if (!selectedBuilderId) {
      toast({
        title: "No builder selected",
        description: "Please select a builder to assign.",
        variant: "warning", // Changed from "destructive" to "warning" for non-critical user error
      })
      return
    }

    if (!selectedPropertyIds || selectedPropertyIds.length === 0) {
      toast({
        title: "No listings selected",
        description: "No listings were selected to assign the builder to.", // More user-friendly message
        variant: "warning",
      })
      return
    }

    setIsAssigning(true)
    const updates = selectedPropertyIds.map((propertyId) => ({
      id: propertyId, // Ensure this matches the primary key of your listings table
      builder_id: selectedBuilderId,
    }))

    // Using .upsert might be safer if you have RLS policies that prevent updates unless certain conditions are met
    // and you want to ensure the operation goes through. .update is also fine.
    const { error } = await supabase.from("listings").upsert(updates).select()

    setIsAssigning(false)

    if (error) {
      toast({
        title: "Failed to assign builder",
        description: error.message || "Something went wrong. Please try again.",
        variant: "destructive",
      })
    } else {
      toast({
        title: "Builder assigned successfully",
        description: `Assigned builder to ${selectedPropertyIds.length} listing(s).`,
      })
      onAssignmentComplete() // Callback to refresh data on the parent page
      onOpenChange(false) // Close the dialog
    }
  }

  // Render nothing if the dialog is not open
  if (!open) {
    return null
  }

  return (
    <AlertDialog open={open} onOpenChange={onOpenChange}>
      <AlertDialogContent>
        <AlertDialogHeader>
          <AlertDialogTitle>Assign Builder to Listings</AlertDialogTitle>
          <AlertDialogDescription>
            Select a builder to assign to the {selectedPropertyIds.length} selected listing(s).
          </AlertDialogDescription>
        </AlertDialogHeader>

        <Popover open={popoverOpen} onOpenChange={setPopoverOpen}>
          <PopoverTrigger asChild>
            <Button
              variant="outline"
              role="combobox"
              aria-expanded={popoverOpen}
              className="w-full justify-between"
              disabled={isLoadingBuilders || builders.length === 0}
            >
              {selectedBuilderId
                ? (builders.find((builder) => builder.id === selectedBuilderId)?.name ?? "Select builder...")
                : "Select builder..."}
              <ChevronsUpDown className="ml-2 h-4 w-4 shrink-0 opacity-50" />
            </Button>
          </PopoverTrigger>
          <PopoverContent className="w-[--radix-popover-trigger-width] p-0">
            <Command>
              <CommandInput placeholder="Search builders..." />
              <CommandList>
                {isLoadingBuilders && <CommandItem disabled>Loading builders...</CommandItem>}
                {!isLoadingBuilders && builders.length === 0 && <CommandItem disabled>No builders found.</CommandItem>}
                <CommandEmpty>No builder found.</CommandEmpty>
                <CommandGroup>
                  {builders.map((builder) => (
                    <CommandItem
                      key={builder.id}
                      value={builder.name || builder.id} // Ensure value is unique and searchable
                      onSelect={() => {
                        setSelectedBuilderId(builder.id)
                        setPopoverOpen(false)
                      }}
                    >
                      <Check
                        className={cn("mr-2 h-4 w-4", selectedBuilderId === builder.id ? "opacity-100" : "opacity-0")}
                      />
                      {builder.name} {builder.company_name && `(${builder.company_name})`}
                    </CommandItem>
                  ))}
                </CommandGroup>
              </CommandList>
            </Command>
          </PopoverContent>
        </Popover>

        <AlertDialogFooter>
          <AlertDialogCancel disabled={isAssigning}>Cancel</AlertDialogCancel>
          <AlertDialogAction
            onClick={handleAssignBuilder}
            disabled={!selectedBuilderId || isAssigning || isLoadingBuilders || selectedPropertyIds.length === 0}
          >
            {isAssigning ? "Assigning..." : "Assign"}
          </AlertDialogAction>
        </AlertDialogFooter>
      </AlertDialogContent>
    </AlertDialog>
  )
}
```

## File: dkl-microapp-2-main/components/builder-form-dialog.tsx
```typescript
"use client"

import type React from "react"
import { useState, useEffect } from "react"
import { supabase } from "@/lib/supabase/client"
import { Button } from "@/components/ui/button"
import { Input } from "@/components/ui/input"
import { Label } from "@/components/ui/label"
import { Textarea } from "@/components/ui/textarea"
import {
  Dialog,
  DialogContent,
  DialogHeader,
  DialogTitle,
  DialogDescription,
  DialogFooter,
  DialogClose,
} from "@/components/ui/dialog"
import { useToast } from "@/hooks/use-toast"
import { Save, Loader2 } from "lucide-react"
import type { Database } from "@/types/supabase"

interface BuilderFormDialogProps {
  open: boolean
  onOpenChange: (open: boolean) => void
  onBuilderCreated: () => void
  builder?: Partial<Database["public"]["Tables"]["builders"]["Row"]> // For potential edit mode
}

const initialFormData = {
  name: "",
  company_name: "",
  phone: "",
  email: "",
  website: "",
  address: "",
  city: "",
  state: "",
  zip_code: "",
  years_in_business: "",
  total_projects: "",
  active_projects: "",
  price_range_min: "",
  price_range_max: "",
  specialties: "", // Stored as comma-separated string in form, converted to array on submit
  notes: "",
}

export function BuilderFormDialog({ open, onOpenChange, onBuilderCreated, builder }: BuilderFormDialogProps) {
  const { toast } = useToast()
  const [loading, setLoading] = useState(false)
  const [formData, setFormData] = useState(initialFormData)

  useEffect(() => {
    if (builder && open) {
      setFormData({
        name: builder.name || "",
        company_name: builder.company_name || "",
        phone: builder.phone || "",
        email: builder.email || "",
        website: builder.website || "",
        address: builder.address || "",
        city: builder.city || "",
        state: builder.state || "",
        zip_code: builder.zip_code || "",
        years_in_business: builder.years_in_business?.toString() || "",
        total_projects: builder.total_projects?.toString() || "",
        active_projects: builder.active_projects?.toString() || "",
        price_range_min: builder.price_range_min?.toString() || "",
        price_range_max: builder.price_range_max?.toString() || "",
        specialties: Array.isArray(builder.specialties) ? builder.specialties.join(", ") : builder.specialties || "",
        notes: builder.notes || "",
      })
    } else if (!builder && open) {
      setFormData(initialFormData)
    }
  }, [builder, open])

  const handleSubmit = async (e: React.FormEvent) => {
    e.preventDefault()
    setLoading(true)

    try {
      const builderData = {
        ...formData,
        years_in_business: formData.years_in_business ? Number.parseInt(formData.years_in_business) : null,
        total_projects: formData.total_projects ? Number.parseInt(formData.total_projects) : null,
        active_projects: formData.active_projects ? Number.parseInt(formData.active_projects) : null,
        price_range_min: formData.price_range_min ? Number.parseFloat(formData.price_range_min) : null,
        price_range_max: formData.price_range_max ? Number.parseFloat(formData.price_range_max) : null,
        specialties: formData.specialties
          ? formData.specialties
              .split(",")
              .map((s) => s.trim())
              .filter(Boolean)
          : null,
      }

      // eslint-disable-next-line @typescript-eslint/no-unused-vars
      const { id, created_at, updated_at, ...upsertData } = builderData

      const { error } = await supabase
        .from("builders")
        .upsert(builder?.id ? { ...upsertData, id: builder.id } : upsertData)

      if (error) throw error

      toast({
        title: builder?.id ? "Builder Updated" : "Builder Created",
        description: `Builder has been successfully ${builder?.id ? "updated" : "added"}.`,
      })
      onBuilderCreated()
      onOpenChange(false)
    } catch (error: any) {
      toast({
        title: "Error",
        description: error.message || `Failed to ${builder?.id ? "update" : "create"} builder.`,
        variant: "destructive",
      })
    } finally {
      setLoading(false)
    }
  }

  return (
    <Dialog open={open} onOpenChange={onOpenChange}>
      <DialogContent className="sm:max-w-[800px] max-h-[90vh] overflow-y-auto">
        <DialogHeader>
          <DialogTitle>{builder?.id ? "Edit Builder" : "Add New Builder"}</DialogTitle>
          <DialogDescription>Fill in the details for the builder. Click save when you're done.</DialogDescription>
        </DialogHeader>
        <form onSubmit={handleSubmit} className="py-4">
          <div className="grid gap-4 lg:grid-cols-2">
            <div className="space-y-3 rounded-md border p-4">
              <h3 className="text-sm font-medium mb-2">Basic Information</h3>
              <div>
                <Label htmlFor="name" className="text-xs">
                  Builder Name *
                </Label>
                <Input
                  id="name"
                  value={formData.name}
                  onChange={(e) => setFormData({ ...formData, name: e.target.value })}
                  className="h-8 text-xs"
                  required
                />
              </div>
              <div>
                <Label htmlFor="company_name" className="text-xs">
                  Company Name
                </Label>
                <Input
                  id="company_name"
                  value={formData.company_name}
                  onChange={(e) => setFormData({ ...formData, company_name: e.target.value })}
                  className="h-8 text-xs"
                />
              </div>
              <div>
                <Label htmlFor="phone" className="text-xs">
                  Phone
                </Label>
                <Input
                  id="phone"
                  value={formData.phone}
                  onChange={(e) => setFormData({ ...formData, phone: e.target.value })}
                  className="h-8 text-xs"
                />
              </div>
              <div>
                <Label htmlFor="email" className="text-xs">
                  Email
                </Label>
                <Input
                  id="email"
                  type="email"
                  value={formData.email}
                  onChange={(e) => setFormData({ ...formData, email: e.target.value })}
                  className="h-8 text-xs"
                />
              </div>
              <div>
                <Label htmlFor="website" className="text-xs">
                  Website
                </Label>
                <Input
                  id="website"
                  value={formData.website}
                  onChange={(e) => setFormData({ ...formData, website: e.target.value })}
                  className="h-8 text-xs"
                  placeholder="https://"
                />
              </div>
            </div>

            <div className="space-y-3 rounded-md border p-4">
              <h3 className="text-sm font-medium mb-2">Address</h3>
              <div>
                <Label htmlFor="address" className="text-xs">
                  Street Address
                </Label>
                <Input
                  id="address"
                  value={formData.address}
                  onChange={(e) => setFormData({ ...formData, address: e.target.value })}
                  className="h-8 text-xs"
                />
              </div>
              <div>
                <Label htmlFor="city" className="text-xs">
                  City
                </Label>
                <Input
                  id="city"
                  value={formData.city}
                  onChange={(e) => setFormData({ ...formData, city: e.target.value })}
                  className="h-8 text-xs"
                />
              </div>
              <div className="grid grid-cols-2 gap-2">
                <div>
                  <Label htmlFor="state" className="text-xs">
                    State
                  </Label>
                  <Input
                    id="state"
                    value={formData.state}
                    onChange={(e) => setFormData({ ...formData, state: e.target.value })}
                    className="h-8 text-xs"
                    placeholder="VA"
                  />
                </div>
                <div>
                  <Label htmlFor="zip_code" className="text-xs">
                    Zip Code
                  </Label>
                  <Input
                    id="zip_code"
                    value={formData.zip_code}
                    onChange={(e) => setFormData({ ...formData, zip_code: e.target.value })}
                    className="h-8 text-xs"
                  />
                </div>
              </div>
            </div>

            <div className="space-y-3 rounded-md border p-4">
              <h3 className="text-sm font-medium mb-2">Business Details</h3>
              <div>
                <Label htmlFor="years_in_business" className="text-xs">
                  Years in Business
                </Label>
                <Input
                  id="years_in_business"
                  type="number"
                  value={formData.years_in_business}
                  onChange={(e) => setFormData({ ...formData, years_in_business: e.target.value })}
                  className="h-8 text-xs"
                />
              </div>
              <div className="grid grid-cols-2 gap-2">
                <div>
                  <Label htmlFor="total_projects" className="text-xs">
                    Total Projects
                  </Label>
                  <Input
                    id="total_projects"
                    type="number"
                    value={formData.total_projects}
                    onChange={(e) => setFormData({ ...formData, total_projects: e.target.value })}
                    className="h-8 text-xs"
                  />
                </div>
                <div>
                  <Label htmlFor="active_projects" className="text-xs">
                    Active Projects
                  </Label>
                  <Input
                    id="active_projects"
                    type="number"
                    value={formData.active_projects}
                    onChange={(e) => setFormData({ ...formData, active_projects: e.target.value })}
                    className="h-8 text-xs"
                  />
                </div>
              </div>
              <div className="grid grid-cols-2 gap-2">
                <div>
                  <Label htmlFor="price_range_min" className="text-xs">
                    Min Price Range
                  </Label>
                  <Input
                    id="price_range_min"
                    type="number"
                    value={formData.price_range_min}
                    onChange={(e) => setFormData({ ...formData, price_range_min: e.target.value })}
                    className="h-8 text-xs"
                  />
                </div>
                <div>
                  <Label htmlFor="price_range_max" className="text-xs">
                    Max Price Range
                  </Label>
                  <Input
                    id="price_range_max"
                    type="number"
                    value={formData.price_range_max}
                    onChange={(e) => setFormData({ ...formData, price_range_max: e.target.value })}
                    className="h-8 text-xs"
                  />
                </div>
              </div>
            </div>

            <div className="space-y-3 rounded-md border p-4">
              <h3 className="text-sm font-medium mb-2">Additional Information</h3>
              <div>
                <Label htmlFor="specialties" className="text-xs">
                  Specialties
                </Label>
                <Input
                  id="specialties"
                  value={formData.specialties}
                  onChange={(e) => setFormData({ ...formData, specialties: e.target.value })}
                  className="h-8 text-xs"
                  placeholder="Luxury Homes, Custom Builds (comma separated)"
                />
              </div>
              <div>
                <Label htmlFor="notes" className="text-xs">
                  Notes
                </Label>
                <Textarea
                  id="notes"
                  value={formData.notes}
                  onChange={(e) => setFormData({ ...formData, notes: e.target.value })}
                  className="text-xs"
                  rows={3}
                />
              </div>
            </div>
          </div>
          <DialogFooter className="pt-6">
            <DialogClose asChild>
              <Button type="button" variant="outline">
                Cancel
              </Button>
            </DialogClose>
            <Button type="submit" disabled={loading}>
              {loading ? <Loader2 className="mr-2 h-4 w-4 animate-spin" /> : <Save className="mr-2 h-4 w-4" />}
              {builder?.id ? "Save Changes" : "Create Builder"}
            </Button>
          </DialogFooter>
        </form>
      </DialogContent>
    </Dialog>
  )
}
```

## File: dkl-microapp-2-main/components/editable-field.tsx
```typescript
"use client"

import type React from "react"

import { useState, useEffect, useRef } from "react"
import { Input } from "@/components/ui/input"
import { Textarea } from "@/components/ui/textarea"
import { Button } from "@/components/ui/button"
import { Check, Edit3, X, Loader2 } from "lucide-react"

interface EditableFieldProps {
  initialValue: string
  onSave: (newValue: string) => Promise<void>
  label: string
  as?: "input" | "textarea"
  inputClassName?: string
  textClassName?: string
  placeholder?: string
}

export function EditableField({
  initialValue,
  onSave,
  label,
  as = "input",
  inputClassName = "",
  textClassName = "",
  placeholder = "Not set",
}: EditableFieldProps) {
  const [isEditing, setIsEditing] = useState(false)
  const [value, setValue] = useState(initialValue)
  const [isLoading, setIsLoading] = useState(false)
  const inputRef = useRef<HTMLInputElement | HTMLTextAreaElement>(null)

  useEffect(() => {
    setValue(initialValue)
  }, [initialValue])

  useEffect(() => {
    if (isEditing && inputRef.current) {
      inputRef.current.focus()
      if (as === "input" && typeof (inputRef.current as HTMLInputElement).select === "function") {
        ;(inputRef.current as HTMLInputElement).select()
      }
    }
  }, [isEditing, as])

  const handleSave = async () => {
    if (value === initialValue && !isEditing) {
      // ensure not to save if not edited or already saved
      setIsEditing(false)
      return
    }
    if (value === initialValue && isEditing) {
      // if value is same as initial, just close edit mode
      setIsEditing(false)
      return
    }

    setIsLoading(true)
    try {
      await onSave(value)
      setIsEditing(false) // Close edit mode on successful save
    } catch (error) {
      console.error(`Failed to save ${label}:`, error)
      // Optionally, revert value or show error to user
      // setValue(initialValue); // Revert to initial value on error
    } finally {
      setIsLoading(false)
    }
  }

  const handleCancel = () => {
    setValue(initialValue)
    setIsEditing(false)
  }

  if (isEditing) {
    return (
      <div className="space-y-1 w-full">
        {as === "input" ? (
          <Input
            ref={inputRef as React.RefObject<HTMLInputElement>}
            type="text"
            value={value}
            onChange={(e) => setValue(e.target.value)}
            className={`h-8 text-sm ${inputClassName}`}
            disabled={isLoading}
            onKeyDown={(e) => {
              if (e.key === "Enter" && !e.shiftKey) {
                e.preventDefault()
                handleSave()
              }
              if (e.key === "Escape") handleCancel()
            }}
          />
        ) : (
          <Textarea
            ref={inputRef as React.RefObject<HTMLTextAreaElement>}
            value={value}
            onChange={(e) => setValue(e.target.value)}
            className={`text-sm min-h-[60px] ${inputClassName}`}
            disabled={isLoading}
            onKeyDown={(e) => {
              if (e.key === "Escape") handleCancel()
            }}
          />
        )}
        <div className="flex items-center space-x-1 pt-1">
          <Button
            variant="ghost"
            size="iconSm"
            onClick={handleSave}
            disabled={isLoading}
            className="h-6 w-6 text-green-600 hover:text-green-700"
            aria-label="Save change"
          >
            {isLoading ? <Loader2 className="h-4 w-4 animate-spin" /> : <Check className="h-4 w-4" />}
          </Button>
          <Button
            variant="ghost"
            size="iconSm"
            onClick={handleCancel}
            disabled={isLoading}
            className="h-6 w-6 text-red-600 hover:text-red-700"
            aria-label="Cancel change"
          >
            <X className="h-4 w-4" />
          </Button>
        </div>
      </div>
    )
  }

  return (
    <div
      className={`group flex items-center cursor-pointer hover:bg-gray-100/50 dark:hover:bg-gray-800/50 p-1 -m-1 rounded transition-colors w-full ${textClassName}`}
      onClick={() => setIsEditing(true)}
      role="button"
      tabIndex={0}
      onKeyDown={(e) => {
        if (e.key === "Enter" || e.key === " ") {
          e.preventDefault()
          setIsEditing(true)
        }
      }}
      aria-label={`Edit ${label}`}
    >
      <span className={`flex-grow text-sm ${!initialValue && "text-muted-foreground"}`}>
        {initialValue || placeholder}
      </span>
      <Edit3 className="h-3 w-3 ml-2 text-muted-foreground opacity-0 group-hover:opacity-100 transition-opacity flex-shrink-0" />
    </div>
  )
}
```

## File: dkl-microapp-2-main/components/field-mapping-sheet.tsx
```typescript
"use client"
import { useState, useEffect } from "react"
import {
  Sheet,
  SheetContent,
  SheetHeader,
  SheetTitle,
  SheetDescription,
  SheetFooter,
  SheetClose,
} from "@/components/ui/sheet"
import { Button } from "@/components/ui/button"
import { Label } from "@/components/ui/label"
import { ScrollArea } from "@/components/ui/scroll-area"
import { Command, CommandEmpty, CommandGroup, CommandInput, CommandItem, CommandList } from "@/components/ui/command"
import { Popover, PopoverContent, PopoverTrigger } from "@/components/ui/popover"
import { Check, ChevronsUpDown } from "lucide-react"
import { cn } from "@/lib/utils"
import type { ListingFieldDefinition, MappedDbColumn } from "@/lib/listing-fields"

interface FieldMappingSheetProps {
  isOpen: boolean
  onClose: () => void
  csvHeaders: string[]
  currentMappings: Record<string, MappedDbColumn>
  onSaveMappings: (mappings: Record<string, MappedDbColumn>) => void
  availableDbColumns: readonly ListingFieldDefinition[]
}

const IGNORE_FIELD_VALUE: MappedDbColumn = "ignore_field"
const IGNORE_FIELD_LABEL = "Ignore this field"

export function FieldMappingSheet({
  isOpen,
  onClose,
  csvHeaders,
  currentMappings,
  onSaveMappings,
  availableDbColumns,
}: FieldMappingSheetProps) {
  const [tempMappings, setTempMappings] = useState<Record<string, MappedDbColumn>>(currentMappings)
  const [popoverOpenStates, setPopoverOpenStates] = useState<Record<string, boolean>>({})

  useEffect(() => {
    setTempMappings(currentMappings)
  }, [isOpen, currentMappings])

  const handleMappingChange = (csvHeader: string, newDbCol: MappedDbColumn) => {
    setTempMappings((prev) => ({ ...prev, [csvHeader]: newDbCol }))
    setPopoverOpenStates((prev) => ({ ...prev, [csvHeader]: false }))
  }

  const handleSave = () => {
    onSaveMappings(tempMappings)
    onClose()
  }

  const getDisplayLabel = (value: MappedDbColumn): string => {
    if (value === IGNORE_FIELD_VALUE) {
      return IGNORE_FIELD_LABEL
    }
    const foundColumn = availableDbColumns.find((col) => col.value === value)
    return foundColumn ? `${foundColumn.label} (${foundColumn.value})` : "Select database field..."
  }

  return (
    <Sheet open={isOpen} onOpenChange={(open) => !open && onClose()}>
      <SheetContent className="sm:max-w-lg w-[90vw] flex flex-col">
        <SheetHeader>
          <SheetTitle>Map CSV Fields to Database Columns</SheetTitle>
          <SheetDescription>
            Review and adjust how your CSV fields correspond to the listing database fields. Unmapped fields or fields
            set to "Ignore" will not be imported.
          </SheetDescription>
        </SheetHeader>
        <ScrollArea className="flex-grow py-4 pr-2">
          <div className="space-y-4 pr-4">
            {csvHeaders.map((header) => (
              <div key={header} className="grid grid-cols-2 gap-4 items-center">
                <Label htmlFor={`map-${header}`} className="truncate text-sm font-medium">
                  {header}
                </Label>
                <Popover
                  open={popoverOpenStates[header] || false}
                  onOpenChange={(isOpenState) => setPopoverOpenStates((prev) => ({ ...prev, [header]: isOpenState }))}
                >
                  <PopoverTrigger asChild>
                    <Button
                      variant="outline"
                      role="combobox"
                      aria-expanded={popoverOpenStates[header] || false}
                      className="w-full justify-between"
                      id={`map-${header}`}
                    >
                      <span className="truncate">{getDisplayLabel(tempMappings[header] || IGNORE_FIELD_VALUE)}</span>
                      <ChevronsUpDown className="ml-2 h-4 w-4 shrink-0 opacity-50" />
                    </Button>
                  </PopoverTrigger>
                  <PopoverContent className="w-[--radix-popover-trigger-width] p-0 max-h-[--radix-popover-content-available-height]">
                    <Command>
                      <CommandInput placeholder="Search field..." />
                      <CommandEmpty>No field found.</CommandEmpty>
                      <CommandList>
                        <CommandGroup>
                          <CommandItem
                            key={IGNORE_FIELD_VALUE}
                            value={IGNORE_FIELD_VALUE}
                            onSelect={() => handleMappingChange(header, IGNORE_FIELD_VALUE)}
                          >
                            <Check
                              className={cn(
                                "mr-2 h-4 w-4",
                                (tempMappings[header] || IGNORE_FIELD_VALUE) === IGNORE_FIELD_VALUE
                                  ? "opacity-100"
                                  : "opacity-0",
                              )}
                            />
                            {IGNORE_FIELD_LABEL}
                          </CommandItem>
                          {availableDbColumns.map((col) => {
                            const isOptionSelectedByCurrentHeader = tempMappings[header] === col.value
                            const isOptionTakenByAnotherHeader = Object.entries(tempMappings).some(
                              ([otherCsvHeader, mappedDbCol]) =>
                                otherCsvHeader !== header &&
                                mappedDbCol === col.value &&
                                mappedDbCol !== "ignore_field",
                            )
                            return (
                              <CommandItem
                                key={col.value}
                                value={col.value}
                                onSelect={() => {
                                  if (!(isOptionTakenByAnotherHeader && !isOptionSelectedByCurrentHeader)) {
                                    handleMappingChange(header, col.value as MappedDbColumn)
                                  }
                                }}
                                disabled={isOptionTakenByAnotherHeader && !isOptionSelectedByCurrentHeader}
                                className={cn(
                                  isOptionTakenByAnotherHeader &&
                                    !isOptionSelectedByCurrentHeader &&
                                    "opacity-50 cursor-not-allowed",
                                )}
                              >
                                <Check
                                  className={cn(
                                    "mr-2 h-4 w-4",
                                    isOptionSelectedByCurrentHeader ? "opacity-100" : "opacity-0",
                                  )}
                                />
                                {col.label} ({col.value})
                                {isOptionTakenByAnotherHeader && !isOptionSelectedByCurrentHeader && (
                                  <span className="ml-auto text-xs text-muted-foreground">(In use)</span>
                                )}
                              </CommandItem>
                            )
                          })}
                        </CommandGroup>
                      </CommandList>
                    </Command>
                  </PopoverContent>
                </Popover>
              </div>
            ))}
          </div>
        </ScrollArea>
        <SheetFooter className="mt-auto pt-4 border-t">
          <SheetClose asChild>
            <Button variant="outline" onClick={onClose}>
              Cancel
            </Button>
          </SheetClose>
          <Button onClick={handleSave}>Save Mappings</Button>
        </SheetFooter>
      </SheetContent>
    </Sheet>
  )
}
```

## File: dkl-microapp-2-main/components/header.tsx
```typescript
"use client"

import { UserNav } from "@/components/user-nav"
import { Input } from "@/components/ui/input"
import { Search } from "lucide-react"

export function Header() {
  return (
    <header className="sticky top-0 z-50 flex h-12 items-center justify-between border-b bg-background px-4">
      <div className="flex items-center gap-x-4">
        <div className="text-sm font-semibold">Real Estate Market Analysis</div>
      </div>
      <div className="flex items-center gap-x-4">
        <div className="relative">
          <Search className="absolute left-2.5 top-2.5 h-4 w-4 text-muted-foreground" />
          <Input type="search" placeholder="Search..." className="w-64 rounded-md pl-8 attio-input" />
        </div>
        <UserNav />
      </div>
    </header>
  )
}
```

## File: dkl-microapp-2-main/components/listing-form-dialog.tsx
```typescript
"use client"

import type React from "react"
import { useState, useEffect } from "react"
import { supabase } from "@/lib/supabase/client"
import { Button } from "@/components/ui/button"
import { Input } from "@/components/ui/input"
import { Label } from "@/components/ui/label"
import { Select, SelectContent, SelectItem, SelectTrigger, SelectValue } from "@/components/ui/select"
import { Checkbox } from "@/components/ui/checkbox"
import {
  Dialog,
  DialogContent,
  DialogHeader,
  DialogTitle,
  DialogDescription,
  DialogFooter,
  DialogClose,
} from "@/components/ui/dialog"
import { useToast } from "@/hooks/use-toast"
import { Save, Loader2 } from "lucide-react"
import type { Database } from "@/types/supabase"

type Builder = Database["public"]["Tables"]["builders"]["Row"]
type Listing = Database["public"]["Tables"]["listings"]["Row"] // Changed from Property

interface ListingFormDialogProps {
  open: boolean
  onOpenChange: (open: boolean) => void
  onListingCreated: () => void // Renamed from onPropertyCreated
  listing?: Partial<Listing> // Changed from Property
}

const initialFormData = {
  mls_number: "",
  status: "Active",
  list_price: "",
  street_number: "",
  street_name: "",
  city: "",
  state: "",
  zip_code: "",
  bedrooms: "",
  baths_full: "",
  baths_half: "",
  interior_sqft: "",
  new_construction: false,
  builder_id: "",
  property_condition: "",
  garage_spaces: "",
  fireplace: false,
  central_air: false,
  basement: false,
  // Add any other relevant fields from your 'listings' table
}

export function ListingFormDialog({ open, onOpenChange, onListingCreated, listing }: ListingFormDialogProps) {
  // Renamed component
  const { toast } = useToast()
  const [builders, setBuilders] = useState<Builder[]>([])
  const [loading, setLoading] = useState(false)
  const [formData, setFormData] = useState(initialFormData)

  useEffect(() => {
    fetchBuilders()
  }, [])

  useEffect(() => {
    if (listing && open) {
      setFormData({
        mls_number: listing.mls_number || "",
        status: listing.status || "Active",
        list_price: listing.list_price?.toString() || "",
        street_number: listing.street_number || "",
        street_name: listing.street_name || "",
        city: listing.city || "",
        state: listing.state || "",
        zip_code: listing.zip_code || "",
        bedrooms: listing.bedrooms?.toString() || "",
        baths_full: listing.baths_full?.toString() || "",
        baths_half: listing.baths_half?.toString() || "",
        interior_sqft: listing.interior_sqft?.toString() || "",
        new_construction: listing.new_construction || false,
        builder_id: listing.builder_id || "",
        property_condition: listing.property_condition || "",
        garage_spaces: listing.garage_spaces?.toString() || "",
        fireplace: listing.fireplace || false,
        central_air: listing.central_air || false,
        basement: listing.basement || false,
        // Map other fields from listing to formData as needed
      })
    } else if (!listing && open) {
      setFormData(initialFormData)
    }
  }, [listing, open])

  async function fetchBuilders() {
    try {
      const { data } = await supabase.from("builders").select("id, name, company_name").order("name")
      setBuilders(data || [])
    } catch (error) {
      console.error("Error fetching builders:", error)
      toast({ title: "Error", description: "Could not fetch builders.", variant: "destructive" })
    }
  }

  const handleSubmit = async (e: React.FormEvent) => {
    e.preventDefault()
    setLoading(true)

    try {
      const listingData = {
        // Renamed from propertyData
        ...formData,
        list_price: formData.list_price ? Number.parseFloat(formData.list_price) : null,
        bedrooms: formData.bedrooms ? Number.parseInt(formData.bedrooms) : null,
        baths_full: formData.baths_full ? Number.parseInt(formData.baths_full) : null,
        baths_half: formData.baths_half ? Number.parseInt(formData.baths_half) : null,
        interior_sqft: formData.interior_sqft ? Number.parseInt(formData.interior_sqft) : null,
        garage_spaces: formData.garage_spaces ? Number.parseInt(formData.garage_spaces) : null,
        builder_id: formData.builder_id || null,
        list_date: listing?.list_date || new Date().toISOString().split("T")[0],
      }

      // eslint-disable-next-line @typescript-eslint/no-unused-vars
      const { id, created_at, updated_at, ...upsertData } = listingData as Partial<Listing> & {
        id?: string
        created_at?: string
        updated_at?: string
      }

      const { error } = await supabase
        .from("listings") // Changed from "properties"
        .upsert(listing?.id ? { ...upsertData, id: listing.id } : upsertData)

      if (error) throw error

      toast({
        title: listing?.id ? "Listing Updated" : "Listing Created",
        description: `Listing has been successfully ${listing?.id ? "updated" : "added"}.`,
      })
      onListingCreated() // Call the renamed prop
      onOpenChange(false)
    } catch (error: any) {
      toast({
        title: "Error",
        description: error.message || `Failed to ${listing?.id ? "update" : "create"} listing.`,
        variant: "destructive",
      })
    } finally {
      setLoading(false)
    }
  }

  return (
    <Dialog open={open} onOpenChange={onOpenChange}>
      <DialogContent className="sm:max-w-[800px] max-h-[90vh] overflow-y-auto">
        <DialogHeader>
          <DialogTitle>{listing?.id ? "Edit Listing" : "Add New Listing"}</DialogTitle>
          <DialogDescription>Fill in the details for the listing. Click save when you're done.</DialogDescription>
        </DialogHeader>
        <form onSubmit={handleSubmit} className="py-4">
          <div className="grid gap-4 lg:grid-cols-2">
            <div className="space-y-3 rounded-md border p-4">
              <h3 className="text-sm font-medium mb-2">Basic Information</h3>
              <div>
                <Label htmlFor="mls_number" className="text-xs">
                  MLS Number *
                </Label>
                <Input
                  id="mls_number"
                  value={formData.mls_number}
                  onChange={(e) => setFormData({ ...formData, mls_number: e.target.value })}
                  className="h-8 text-xs"
                  required
                />
              </div>
              <div>
                <Label htmlFor="status" className="text-xs">
                  Status
                </Label>
                <Select value={formData.status} onValueChange={(value) => setFormData({ ...formData, status: value })}>
                  <SelectTrigger className="h-8 text-xs">
                    <SelectValue />
                  </SelectTrigger>
                  <SelectContent>
                    <SelectItem value="Active">Active</SelectItem>
                    <SelectItem value="Pending">Pending</SelectItem>
                    <SelectItem value="Under Contract">Under Contract</SelectItem>
                    <SelectItem value="Sold">Sold</SelectItem>
                    <SelectItem value="Coming Soon">Coming Soon</SelectItem>
                  </SelectContent>
                </Select>
              </div>
              <div>
                <Label htmlFor="list_price" className="text-xs">
                  List Price
                </Label>
                <Input
                  id="list_price"
                  type="number"
                  value={formData.list_price}
                  onChange={(e) => setFormData({ ...formData, list_price: e.target.value })}
                  className="h-8 text-xs"
                  placeholder="0"
                />
              </div>
              <div>
                <Label htmlFor="builder_id" className="text-xs">
                  Builder
                </Label>
                <Select
                  value={formData.builder_id}
                  onValueChange={(value) =>
                    setFormData({ ...formData, builder_id: value === "no_builder" ? "" : value })
                  }
                >
                  <SelectTrigger className="h-8 text-xs">
                    <SelectValue placeholder="Select builder" />
                  </SelectTrigger>
                  <SelectContent>
                    <SelectItem value="no_builder">No builder</SelectItem>
                    {builders.map((b) => (
                      <SelectItem key={b.id} value={b.id}>
                        {b.name} {b.company_name && `(${b.company_name})`}
                      </SelectItem>
                    ))}
                  </SelectContent>
                </Select>
              </div>
            </div>

            <div className="space-y-3 rounded-md border p-4">
              <h3 className="text-sm font-medium mb-2">Address</h3>
              <div className="grid grid-cols-2 gap-2">
                <div>
                  <Label htmlFor="street_number" className="text-xs">
                    Street Number
                  </Label>
                  <Input
                    id="street_number"
                    value={formData.street_number}
                    onChange={(e) => setFormData({ ...formData, street_number: e.target.value })}
                    className="h-8 text-xs"
                  />
                </div>
                <div>
                  <Label htmlFor="street_name" className="text-xs">
                    Street Name
                  </Label>
                  <Input
                    id="street_name"
                    value={formData.street_name}
                    onChange={(e) => setFormData({ ...formData, street_name: e.target.value })}
                    className="h-8 text-xs"
                  />
                </div>
              </div>
              <div>
                <Label htmlFor="city" className="text-xs">
                  City
                </Label>
                <Input
                  id="city"
                  value={formData.city}
                  onChange={(e) => setFormData({ ...formData, city: e.target.value })}
                  className="h-8 text-xs"
                />
              </div>
              <div className="grid grid-cols-2 gap-2">
                <div>
                  <Label htmlFor="state" className="text-xs">
                    State
                  </Label>
                  <Input
                    id="state"
                    value={formData.state}
                    onChange={(e) => setFormData({ ...formData, state: e.target.value })}
                    className="h-8 text-xs"
                    placeholder="VA"
                  />
                </div>
                <div>
                  <Label htmlFor="zip_code" className="text-xs">
                    Zip Code
                  </Label>
                  <Input
                    id="zip_code"
                    value={formData.zip_code}
                    onChange={(e) => setFormData({ ...formData, zip_code: e.target.value })}
                    className="h-8 text-xs"
                  />
                </div>
              </div>
            </div>

            <div className="space-y-3 rounded-md border p-4">
              <h3 className="text-sm font-medium mb-2">Listing Details</h3> {/* Changed from Property Details */}
              <div className="grid grid-cols-3 gap-2">
                <div>
                  <Label htmlFor="bedrooms" className="text-xs">
                    Bedrooms
                  </Label>
                  <Input
                    id="bedrooms"
                    type="number"
                    value={formData.bedrooms}
                    onChange={(e) => setFormData({ ...formData, bedrooms: e.target.value })}
                    className="h-8 text-xs"
                  />
                </div>
                <div>
                  <Label htmlFor="baths_full" className="text-xs">
                    Full Baths
                  </Label>
                  <Input
                    id="baths_full"
                    type="number"
                    value={formData.baths_full}
                    onChange={(e) => setFormData({ ...formData, baths_full: e.target.value })}
                    className="h-8 text-xs"
                  />
                </div>
                <div>
                  <Label htmlFor="baths_half" className="text-xs">
                    Half Baths
                  </Label>
                  <Input
                    id="baths_half"
                    type="number"
                    value={formData.baths_half}
                    onChange={(e) => setFormData({ ...formData, baths_half: e.target.value })}
                    className="h-8 text-xs"
                  />
                </div>
              </div>
              <div>
                <Label htmlFor="interior_sqft" className="text-xs">
                  Square Feet
                </Label>
                <Input
                  id="interior_sqft"
                  type="number"
                  value={formData.interior_sqft}
                  onChange={(e) => setFormData({ ...formData, interior_sqft: e.target.value })}
                  className="h-8 text-xs"
                />
              </div>
              <div>
                <Label htmlFor="garage_spaces" className="text-xs">
                  Garage Spaces
                </Label>
                <Input
                  id="garage_spaces"
                  type="number"
                  value={formData.garage_spaces}
                  onChange={(e) => setFormData({ ...formData, garage_spaces: e.target.value })}
                  className="h-8 text-xs"
                />
              </div>
            </div>

            <div className="space-y-3 rounded-md border p-4">
              <h3 className="text-sm font-medium mb-2">Features</h3>
              <div className="flex items-center space-x-2">
                <Checkbox
                  id="new_construction"
                  checked={formData.new_construction}
                  onCheckedChange={(checked) => setFormData({ ...formData, new_construction: !!checked })}
                />
                <Label htmlFor="new_construction" className="text-xs font-normal">
                  New Construction
                </Label>
              </div>
              <div className="flex items-center space-x-2">
                <Checkbox
                  id="fireplace"
                  checked={formData.fireplace}
                  onCheckedChange={(checked) => setFormData({ ...formData, fireplace: !!checked })}
                />
                <Label htmlFor="fireplace" className="text-xs font-normal">
                  Fireplace
                </Label>
              </div>
              <div className="flex items-center space-x-2">
                <Checkbox
                  id="central_air"
                  checked={formData.central_air}
                  onCheckedChange={(checked) => setFormData({ ...formData, central_air: !!checked })}
                />
                <Label htmlFor="central_air" className="text-xs font-normal">
                  Central Air
                </Label>
              </div>
              <div className="flex items-center space-x-2">
                <Checkbox
                  id="basement"
                  checked={formData.basement}
                  onCheckedChange={(checked) => setFormData({ ...formData, basement: !!checked })}
                />
                <Label htmlFor="basement" className="text-xs font-normal">
                  Basement
                </Label>
              </div>
            </div>
          </div>
          <DialogFooter className="pt-6">
            <DialogClose asChild>
              <Button type="button" variant="outline">
                Cancel
              </Button>
            </DialogClose>
            <Button type="submit" disabled={loading}>
              {loading ? <Loader2 className="mr-2 h-4 w-4 animate-spin" /> : <Save className="mr-2 h-4 w-4" />}
              {listing?.id ? "Save Changes" : "Create Listing"}
            </Button>
          </DialogFooter>
        </form>
      </DialogContent>
    </Dialog>
  )
}
```

## File: dkl-microapp-2-main/components/main-nav.tsx
```typescript
"use client"

import Link from "next/link"
import { usePathname } from "next/navigation"
import { cn } from "@/lib/utils"
import {
  BarChart3,
  Building2,
  Home,
  Settings,
  Upload,
  Users,
  TrendingUp,
  FileText,
  Share2,
  Palette,
} from "lucide-react"

const navItems = [
  {
    name: "Dashboard",
    href: "/dashboard",
    icon: Home,
  },
  {
    name: "Listings",
    href: "/listings",
    icon: Building2,
  },
  {
    name: "Builders",
    href: "/builders",
    icon: Users,
  },
  {
    name: "Social Posts",
    href: "/social",
    icon: Share2,
  },
  {
    name: "Market Insights",
    href: "/insights",
    icon: TrendingUp,
  },
  {
    name: "Reports",
    href: "/reports",
    icon: FileText,
  },
  {
    name: "Analytics",
    href: "/analytics",
    icon: BarChart3,
  },
  {
    name: "Data Import",
    href: "/import",
    icon: Upload,
  },
  // This is the new item
  {
    name: "Style Guide",
    href: "/style-guide",
    icon: Palette,
  },
  {
    name: "Settings",
    href: "/settings",
    icon: Settings,
  },
]

export function MainNav() {
  const pathname = usePathname()

  return (
    <nav className="flex flex-col space-y-1">
      {navItems.map((item) => {
        const isActive = pathname === item.href || pathname?.startsWith(`${item.href}/`)
        const Icon = item.icon

        return (
          <Link
            key={item.href}
            href={item.href}
            className={cn(
              "flex items-center gap-x-2 rounded-md px-3 py-2 text-xs font-medium",
              isActive ? "bg-primary/10 text-primary" : "text-muted-foreground hover:bg-muted hover:text-foreground",
            )}
          >
            <Icon className="h-4 w-4" />
            <span>{item.name}</span>
          </Link>
        )
      })}
    </nav>
  )
}
```

## File: dkl-microapp-2-main/components/mapbox-map.tsx
```typescript
"use client"

import type React from "react"
import { useEffect, useRef, useState } from "react"
import mapboxgl, { type Map } from "mapbox-gl" // ES6 import
import { Loader2, AlertTriangle } from "lucide-react"

// Update the MappableProperty interface to include additional fields for the popup
export interface MappableListing {
  id: string
  address_line_1: string | null
  city: string | null
  state: string | null
  latitude?: number | null
  longitude?: number | null
  status?: string | null
  list_price?: number | null
  builder_name?: string | null
  [key: string]: any // Allow other listing fields
}

interface MapboxMapProps {
  userApiKey: string | null // API key from user settings
  properties: MappableListing[]
  initialViewState?: {
    longitude: number
    latitude: number
    zoom: number
  }
  className?: string
}

const FALLBACK_MAPBOX_TOKEN = process.env.NEXT_PUBLIC_MAPBOX_ACCESS_TOKEN

// Update the MapboxMap component to use a flat projection, limit to DC area, and add popups
const MapboxMap: React.FC<MapboxMapProps> = ({ userApiKey, properties, initialViewState, className }) => {
  const mapContainer = useRef<HTMLDivElement | null>(null)
  const map = useRef<Map | null>(null)
  const [isLoading, setIsLoading] = useState(true)
  const [error, setError] = useState<string | null>(null)
  const [currentMarkers, setCurrentMarkers] = useState<mapboxgl.Marker[]>([])
  const [currentPopups, setCurrentPopups] = useState<mapboxgl.Popup[]>([])

  const effectiveApiKey = userApiKey || FALLBACK_MAPBOX_TOKEN

  // Washington DC coordinates
  const DC_CENTER = [-77.0369, 38.9072]
  const DC_BOUNDS = [
    [-77.4369, 38.5072], // Southwest coordinates (roughly 20 miles from center)
    [-76.6369, 39.3072], // Northeast coordinates (roughly 20 miles from center)
  ]

  // Get color based on listing status
  const getStatusColor = (status: string | null): string => {
    switch (status?.toLowerCase()) {
      case "active":
        return "#10b981" // green
      case "pending":
        return "#f59e0b" // yellow/amber
      case "sold":
        return "#3b82f6" // blue
      case "under contract":
        return "#8b5cf6" // purple
      case "coming soon":
        return "#f97316" // orange
      default:
        return "#6b7280" // gray
    }
  }

  // Format price for popup
  const formatPrice = (price: number | null | undefined): string => {
    if (price == null) return "Price not available"
    return new Intl.NumberFormat("en-US", {
      style: "currency",
      currency: "USD",
      maximumFractionDigits: 0,
    }).format(price)
  }

  useEffect(() => {
    if (!effectiveApiKey) {
      setError("Mapbox Access Token is not configured. Please set it in settings or as an environment variable.")
      setIsLoading(false)
      return
    }

    if (!mapContainer.current) {
      setError("Map container not found.")
      setIsLoading(false)
      return
    }

    if (map.current) return // Initialize map only once

    mapboxgl.accessToken = effectiveApiKey

    try {
      map.current = new mapboxgl.Map({
        container: mapContainer.current,
        style: "mapbox://styles/mapbox/light-v11", // Minimalist style
        center: DC_CENTER, // Center on Washington DC
        zoom: 10, // Default zoom level
        maxBounds: DC_BOUNDS, // Restrict panning to DC area
        minZoom: 9, // Restrict zooming out too far
      })

      map.current.addControl(new mapboxgl.NavigationControl(), "top-right")

      map.current.on("load", () => {
        setIsLoading(false)
      })

      map.current.on("error", (e) => {
        console.error("Mapbox GL error:", e.error?.message || e)
        setError(`Mapbox error: ${e.error?.message || "Unknown map error"}`)
        setIsLoading(false)
      })
    } catch (e: any) {
      console.error("Failed to initialize Mapbox map:", e)
      setError(`Failed to initialize map: ${e.message}`)
      setIsLoading(false)
    }

    return () => {
      map.current?.remove()
      map.current = null
    }
  }, [effectiveApiKey])

  useEffect(() => {
    // Guard: If map instance doesn't exist or is still in its initial loading phase.
    if (!map.current || isLoading) {
      // It's too early to do anything with markers.
      // If there were old markers and the map is re-initializing or properties cleared,
      // ensure markers are cleared.
      if (currentMarkers.length > 0) {
        currentMarkers.forEach((marker) => marker.remove())
        setCurrentMarkers([])
      }

      // Also clear any popups
      if (currentPopups.length > 0) {
        currentPopups.forEach((popup) => popup.remove())
        setCurrentPopups([])
      }
      return
    }

    // At this point, map.current exists and isLoading is false (map has loaded).

    // Clear all previously added markers and popups from the map.
    currentMarkers.forEach((marker) => marker.remove())
    currentPopups.forEach((popup) => popup.remove())

    if (!properties || properties.length === 0) {
      setCurrentMarkers([])
      setCurrentPopups([])
      return
    }

    const geocodePromises: Promise<mapboxgl.Marker | null>[] = []
    const newMarkersFromLatLon: mapboxgl.Marker[] = []
    const newPopups: mapboxgl.Popup[] = []
    const bounds = new mapboxgl.LngLatBounds()

    properties.forEach((listing) => {
      if (listing.latitude && listing.longitude) {
        // Create popup for this listing
        const popup = new mapboxgl.Popup({ offset: 25, closeButton: false }).setHTML(`
            <div class="p-2">
              <p class="font-medium">${listing.address_line_1 || ""}, ${listing.city || ""}, ${listing.state || ""}</p>
              <p class="text-sm text-gray-600">Status: <span class="font-medium">${listing.status || "N/A"}</span></p>
              <p class="text-sm text-gray-600">Builder: <span class="font-medium">${listing.builder_name || "N/A"}</span></p>
              <p class="text-sm text-gray-600">Price: <span class="font-medium">${formatPrice(listing.list_price)}</span></p>
            </div>
          `)

        newPopups.push(popup)

        // Create a custom marker element
        const el = document.createElement("div")
        el.className = "custom-marker"
        el.style.backgroundColor = getStatusColor(listing.status)
        el.style.width = "12px"
        el.style.height = "12px"
        el.style.borderRadius = "50%"
        el.style.border = "2px solid white"
        el.style.boxShadow = "0 0 2px rgba(0,0,0,0.3)"

        // Create the marker
        const marker = new mapboxgl.Marker(el).setLngLat([listing.longitude, listing.latitude]).setPopup(popup) // Attach popup to marker

        newMarkersFromLatLon.push(marker)
        bounds.extend([listing.longitude, listing.latitude])
      } else if (listing.address_line_1 && listing.city && listing.state && effectiveApiKey) {
        const query = `${listing.address_line_1}, ${listing.city}, ${listing.state}`
        const geocodeUrl = `https://api.mapbox.com/geocoding/v5/mapbox.places/${encodeURIComponent(
          query,
        )}.json?access_token=${effectiveApiKey}&limit=1`

        geocodePromises.push(
          fetch(geocodeUrl)
            .then((response) => response.json())
            .then((data) => {
              if (data.features && data.features.length > 0) {
                const [lng, lat] = data.features[0].center

                // Create popup for this listing
                const popup = new mapboxgl.Popup({ offset: 25, closeButton: false }).setHTML(`
                    <div class="p-2">
                      <p class="font-medium">${listing.address_line_1 || ""}, ${listing.city || ""}, ${listing.state || ""}</p>
                      <p class="text-sm text-gray-600">Status: <span class="font-medium">${listing.status || "N/A"}</span></p>
                      <p class="text-sm text-gray-600">Builder: <span class="font-medium">${listing.builder_name || "N/A"}</span></p>
                      <p class="text-sm text-gray-600">Price: <span class="font-medium">${formatPrice(listing.list_price)}</span></p>
                    </div>
                  `)

                newPopups.push(popup)

                // Create a custom marker element
                const el = document.createElement("div")
                el.className = "custom-marker"
                el.style.backgroundColor = getStatusColor(listing.status)
                el.style.width = "12px"
                el.style.height = "12px"
                el.style.borderRadius = "50%"
                el.style.border = "2px solid white"
                el.style.boxShadow = "0 0 2px rgba(0,0,0,0.3)"

                // Create the marker
                const marker = new mapboxgl.Marker(el).setLngLat([lng, lat]).setPopup(popup) // Attach popup to marker

                bounds.extend([lng, lat])
                return marker
              }
              console.warn(`Geocoding failed for: ${query}`)
              return null
            })
            .catch((err) => {
              console.error(`Geocoding error for ${query}:`, err)
              return null
            }),
        )
      }
    })

    Promise.all(geocodePromises).then((resolvedGeocodedMarkers) => {
      const allMarkersToAdd: mapboxgl.Marker[] = [...newMarkersFromLatLon]
      const validGeocodedMarkers = resolvedGeocodedMarkers.filter(Boolean) as mapboxgl.Marker[]
      allMarkersToAdd.push(...validGeocodedMarkers)

      if (map.current && allMarkersToAdd.length > 0) {
        allMarkersToAdd.forEach((marker) => marker.addTo(map.current!))

        // Only fit bounds if we have markers and they're within our DC area
        if (!bounds.isEmpty()) {
          // Ensure we don't zoom out beyond our restricted area
          map.current.fitBounds(bounds, {
            padding: 50,
            maxZoom: 15,
            duration: 1000,
            // Ensure we don't go beyond our DC bounds
            bounds: DC_BOUNDS,
          })
        }
      }

      setCurrentMarkers(allMarkersToAdd)
      setCurrentPopups(newPopups)
    })
  }, [properties, effectiveApiKey, isLoading])

  return (
    <div className={`relative w-full h-full min-h-[300px] ${className || ""}`}>
      <div ref={mapContainer} className="absolute top-0 bottom-0 w-full h-full" />
      {isLoading && (
        <div className="absolute inset-0 flex items-center justify-center bg-white/50 backdrop-blur-sm z-10">
          <Loader2 className="h-8 w-8 animate-spin text-primary" />
          <p className="ml-2">Loading map...</p>
        </div>
      )}
      {!isLoading && error && (
        <div className="absolute inset-0 flex flex-col items-center justify-center bg-red-50 p-4 z-10">
          <AlertTriangle className="h-8 w-8 text-red-500 mb-2" />
          <p className="text-red-700 text-center text-sm">{error}</p>
          {error.includes("Access Token") && (
            <p className="text-xs text-red-600 mt-1 text-center">
              Please verify your Mapbox Access Token in Settings &gt; Integrations.
            </p>
          )}
        </div>
      )}
    </div>
  )
}

export default MapboxMap
```

## File: dkl-microapp-2-main/components/pill-input.tsx
```typescript
"use client"

import { useState, type KeyboardEvent } from "react"
import { Input } from "@/components/ui/input"
import { Button } from "@/components/ui/button"
import { Badge } from "@/components/ui/badge"
import { XIcon } from "lucide-react"
import { cn } from "@/lib/utils"

interface PillInputProps {
  value: string[]
  onChange: (newValue: string[]) => void
  placeholder?: string
  className?: string
  maxPills?: number
}

export function PillInput({ value = [], onChange, placeholder = "Add item...", className, maxPills }: PillInputProps) {
  const [inputValue, setInputValue] = useState("")

  const handleAddPill = () => {
    const newPill = inputValue.trim()
    if (newPill && !value.includes(newPill) && (!maxPills || value.length < maxPills)) {
      onChange([...value, newPill])
      setInputValue("")
    }
  }

  const handleRemovePill = (pillToRemove: string) => {
    onChange(value.filter((pill) => pill !== pillToRemove))
  }

  const handleKeyDown = (event: KeyboardEvent<HTMLInputElement>) => {
    if (event.key === "Enter") {
      event.preventDefault()
      handleAddPill()
    } else if (event.key === "Backspace" && inputValue === "" && value.length > 0) {
      handleRemovePill(value[value.length - 1])
    }
  }

  return (
    <div className={cn("space-y-2", className)}>
      <div className="flex flex-wrap gap-2 mb-2">
        {value.map((pill) => (
          <Badge key={pill} variant="secondary" className="flex items-center gap-1">
            {pill}
            <button
              type="button"
              onClick={() => handleRemovePill(pill)}
              className="rounded-full hover:bg-muted-foreground/20 p-0.5"
              aria-label={`Remove ${pill}`}
            >
              <XIcon className="h-3 w-3" />
            </button>
          </Badge>
        ))}
      </div>
      {(!maxPills || value.length < maxPills) && (
        <div className="flex gap-2">
          <Input
            type="text"
            value={inputValue}
            onChange={(e) => setInputValue(e.target.value)}
            onKeyDown={handleKeyDown}
            placeholder={placeholder}
            className="attio-input flex-grow"
          />
          <Button type="button" onClick={handleAddPill} variant="outline" size="sm">
            Add
          </Button>
        </div>
      )}
      {maxPills && value.length >= maxPills && (
        <p className="text-xs text-muted-foreground">Maximum number of items reached.</p>
      )}
    </div>
  )
}
```

## File: dkl-microapp-2-main/components/sidebar.tsx
```typescript
import { MainNav } from "@/components/main-nav"

export function Sidebar() {
  return (
    <aside className="fixed inset-y-0 left-0 z-40 hidden w-48 flex-col border-r bg-background md:flex">
      <div className="flex h-12 items-center border-b px-4">
        <div className="flex items-center gap-x-2">
          <div className="h-6 w-6 rounded-md bg-primary" />
          <span className="text-sm font-semibold">RE Market</span>
        </div>
      </div>
      <div className="flex-1 overflow-auto py-4 px-3">
        <MainNav />
      </div>
    </aside>
  )
}
```

## File: dkl-microapp-2-main/components/social-post-property-item.tsx
```typescript
"use client"

import { useState, useEffect, type ChangeEvent } from "react"
import { supabase } from "@/lib/supabase/client"
import type { Database } from "@/types/supabase"
import { Button } from "@/components/ui/button"
import { Checkbox } from "@/components/ui/checkbox"
import { Input } from "@/components/ui/input"
import { Textarea } from "@/components/ui/textarea"
import { toast } from "@/hooks/use-toast"
import { ChevronDown, ChevronUp, Plus, XIcon, ImageIcon, AlertTriangle, Loader2, Wand2 } from "lucide-react"
import { cn } from "@/lib/utils"
import { Popover, PopoverContent, PopoverTrigger } from "@/components/ui/popover"
import { Dialog, DialogContent, DialogHeader, DialogTitle, DialogFooter } from "@/components/ui/dialog"
import { Label } from "@/components/ui/label"
import { generateDescriptionWithAI } from "@/app/actions/ai-actions"

type SocialPostProperty = Database["public"]["Tables"]["social_post_properties"]["Row"] & {
  properties: Database["public"]["Tables"]["listings"]["Row"] | null
}

interface SocialPostPropertyItemProps {
  item: SocialPostProperty
  postId: string
  onUpdate: (updatedItem: Partial<SocialPostProperty>) => void
}

const formatCurrency = (amount: number | null) => {
  if (amount === null || amount === undefined) return "N/A"
  return new Intl.NumberFormat("en-US", {
    style: "currency",
    currency: "USD",
    minimumFractionDigits: 0,
    maximumFractionDigits: 0,
  }).format(amount)
}

const IMAGE_BUCKET_NAME = "social-post-images"

export function SocialPostPropertyItem({ item, postId, onUpdate }: SocialPostPropertyItemProps) {
  const [isExpanded, setIsExpanded] = useState(true) // Default to expanded
  const [contacted, setContacted] = useState(item.contacted_complete)
  const [imageComplete, setImageComplete] = useState(item.image_complete)
  const [descriptionComplete, setDescriptionComplete] = useState(item.description_complete)

  const [propertyDescription, setPropertyDescription] = useState(item.description || "")
  const [imageUrls, setImageUrls] = useState<string[]>(item.image_urls || [])
  const [isUploading, setIsUploading] = useState(false)
  const [isSavingDesc, setIsSavingDesc] = useState(false)

  const [showPromptDialog, setShowPromptDialog] = useState(false)
  const [aiPrompt, setAiPrompt] = useState("")
  const [isGenerating, setIsGenerating] = useState(false)

  const property = item.properties

  useEffect(() => {
    setContacted(item.contacted_complete)
    setImageComplete(item.image_complete)
    setDescriptionComplete(item.description_complete)
    setPropertyDescription(item.description || "")
    setImageUrls(item.image_urls || [])
  }, [item])

  const handleCheckboxChange = async (
    field: "contacted_complete" | "image_complete" | "description_complete",
    value: boolean,
  ) => {
    if (!item.id) return
    const { error } = await supabase
      .from("social_post_properties")
      .update({ [field]: value })
      .eq("id", item.id)

    if (error) {
      toast({ title: "Error updating status", description: error.message, variant: "destructive" })
    } else {
      if (field === "contacted_complete") setContacted(value)
      if (field === "image_complete") setImageComplete(value)
      if (field === "description_complete") setDescriptionComplete(value)
      onUpdate({ id: item.id, [field]: value })
    }
  }

  const handlePropertyDescriptionSave = async (descriptionToSave?: string) => {
    if (!item.id) return
    const currentDesc = descriptionToSave !== undefined ? descriptionToSave : propertyDescription
    setIsSavingDesc(true)
    try {
      const { error } = await supabase
        .from("social_post_properties")
        .update({ description: currentDesc })
        .eq("id", item.id)

      if (error) {
        toast({ title: "Error saving description", description: error.message, variant: "destructive" })
      } else {
        toast({ title: "Description Saved", description: "Listing-specific description has been updated." })
        onUpdate({ id: item.id, description: currentDesc })
        if (descriptionToSave !== undefined) {
          setPropertyDescription(currentDesc)
        }
      }
    } catch (e: any) {
      toast({ title: "Error", description: e.message || "Could not save description.", variant: "destructive" })
    } finally {
      setIsSavingDesc(false)
    }
  }

  const handleImageUpload = async (event: ChangeEvent<HTMLInputElement>) => {
    if (!event.target.files || event.target.files.length === 0) return
    const file = event.target.files[0]
    if (!item.id || !property?.id) return

    setIsUploading(true)
    const filePath = `${postId}/${item.id}/${Date.now()}-${file.name}`

    try {
      const { error: uploadError } = await supabase.storage.from(IMAGE_BUCKET_NAME).upload(filePath, file)
      if (uploadError) throw uploadError

      const { data: publicUrlData } = supabase.storage.from(IMAGE_BUCKET_NAME).getPublicUrl(filePath)
      if (!publicUrlData?.publicUrl) throw new Error("Failed to get public URL for uploaded image.")

      const newImageUrls = [...imageUrls, publicUrlData.publicUrl]
      setImageUrls(newImageUrls)

      const { error: dbError } = await supabase
        .from("social_post_properties")
        .update({ image_urls: newImageUrls })
        .eq("id", item.id)
      if (dbError) throw dbError

      toast({ title: "Image Uploaded", description: "New image added successfully." })
      onUpdate({ id: item.id, image_urls: newImageUrls })
    } catch (error: any) {
      console.error("Image upload error:", error)
      toast({ title: "Upload Failed", description: error.message || "Could not upload image.", variant: "destructive" })
    } finally {
      setIsUploading(false)
      if (event.target) event.target.value = ""
    }
  }

  const handleImageDelete = async (imageUrlToDelete: string) => {
    if (!item.id) return
    const bucketBaseUrl = `${supabase.storage.url}/object/public/${IMAGE_BUCKET_NAME}/`
    const filePath = imageUrlToDelete.replace(bucketBaseUrl, "")

    try {
      const { error: deleteError } = await supabase.storage.from(IMAGE_BUCKET_NAME).remove([filePath])
      if (deleteError) throw deleteError

      const newImageUrls = imageUrls.filter((url) => url !== imageUrlToDelete)
      setImageUrls(newImageUrls)

      const { error: dbError } = await supabase
        .from("social_post_properties")
        .update({ image_urls: newImageUrls })
        .eq("id", item.id)
      if (dbError) throw dbError

      toast({ title: "Image Deleted", description: "Image removed successfully." })
      onUpdate({ id: item.id, image_urls: newImageUrls })
    } catch (error: any) {
      console.error("Image delete error:", error)
      toast({ title: "Delete Failed", description: error.message || "Could not delete image.", variant: "destructive" })
    }
  }

  const handleAiRewrite = async () => {
    if (!propertyDescription.trim()) {
      toast({ title: "Nothing to rewrite", description: "Description is empty.", variant: "default" })
      return
    }
    console.log("Client: Starting AI Rewrite for description:", propertyDescription.substring(0, 100) + "...")
    setIsGenerating(true)
    try {
      const result = await generateDescriptionWithAI("rewrite", propertyDescription)
      console.log("Client: AI Rewrite result:", result)

      if (result.error) {
        toast({ title: "AI Rewrite Failed", description: result.error, variant: "destructive" })
      } else if (result.generatedText !== null) {
        // Check for null explicitly
        setPropertyDescription(result.generatedText)
        toast({ title: "Text Rewritten", description: "Description updated with AI suggestion. Save to persist." })
      } else {
        toast({
          title: "AI Rewrite",
          description: "No text was generated or an unknown issue occurred.",
          variant: "default",
        })
      }
    } catch (e: any) {
      console.error("Client: AI Rewrite caught error:", e)
      toast({
        title: "AI Rewrite Error",
        description: e.message || "An unexpected error occurred.",
        variant: "destructive",
      })
    } finally {
      setIsGenerating(false)
      console.log("Client: AI Rewrite finished.")
    }
  }

  const handleAiPromptSubmit = async () => {
    if (!aiPrompt.trim()) {
      toast({ title: "Prompt is empty", description: "Please enter a prompt.", variant: "default" })
      return
    }
    console.log(
      "Client: Starting AI Prompt with prompt:",
      aiPrompt,
      "and context:",
      propertyDescription.substring(0, 100) + "...",
    )
    setIsGenerating(true)
    setShowPromptDialog(false)
    try {
      const result = await generateDescriptionWithAI("prompt", aiPrompt, propertyDescription)
      console.log("Client: AI Prompt result:", result)

      if (result.error) {
        toast({ title: "AI Generation Failed", description: result.error, variant: "destructive" })
      } else if (result.generatedText !== null) {
        // Check for null explicitly
        setPropertyDescription(result.generatedText)
        toast({ title: "Text Generated", description: "Description updated with AI suggestion. Save to persist." })
      } else {
        toast({
          title: "AI Generation",
          description: "No text was generated or an unknown issue occurred.",
          variant: "default",
        })
      }
    } catch (e: any) {
      console.error("Client: AI Prompt caught error:", e)
      toast({
        title: "AI Generation Error",
        description: e.message || "An unexpected error occurred.",
        variant: "destructive",
      })
    } finally {
      setAiPrompt("")
      setIsGenerating(false)
      console.log("Client: AI Prompt finished.")
    }
  }

  if (!property) {
    return (
      <div className="p-3 border rounded-md bg-red-50 dark:bg-red-900/30 border-red-200 dark:border-red-700 text-red-700 dark:text-red-400 flex items-center">
        <AlertTriangle className="h-5 w-5 mr-2 flex-shrink-0" />
        Listing data missing for this item (ID: {item.property_id}).
      </div>
    )
  }

  const fullAddress = [
    property.street_number,
    property.street_direction,
    property.street_name,
    property.unit_number ? `#${property.unit_number}` : null,
    property.city,
    property.state,
    property.zip_code,
  ]
    .filter(Boolean)
    .join(" ")
    .replace(/\s+/g, " ")
    .trim()

  return (
    <div className="border border-gray-200 dark:border-gray-700 rounded-md bg-white dark:bg-gray-800/30 shadow-sm">
      <div className="p-3 flex flex-col sm:flex-row justify-between items-start sm:items-center">
        <div className="flex-grow mb-2 sm:mb-0 pr-2">
          <p
            className="text-[11px] text-muted-foreground mb-0.5 truncate"
            title={fullAddress || "Address not available"}
          >
            {fullAddress || "Address not available"}
          </p>
          <p className="text-sm font-medium text-gray-700 dark:text-gray-300">MLS: {property.mls_number || "N/A"}</p>
          <div className="flex space-x-4 mt-1">
            <p className="text-xs text-gray-600 dark:text-gray-400">
              Price: <span className="font-normal">{formatCurrency(property.list_price)}</span>
            </p>
            <p className="text-xs text-gray-600 dark:text-gray-400">
              Status: <span className="font-normal">{property.status || "N/A"}</span>
            </p>
          </div>
        </div>

        <div className="flex flex-col items-center space-y-1.5 sm:space-y-0 sm:flex-row sm:space-x-3 mx-auto sm:mx-0 my-2 sm:my-0 px-2">
          {[
            {
              label: "Contacted",
              state: contacted,
              setter: (val: boolean) => handleCheckboxChange("contacted_complete", val),
            },
            {
              label: "Image",
              state: imageComplete,
              setter: (val: boolean) => handleCheckboxChange("image_complete", val),
            },
            {
              label: "Desc.",
              state: descriptionComplete,
              setter: (val: boolean) => handleCheckboxChange("description_complete", val),
            },
          ].map((cb) => (
            <div key={cb.label} className="flex flex-col items-center">
              <label className="text-[10px] text-gray-500 dark:text-gray-400 mb-0.5">{cb.label}</label>
              <Checkbox
                checked={cb.state}
                onCheckedChange={cb.setter}
                className="rounded-[3px] data-[state=checked]:bg-blueishGreen-500 data-[state=checked]:border-blueishGreen-500 border-gray-400 dark:border-gray-500"
              />
            </div>
          ))}
        </div>

        <Button
          variant="ghost"
          size="sm"
          onClick={() => setIsExpanded(!isExpanded)}
          className="ml-auto sm:ml-2 p-1.5 self-start sm:self-center flex-shrink-0"
          aria-label={isExpanded ? "Collapse property details" : "Expand property details"}
        >
          {isExpanded ? <ChevronUp className="h-4 w-4" /> : <ChevronDown className="h-4 w-4" />}
        </Button>
      </div>

      {isExpanded && (
        <div className="p-3 border-t border-gray-200 dark:border-gray-700 bg-gray-50 dark:bg-gray-800/50">
          <div className="flex flex-col md:flex-row gap-4">
            <div className="flex-grow md:w-[60%] space-y-2">
              <label htmlFor={`prop-desc-${item.id}`} className="text-xs font-medium text-gray-700 dark:text-gray-300">
                Property-Specific Description
              </label>
              <Textarea
                id={`prop-desc-${item.id}`}
                value={propertyDescription}
                onChange={(e) => setPropertyDescription(e.target.value)}
                placeholder="Enter description for this property in the context of this social post..."
                className="min-h-[100px] text-sm bg-white dark:bg-gray-700/50"
              />
              <div className="flex items-center justify-between mt-1">
                <Popover>
                  <PopoverTrigger asChild>
                    <Button variant="ghost" size="sm" className="text-muted-foreground hover:text-primary px-2 py-1">
                      <Wand2 className="h-4 w-4 mr-1" /> AI Tools
                    </Button>
                  </PopoverTrigger>
                  <PopoverContent className="w-48 p-1">
                    <Button
                      variant="ghost"
                      className="w-full justify-start text-sm font-normal px-2 py-1.5 h-auto"
                      onClick={handleAiRewrite}
                      disabled={isGenerating || !propertyDescription.trim()}
                    >
                      {isGenerating && <Loader2 className="h-4 w-4 animate-spin mr-2" />} Rewrite
                    </Button>
                    <Button
                      variant="ghost"
                      className="w-full justify-start text-sm font-normal px-2 py-1.5 h-auto"
                      onClick={() => setShowPromptDialog(true)}
                      disabled={isGenerating}
                    >
                      {isGenerating && <Loader2 className="h-4 w-4 animate-spin mr-2" />} Prompt...
                    </Button>
                  </PopoverContent>
                </Popover>
                <Button
                  size="sm"
                  onClick={() => handlePropertyDescriptionSave()}
                  disabled={isSavingDesc || isGenerating}
                  className="text-xs"
                >
                  {isSavingDesc ? <Loader2 className="mr-1 h-3 w-3 animate-spin" /> : null}
                  Save Description
                </Button>
              </div>
            </div>

            <div className="flex-grow md:w-[40%] space-y-2">
              <label className="text-xs font-medium text-gray-700 dark:text-gray-300">Images</label>
              <div className="grid grid-cols-2 sm:grid-cols-3 gap-2 mb-2">
                {imageUrls.map((url) => (
                  <div key={url} className="relative group aspect-square bg-gray-100 dark:bg-gray-700 rounded">
                    <img
                      src={url || "/placeholder.svg?width=100&height=100&query=property"}
                      alt="Listing image"
                      className="object-cover w-full h-full rounded"
                      onError={(e) => (e.currentTarget.src = "/placeholder.svg?width=100&height=100")}
                    />
                    <Button
                      variant="destructive"
                      size="iconSm"
                      className="absolute top-1 right-1 h-5 w-5 p-0 opacity-0 group-hover:opacity-100 focus:opacity-100"
                      onClick={() => handleImageDelete(url)}
                      aria-label="Delete image"
                    >
                      <XIcon className="h-3 w-3" />
                    </Button>
                  </div>
                ))}
                <label
                  htmlFor={`img-upload-${item.id}`}
                  className={cn(
                    "aspect-square flex flex-col items-center justify-center border-2 border-dashed border-gray-300 dark:border-gray-600 rounded cursor-pointer hover:border-blueishGreen-500 dark:hover:border-blueishGreen-400 transition-colors",
                    isUploading && "opacity-50 cursor-not-allowed",
                  )}
                >
                  {isUploading ? (
                    <Loader2 className="h-6 w-6 animate-spin text-blueishGreen-500" />
                  ) : (
                    <>
                      <Plus className="h-6 w-6 text-gray-400 dark:text-gray-500" />
                      <span className="text-[10px] text-muted-foreground mt-1">Add Image</span>
                    </>
                  )}
                  <Input
                    id={`img-upload-${item.id}`}
                    type="file"
                    className="hidden"
                    onChange={handleImageUpload}
                    accept="image/png, image/jpeg, image/gif, image/webp"
                    disabled={isUploading}
                  />
                </label>
              </div>
              {imageUrls.length === 0 && !isUploading && (
                <div className="text-center py-4 text-xs text-muted-foreground">
                  <ImageIcon className="mx-auto h-8 w-8 mb-1 text-gray-400 dark:text-gray-500" />
                  No images added yet.
                </div>
              )}
            </div>
          </div>
        </div>
      )}
      <Dialog open={showPromptDialog} onOpenChange={setShowPromptDialog}>
        <DialogContent>
          <DialogHeader>
            <DialogTitle>Generate with AI Prompt</DialogTitle>
          </DialogHeader>
          <div className="py-4 space-y-2">
            <Label htmlFor="ai-prompt-input">Your Prompt</Label>
            <Textarea
              id="ai-prompt-input"
              value={aiPrompt}
              onChange={(e) => setAiPrompt(e.target.value)}
              placeholder="e.g., Write a catchy description focusing on the new kitchen..."
              className="min-h-[80px]"
            />
            {propertyDescription && (
              <p className="text-xs text-muted-foreground">
                Current description will be used as context if relevant to your prompt.
              </p>
            )}
          </div>
          <DialogFooter>
            <Button variant="outline" onClick={() => setShowPromptDialog(false)} disabled={isGenerating}>
              Cancel
            </Button>
            <Button onClick={handleAiPromptSubmit} disabled={isGenerating || !aiPrompt.trim()}>
              {isGenerating && <Loader2 className="mr-2 h-4 w-4 animate-spin" />}
              Generate
            </Button>
          </DialogFooter>
        </DialogContent>
      </Dialog>
    </div>
  )
}
```

## File: dkl-microapp-2-main/components/theme-provider.tsx
```typescript
'use client'

import * as React from 'react'
import {
  ThemeProvider as NextThemesProvider,
  type ThemeProviderProps,
} from 'next-themes'

export function ThemeProvider({ children, ...props }: ThemeProviderProps) {
  return <NextThemesProvider {...props}>{children}</NextThemesProvider>
}
```

## File: dkl-microapp-2-main/components/user-nav.tsx
```typescript
"use client"

import { useAuth } from "@/contexts/auth-context"
import { Avatar, AvatarFallback } from "@/components/ui/avatar"
import { Button } from "@/components/ui/button"
import {
  DropdownMenu,
  DropdownMenuContent,
  DropdownMenuGroup,
  DropdownMenuItem,
  DropdownMenuLabel,
  DropdownMenuSeparator,
  DropdownMenuTrigger,
} from "@/components/ui/dropdown-menu"
import { LogOut, Settings, User } from "lucide-react"
import Link from "next/link"

export function UserNav() {
  const { user, signOut } = useAuth()

  if (!user) return null

  const initials = user.email ? user.email.substring(0, 2).toUpperCase() : "U"

  return (
    <DropdownMenu>
      <DropdownMenuTrigger asChild>
        <Button variant="ghost" className="relative h-8 w-8 rounded-full">
          <Avatar className="h-8 w-8">
            <AvatarFallback className="text-xs">{initials}</AvatarFallback>
          </Avatar>
        </Button>
      </DropdownMenuTrigger>
      <DropdownMenuContent className="w-56" align="end" forceMount>
        <DropdownMenuLabel className="font-normal">
          <div className="flex flex-col space-y-1">
            <p className="text-sm font-medium leading-none">{user.email}</p>
            <p className="text-xs leading-none text-muted-foreground">{user.id.substring(0, 8)}</p>
          </div>
        </DropdownMenuLabel>
        <DropdownMenuSeparator />
        <DropdownMenuGroup>
          <DropdownMenuItem asChild>
            <Link href="/profile">
              <User className="mr-2 h-4 w-4" />
              <span>Profile</span>
            </Link>
          </DropdownMenuItem>
          <DropdownMenuItem asChild>
            <Link href="/settings">
              <Settings className="mr-2 h-4 w-4" />
              <span>Settings</span>
            </Link>
          </DropdownMenuItem>
        </DropdownMenuGroup>
        <DropdownMenuSeparator />
        <DropdownMenuItem onClick={() => signOut()}>
          <LogOut className="mr-2 h-4 w-4" />
          <span>Log out</span>
        </DropdownMenuItem>
      </DropdownMenuContent>
    </DropdownMenu>
  )
}
```

## File: dkl-microapp-2-main/contexts/auth-context.tsx
```typescript
"use client"

import type React from "react"

import { createContext, useContext, useEffect, useState } from "react"
import type { User, Session } from "@supabase/supabase-js"
import { supabase } from "@/lib/supabase/client"
import { useRouter } from "next/navigation"

interface AuthContextType {
  user: User | null
  session: Session | null
  loading: boolean
  signIn: (email: string, password: string) => Promise<void>
  signUp: (email: string, password: string) => Promise<void>
  signOut: () => Promise<void>
}

const AuthContext = createContext<AuthContextType | undefined>(undefined)

export function AuthProvider({ children }: { children: React.ReactNode }) {
  const [user, setUser] = useState<User | null>(null)
  const [session, setSession] = useState<Session | null>(null)
  const [loading, setLoading] = useState(true)
  const router = useRouter()

  useEffect(() => {
    const {
      data: { subscription },
    } = supabase.auth.onAuthStateChange(async (event, session) => {
      setSession(session)
      setUser(session?.user ?? null)
      setLoading(false)

      if (event === "SIGNED_OUT") {
        router.push("/login")
      }
    })

    supabase.auth.getSession().then(({ data: { session } }) => {
      setSession(session)
      setUser(session?.user ?? null)
      setLoading(false)
    })

    return () => {
      subscription.unsubscribe()
    }
  }, [router])

  const signIn = async (email: string, password: string) => {
    const { error } = await supabase.auth.signInWithPassword({ email, password })
    if (error) throw error
    router.push("/dashboard")
  }

  const signUp = async (email: string, password: string) => {
    const { error } = await supabase.auth.signUp({ email, password })
    if (error) throw error
  }

  const signOut = async () => {
    const { error } = await supabase.auth.signOut()
    if (error) throw error
  }

  return (
    <AuthContext.Provider value={{ user, session, loading, signIn, signUp, signOut }}>{children}</AuthContext.Provider>
  )
}

export const useAuth = () => {
  const context = useContext(AuthContext)
  if (!context) {
    throw new Error("useAuth must be used within an AuthProvider")
  }
  return context
}
```

## File: dkl-microapp-2-main/hooks/use-toast.ts
```typescript
"use client"

// Inspired by react-hot-toast library
import * as React from "react"

import type { ToastActionElement, ToastProps } from "@/components/ui/toast"

const TOAST_LIMIT = 5
const TOAST_REMOVE_DELAY = 1000000

type ToasterToast = ToastProps & {
  id: string
  title?: React.ReactNode
  description?: React.ReactNode
  action?: ToastActionElement
}

const actionTypes = {
  ADD_TOAST: "ADD_TOAST",
  UPDATE_TOAST: "UPDATE_TOAST",
  DISMISS_TOAST: "DISMISS_TOAST",
  REMOVE_TOAST: "REMOVE_TOAST",
} as const

let count = 0

function genId() {
  count = (count + 1) % Number.MAX_VALUE
  return count.toString()
}

type ActionType = typeof actionTypes

type Action =
  | {
      type: ActionType["ADD_TOAST"]
      toast: ToasterToast
    }
  | {
      type: ActionType["UPDATE_TOAST"]
      toast: Partial<ToasterToast>
    }
  | {
      type: ActionType["DISMISS_TOAST"]
      toastId?: ToasterToast["id"]
    }
  | {
      type: ActionType["REMOVE_TOAST"]
      toastId?: ToasterToast["id"]
    }

interface State {
  toasts: ToasterToast[]
}

const toastTimeouts = new Map<string, ReturnType<typeof setTimeout>>()

const addToRemoveQueue = (toastId: string) => {
  if (toastTimeouts.has(toastId)) {
    return
  }

  const timeout = setTimeout(() => {
    toastTimeouts.delete(toastId)
    dispatch({
      type: "REMOVE_TOAST",
      toastId: toastId,
    })
  }, TOAST_REMOVE_DELAY)

  toastTimeouts.set(toastId, timeout)
}

export const reducer = (state: State, action: Action): State => {
  switch (action.type) {
    case "ADD_TOAST":
      return {
        ...state,
        toasts: [action.toast, ...state.toasts].slice(0, TOAST_LIMIT),
      }

    case "UPDATE_TOAST":
      return {
        ...state,
        toasts: state.toasts.map((t) => (t.id === action.toast.id ? { ...t, ...action.toast } : t)),
      }

    case "DISMISS_TOAST": {
      const { toastId } = action

      // ! Side effects ! - This could be extracted into a dismissToast() action,
      // but I'll keep it here for simplicity
      if (toastId) {
        addToRemoveQueue(toastId)
      } else {
        state.toasts.forEach((toast) => {
          addToRemoveQueue(toast.id)
        })
      }

      return {
        ...state,
        toasts: state.toasts.map((t) =>
          t.id === toastId || toastId === undefined
            ? {
                ...t,
                open: false,
              }
            : t,
        ),
      }
    }
    case "REMOVE_TOAST":
      if (action.toastId === undefined) {
        return {
          ...state,
          toasts: [],
        }
      }
      return {
        ...state,
        toasts: state.toasts.filter((t) => t.id !== action.toastId),
      }
  }
}

const listeners: Array<(state: State) => void> = []

let memoryState: State = { toasts: [] }

function dispatch(action: Action) {
  memoryState = reducer(memoryState, action)
  listeners.forEach((listener) => {
    listener(memoryState)
  })
}

type Toast = Omit<ToasterToast, "id">

function toast({ ...props }: Toast) {
  const id = genId()

  const update = (props: ToasterToast) =>
    dispatch({
      type: "UPDATE_TOAST",
      toast: { ...props, id },
    })
  const dismiss = () => dispatch({ type: "DISMISS_TOAST", toastId: id })

  dispatch({
    type: "ADD_TOAST",
    toast: {
      ...props,
      id,
      open: true,
      onOpenChange: (open) => {
        if (!open) dismiss()
      },
    },
  })

  return {
    id: id,
    dismiss,
    update,
  }
}

function useToast() {
  const [state, setState] = React.useState<State>(memoryState)

  React.useEffect(() => {
    listeners.push(setState)
    return () => {
      const index = listeners.indexOf(setState)
      if (index > -1) {
        listeners.splice(index, 1)
      }
    }
  }, [state])

  return {
    ...state,
    toast,
    dismiss: (toastId?: string) => dispatch({ type: "DISMISS_TOAST", toastId }),
  }
}

export { useToast, toast }
```

## File: dkl-microapp-2-main/lib/supabase/client.ts
```typescript
import { createClient } from "@supabase/supabase-js"
import type { Database } from "@/types/supabase"

const supabaseUrl = process.env.NEXT_PUBLIC_SUPABASE_URL
const supabaseAnonKey = process.env.NEXT_PUBLIC_SUPABASE_ANON_KEY

if (!supabaseUrl) {
  console.error("Supabase URL is not defined. Please check your NEXT_PUBLIC_SUPABASE_URL environment variable.")
  // throw new Error("Supabase URL is not defined."); // Optionally throw to halt execution
}

if (!supabaseAnonKey) {
  console.error(
    "Supabase Anon Key is not defined. Please check your NEXT_PUBLIC_SUPABASE_ANON_KEY environment variable.",
  )
  // throw new Error("Supabase Anon Key is not defined."); // Optionally throw
}

// The export should only happen if the keys are defined, or handle the error gracefully.
// For Next.js, we'll proceed with the export, relying on the console errors for debugging.
export const supabase = createClient<Database>(supabaseUrl!, supabaseAnonKey!)
```

## File: dkl-microapp-2-main/lib/supabase/server.ts
```typescript
import { createClient } from "@supabase/supabase-js"
import { cookies } from "next/headers"
import type { Database } from "@/types/supabase"

export async function createServerClient() {
  const cookieStore = cookies()

  return createClient<Database>(process.env.NEXT_PUBLIC_SUPABASE_URL!, process.env.NEXT_PUBLIC_SUPABASE_ANON_KEY!, {
    cookies: {
      get(name: string) {
        return cookieStore.get(name)?.value
      },
    },
  })
}
```

## File: dkl-microapp-2-main/lib/builder-fields.ts
```typescript
import type { Database } from "@/types/supabase"

type BuilderRowKeys = keyof Database["public"]["Tables"]["builders"]["Row"]

export interface BuilderFieldDefinition {
  value: BuilderRowKeys
  label: string
  typeHint: "string" | "number" | "boolean" | "date" | "array_string" | "json"
}

export const builderTableColumns: readonly BuilderFieldDefinition[] = [
  { value: "name", label: "Builder Name", typeHint: "string" },
  { value: "company_name", label: "Company Name", typeHint: "string" },
  { value: "phone", label: "Phone", typeHint: "string" },
  { value: "email", label: "Email", typeHint: "string" },
  { value: "website", label: "Website", typeHint: "string" },
  { value: "address", label: "Address", typeHint: "string" },
  { value: "city", label: "City", typeHint: "string" },
  { value: "state", label: "State", typeHint: "string" },
  { value: "zip_code", label: "Zip Code", typeHint: "string" },
  { value: "years_in_business", label: "Years In Business", typeHint: "number" },
  { value: "total_projects", label: "Total Projects", typeHint: "number" },
  { value: "active_projects", label: "Active Projects", typeHint: "number" },
  { value: "specialties", label: "Specialties", typeHint: "array_string" },
  { value: "price_range_min", label: "Price Range Min", typeHint: "number" },
  { value: "price_range_max", label: "Price Range Max", typeHint: "number" },
  { value: "rating", label: "Rating", typeHint: "number" },
  { value: "notes", label: "Notes", typeHint: "string" },
  { value: "metadata", label: "Metadata", typeHint: "json" },
] as const

export type MappedBuilderDbColumn = BuilderFieldDefinition["value"] | "ignore_field"
```

## File: dkl-microapp-2-main/lib/color-utils.ts
```typescript
/**
 * Converts a HEX color value to HSL. Conversion formula
 * adapted from https://stackoverflow.com/a/9493060.
 * Assumes hex is a valid color string.
 * @param   {string}  hex       The hex color to convert
 * @returns {string | null}     The HSL representation "H S% L%" or null on error
 */
export function hexToHsl(hex: string): string | null {
  let r = 0,
    g = 0,
    b = 0
  // 3 digits
  if (hex.length == 4) {
    r = Number.parseInt(hex[1] + hex[1], 16)
    g = Number.parseInt(hex[2] + hex[2], 16)
    b = Number.parseInt(hex[3] + hex[3], 16)
  }
  // 6 digits
  else if (hex.length == 7) {
    r = Number.parseInt(hex.substring(1, 3), 16)
    g = Number.parseInt(hex.substring(3, 5), 16)
    b = Number.parseInt(hex.substring(5, 7), 16)
  } else {
    return null // Invalid hex format
  }

  r /= 255
  g /= 255
  b /= 255
  const max = Math.max(r, g, b)
  const min = Math.min(r, g, b)
  let h = 0,
    s = 0,
    l = (max + min) / 2

  if (max == min) {
    h = s = 0 // achromatic
  } else {
    const d = max - min
    s = l > 0.5 ? d / (2 - max - min) : d / (max + min)
    switch (max) {
      case r:
        h = (g - b) / d + (g < b ? 6 : 0)
        break
      case g:
        h = (b - r) / d + 2
        break
      case b:
        h = (r - g) / d + 4
        break
    }
    h /= 6
  }

  h = Math.round(h * 360)
  s = Math.round(s * 100)
  l = Math.round(l * 100)

  return `${h} ${s}% ${l}%`
}

/**
 * Converts an HSL color value to HEX. Conversion formula
 * adapted from https://stackoverflow.com/a/9493060.
 * Assumes h, s, and l are contained in the set [0, 1] and
 * returns r, g, and b in the set [0, 255].
 *
 * @param   {string}  hsl       The HSL color "H S% L%"
 * @returns {string | null}     The HEX representation or null on error
 */
export function hslToHex(hsl: string): string | null {
  const hslMatch = hsl.match(/(\d+)\s+(\d+)%\s+(\d+)%/)
  if (!hslMatch) return null

  let h = Number.parseInt(hslMatch[1])
  let s = Number.parseInt(hslMatch[2])
  let l = Number.parseInt(hslMatch[3])

  h /= 360
  s /= 100
  l /= 100

  let r, g, b
  if (s == 0) {
    r = g = b = l // achromatic
  } else {
    const hue2rgb = (p: number, q: number, t: number) => {
      if (t < 0) t += 1
      if (t > 1) t -= 1
      if (t < 1 / 6) return p + (q - p) * 6 * t
      if (t < 1 / 2) return q
      if (t < 2 / 3) return p + (q - p) * (2 / 3 - t) * 6
      return p
    }
    const q = l < 0.5 ? l * (1 + s) : l + s - l * s
    const p = 2 * l - q
    r = hue2rgb(p, q, h + 1 / 3)
    g = hue2rgb(p, q, h)
    b = hue2rgb(p, q, h - 1 / 3)
  }

  const toHex = (x: number) => {
    const hex = Math.round(x * 255).toString(16)
    return hex.length == 1 ? "0" + hex : hex
  }

  return `#${toHex(r)}${toHex(g)}${toHex(b)}`
}
```

## File: dkl-microapp-2-main/lib/listing-fields.ts
```typescript
import type { Database } from "@/types/supabase"

// Extracting keys from a specific table's Row type
type ListingRowKeys = keyof Database["public"]["Tables"]["listings"]["Row"]

// Define a structure for our mapping options
export interface ListingFieldDefinition {
  value: ListingRowKeys
  label: string
  typeHint: "string" | "number" | "boolean" | "date" | "array_string" | "json" // Add more as needed
}

// Manually define user-friendly labels and type hints for each listing column
export const listingTableColumns: ListingFieldDefinition[] = [
  { value: "mls_number", label: "MLS Number", typeHint: "string" },
  { value: "status", label: "Status", typeHint: "string" },
  { value: "type", label: "Type", typeHint: "string" },
  { value: "dom", label: "DOM (Days on Market)", typeHint: "number" },
  { value: "cdom", label: "CDOM (Cumulative Days on Market)", typeHint: "number" },
  { value: "list_date", label: "List Date", typeHint: "date" },
  { value: "off_market_date", label: "Off Market Date", typeHint: "date" },
  { value: "settled_date", label: "Settled Date", typeHint: "date" },
  { value: "original_price", label: "Original Price", typeHint: "number" },
  { value: "list_price", label: "List Price", typeHint: "number" },
  { value: "sold_price", label: "Sold Price", typeHint: "number" },
  { value: "city", label: "City", typeHint: "string" },
  { value: "state", label: "State", typeHint: "string" },
  { value: "zip_code", label: "Zip Code", typeHint: "string" },
  { value: "county", label: "County", typeHint: "string" },
  { value: "subdivision", label: "Subdivision", typeHint: "string" },
  { value: "list_agent_name", label: "List Agent Name", typeHint: "string" },
  { value: "list_office_name", label: "List Office Name", typeHint: "string" },
  { value: "acres_total", label: "Acres Total", typeHint: "number" },
  { value: "land_use_code", label: "Land Use Code", typeHint: "string" },
  { value: "hoa", label: "HOA", typeHint: "boolean" },
  { value: "association_fee_frequency", label: "Association Fee Frequency", typeHint: "string" },
  { value: "property_condition", label: "Listing Condition", typeHint: "string" },
  { value: "bedrooms", label: "Bedrooms", typeHint: "number" },
  { value: "baths_full", label: "Baths Full", typeHint: "number" },
  { value: "baths_half", label: "Baths Half", typeHint: "number" },
  { value: "style", label: "Style", typeHint: "string" },
  { value: "basement", label: "Basement", typeHint: "boolean" },
  { value: "garage_spaces", label: "Garage Spaces", typeHint: "number" },
  { value: "fireplace", label: "Fireplace", typeHint: "boolean" },
  { value: "new_construction", label: "New Construction (Y/N)", typeHint: "boolean" },
  { value: "new_construction_details", label: "New Construction Details", typeHint: "string" },
  { value: "model_name", label: "Model Name", typeHint: "string" },
  { value: "builder_id", label: "Builder ID", typeHint: "string" },
  { value: "metadata", label: "Metadata", typeHint: "json" },
  { value: "in_social_queue", label: "In Social Queue", typeHint: "boolean" },
  { value: "owner_name", label: "Owner Name", typeHint: "string" },
  { value: "construction_completed_yn", label: "Construction Completed (Y/N)", typeHint: "boolean" },
  { value: "year_built", label: "Year Built", typeHint: "number" },
  { value: "year_built_source", label: "Year Built Source", typeHint: "string" },
  { value: "imported_builder_name", label: "Imported Builder Name", typeHint: "string" },
  { value: "occupant_type", label: "Occupant Type", typeHint: "string" },
  { value: "occupant_name", label: "Occupant Name", typeHint: "string" },
  { value: "previous_list_price", label: "Previous List Price", typeHint: "number" },
  { value: "architect_name", label: "Architect Name", typeHint: "string" },
  { value: "structure_type", label: "Structure Type", typeHint: "string" },
  { value: "block_lot", label: "Block/Lot", typeHint: "string" },
  { value: "remarks_private", label: "Remarks - Private", typeHint: "string" },
  { value: "remarks_public", label: "Remarks - Public", typeHint: "string" },
  { value: "year_major_reno_remodel", label: "Year Major Reno/Remodel", typeHint: "number" },
  { value: "change_info", label: "Change Info", typeHint: "string" },
  { value: "close_date", label: "Close Date", typeHint: "date" },
  { value: "close_price", label: "Close Price", typeHint: "number" },
  { value: "close_sale_type", label: "Close Sale Type", typeHint: "string" },
  { value: "foundation_details", label: "Foundation Details", typeHint: "string" },
  { value: "land_assessed_value", label: "Land Assessed Value", typeHint: "number" },
  { value: "list_picture_url", label: "List Picture URL", typeHint: "string" },
  { value: "lot_features", label: "Lot Features", typeHint: "array_string" },
  { value: "lot_size_sqft", label: "Lot Size SqFt", typeHint: "number" },
  { value: "address_line_1", label: "Address Line 1", typeHint: "string" },
  { value: "latitude", label: "Latitude", typeHint: "number" },
  { value: "longitude", label: "Longitude", typeHint: "number" },
  { value: "last_sold_date", label: "Last Sold Date", typeHint: "date" },
  { value: "last_sold_price", label: "Last Sold Price", typeHint: "number" },
  { value: "property_type", label: "Listing Type", typeHint: "string" },
  { value: "description", label: "Description", typeHint: "string" },
]

export type MappedDbColumn = ListingFieldDefinition["value"] | "ignore_field"
```

## File: dkl-microapp-2-main/lib/supabase.ts
```typescript
import { createClient } from "@supabase/supabase-js"
import type { Database } from "@/types/supabase"

const supabaseUrl = process.env.NEXT_PUBLIC_SUPABASE_URL!
const supabaseAnonKey = process.env.NEXT_PUBLIC_SUPABASE_ANON_KEY!

// Create a single supabase client for interacting with your database
export const supabase = createClient<Database>(supabaseUrl, supabaseAnonKey)

// Server-side client with service role for admin operations
export const createServerSupabaseClient = () => {
  const supabaseUrl = process.env.NEXT_PUBLIC_SUPABASE_URL!
  const supabaseServiceKey = process.env.SUPABASE_SERVICE_ROLE_KEY!
  return createClient<Database>(supabaseUrl, supabaseServiceKey)
}
```

## File: dkl-microapp-2-main/lib/utils.ts
```typescript
import { type ClassValue, clsx } from "clsx"
import { twMerge } from "tailwind-merge"

export function cn(...inputs: ClassValue[]) {
  return twMerge(clsx(inputs))
}

export function formatCurrency(value: number | null | undefined): string {
  if (value === null || value === undefined) return "-"
  return new Intl.NumberFormat("en-US", {
    style: "currency",
    currency: "USD",
    maximumFractionDigits: 0,
  }).format(value)
}

export function formatNumber(value: number | null | undefined): string {
  if (value === null || value === undefined) return "-"
  return new Intl.NumberFormat("en-US").format(value)
}

export function formatDate(date: string | null | undefined): string {
  if (!date) return "-"
  try {
    // Attempt to parse common date formats, including those with slashes or hyphens
    const parsedDate = new Date(date.replace(/-/g, "/"))
    if (isNaN(parsedDate.getTime())) {
      // Handle cases where date might be just a year or invalid
      if (/^\d{4}$/.test(date)) return date // If it's just a year, return it
      return "-" // Invalid date
    }
    return parsedDate.toLocaleDateString("en-US", {
      year: "numeric",
      month: "short",
      day: "numeric",
    })
  } catch (error) {
    console.warn(`Could not parse date: ${date}`, error)
    return "-"
  }
}

export function getFullAddress(listing: any): string {
  const parts = [
    listing.street_number,
    listing.street_direction,
    listing.street_name,
    listing.unit_number ? `Unit ${listing.unit_number}` : "",
  ]
    .filter(Boolean)
    .join(" ")

  const cityStateZip = [listing.city, listing.state, listing.zip_code].filter(Boolean).join(", ")

  return [parts, cityStateZip].filter(Boolean).join(", ")
}

export function getStatusColor(status: string | null): string {
  switch (status?.toLowerCase()) {
    case "active":
      return "bg-green-100 text-green-800"
    case "pending":
      return "bg-yellow-100 text-yellow-800"
    case "sold":
      return "bg-blue-100 text-blue-800"
    case "under contract":
      return "bg-purple-100 text-purple-800"
    case "coming soon":
      return "bg-orange-100 text-orange-800"
    default:
      return "bg-gray-100 text-gray-800"
  }
}

export function parseCSVValue(
  value: string | null | undefined,
  targetTypeHint?: "string" | "number" | "boolean" | "date" | "array_string",
): any {
  if (value === null || value === undefined || value.trim() === "") return null

  // Remove dollar signs and commas for currency/numbers before other parsing
  const cleanedValue = value.replace(/[$,]/g, "")

  if (targetTypeHint === "array_string") {
    return value
      .split(",")
      .map((item) => item.trim())
      .filter(Boolean)
  }

  // Convert Yes/No to boolean
  if (cleanedValue.toLowerCase() === "yes") return true
  if (cleanedValue.toLowerCase() === "no") return false

  // Try to parse as number if it looks like one or hinted
  if (targetTypeHint === "number" || /^-?\d+(\.\d+)?$/.test(cleanedValue)) {
    const num = Number.parseFloat(cleanedValue)
    if (!isNaN(num)) {
      return num
    }
  }

  // Try to parse as date if hinted
  if (targetTypeHint === "date") {
    try {
      const dateVal = new Date(value.replace(/-/g, "/")) // Normalize separators
      if (!isNaN(dateVal.getTime())) {
        return dateVal.toISOString()
      }
    } catch (e) {
      /* ignore, will return original string */
    }
  }

  // If it's a boolean string "true" or "false"
  if (cleanedValue.toLowerCase() === "true") return true
  if (cleanedValue.toLowerCase() === "false") return false

  // Default to string
  return value.trim()
}

export function toTitleCase(str: string | null | undefined): string | null {
  if (!str) return null
  // Handle cases like "McKinley" or "O'Malley" by not lowercasing the entire string first.
  // This regex capitalizes the first letter of each word.
  // It also handles hyphens by capitalizing the letter after a hyphen.
  return str
    .replace(/\b([a-z'])([a-z']*)\b|\b([A-Z'])([A-Z']*)\b/g, (match, firstLower, restLower, firstUpper, restUpper) => {
      if (firstLower) {
        return firstLower.toUpperCase() + (restLower || "")
      }
      if (firstUpper) {
        // If it's already mostly uppercase (e.g., an acronym), leave it, unless it's a single char.
        // Or if it's a mixed case word that starts with uppercase.
        if ((restUpper && restUpper.match(/[a-z]/)) || !restUpper || restUpper.length === 0) {
          return firstUpper + (restUpper || "")
        }
        // If it's all caps and longer than 1 char, convert to title case.
        if (restUpper && !restUpper.match(/[a-z]/) && (firstUpper + restUpper).length > 1) {
          return firstUpper + restUpper.toLowerCase()
        }
        return firstUpper + (restUpper || "")
      }
      return match
    })
    .replace(/([a-zA-Z])(?:-|_)+([a-zA-Z])/g, (match, p1, p2) => p1 + "-" + p2.toUpperCase()) // Capitalize after hyphen
}

/**
 * Normalizes a CSV header string.
 * - Trims whitespace.
 * - Converts to uppercase.
 * - Replaces sequences of non-alphanumeric characters (excluding underscore) with a single underscore.
 * - Removes leading and trailing underscores.
 * Example: "  List Price ($)  " -> "LIST_PRICE"
 * Example: "MLS #" -> "MLS_"
 */
export function normalizeHeader(header: string): string {
  if (!header) return ""
  return header
    .trim()
    .toUpperCase()
    .replace(/[^A-Z0-9_]+/g, "_") // Replace one or more non-alphanumeric (A-Z, 0-9) or non-underscore chars with a single underscore
    .replace(/^_|_$/g, "") // Remove leading/trailing underscores
}
```

## File: dkl-microapp-2-main/public/placeholder-logo.svg
```
<svg xmlns="http://www.w3.org/2000/svg" width="215" height="48" fill="none"><path fill="#000" d="M57.588 9.6h6L73.828 38h-5.2l-2.36-6.88h-11.36L52.548 38h-5.2l10.24-28.4Zm7.16 17.16-4.16-12.16-4.16 12.16h8.32Zm23.694-2.24c-.186-1.307-.706-2.32-1.56-3.04-.853-.72-1.866-1.08-3.04-1.08-1.68 0-2.986.613-3.92 1.84-.906 1.227-1.36 2.947-1.36 5.16s.454 3.933 1.36 5.16c.934 1.227 2.24 1.84 3.92 1.84 1.254 0 2.307-.373 3.16-1.12.854-.773 1.387-1.867 1.6-3.28l5.12.24c-.186 1.68-.733 3.147-1.64 4.4-.906 1.227-2.08 2.173-3.52 2.84-1.413.667-2.986 1-4.72 1-2.08 0-3.906-.453-5.48-1.36-1.546-.907-2.76-2.2-3.64-3.88-.853-1.68-1.28-3.627-1.28-5.84 0-2.24.427-4.187 1.28-5.84.88-1.68 2.094-2.973 3.64-3.88 1.574-.907 3.4-1.36 5.48-1.36 1.68 0 3.227.32 4.64.96 1.414.64 2.56 1.56 3.44 2.76.907 1.2 1.454 2.6 1.64 4.2l-5.12.28Zm11.486-7.72.12 3.4c.534-1.227 1.307-2.173 2.32-2.84 1.04-.693 2.267-1.04 3.68-1.04 1.494 0 2.76.387 3.8 1.16 1.067.747 1.827 1.813 2.28 3.2.507-1.44 1.294-2.52 2.36-3.24 1.094-.747 2.414-1.12 3.96-1.12 1.414 0 2.64.307 3.68.92s1.84 1.52 2.4 2.72c.56 1.2.84 2.667.84 4.4V38h-4.96V25.92c0-1.813-.293-3.187-.88-4.12-.56-.96-1.413-1.44-2.56-1.44-.906 0-1.68.213-2.32.64-.64.427-1.133 1.053-1.48 1.88-.32.827-.48 1.84-.48 3.04V38h-4.56V25.92c0-1.2-.133-2.213-.4-3.04-.24-.827-.626-1.453-1.16-1.88-.506-.427-1.133-.64-1.88-.64-.906 0-1.68.227-2.32.68-.64.427-1.133 1.053-1.48 1.88-.32.827-.48 1.827-.48 3V38h-4.96V16.8h4.48Zm26.723 10.6c0-2.24.427-4.187 1.28-5.84.854-1.68 2.067-2.973 3.64-3.88 1.574-.907 3.4-1.36 5.48-1.36 1.84 0 3.494.413 4.96 1.24 1.467.827 2.64 2.08 3.52 3.76.88 1.653 1.347 3.693 1.4 6.12v1.32h-15.08c.107 1.813.614 3.227 1.52 4.24.907.987 2.134 1.48 3.68 1.48.987 0 1.88-.253 2.68-.76a4.803 4.803 0 0 0 1.84-2.2l5.08.36c-.64 2.027-1.84 3.64-3.6 4.84-1.733 1.173-3.733 1.76-6 1.76-2.08 0-3.906-.453-5.48-1.36-1.573-.907-2.786-2.2-3.64-3.88-.853-1.68-1.28-3.627-1.28-5.84Zm15.16-2.04c-.213-1.733-.76-3.013-1.64-3.84-.853-.827-1.893-1.24-3.12-1.24-1.44 0-2.6.453-3.48 1.36-.88.88-1.44 2.12-1.68 3.72h9.92ZM163.139 9.6V38h-5.04V9.6h5.04Zm8.322 7.2.24 5.88-.64-.36c.32-2.053 1.094-3.56 2.32-4.52 1.254-.987 2.787-1.48 4.6-1.48 2.32 0 4.107.733 5.36 2.2 1.254 1.44 1.88 3.387 1.88 5.84V38h-4.96V25.92c0-1.253-.12-2.28-.36-3.08-.24-.8-.64-1.413-1.2-1.84-.533-.427-1.253-.64-2.16-.64-1.44 0-2.573.48-3.4 1.44-.8.933-1.2 2.307-1.2 4.12V38h-4.96V16.8h4.48Zm30.003 7.72c-.186-1.307-.706-2.32-1.56-3.04-.853-.72-1.866-1.08-3.04-1.08-1.68 0-2.986.613-3.92 1.84-.906 1.227-1.36 2.947-1.36 5.16s.454 3.933 1.36 5.16c.934 1.227 2.24 1.84 3.92 1.84 1.254 0 2.307-.373 3.16-1.12.854-.773 1.387-1.867 1.6-3.28l5.12.24c-.186 1.68-.733 3.147-1.64 4.4-.906 1.227-2.08 2.173-3.52 2.84-1.413.667-2.986 1-4.72 1-2.08 0-3.906-.453-5.48-1.36-1.546-.907-2.76-2.2-3.64-3.88-.853-1.68-1.28-3.627-1.28-5.84 0-2.24.427-4.187 1.28-5.84.88-1.68 2.094-2.973 3.64-3.88 1.574-.907 3.4-1.36 5.48-1.36 1.68 0 3.227.32 4.64.96 1.414.64 2.56 1.56 3.44 2.76.907 1.2 1.454 2.6 1.64 4.2l-5.12.28Zm11.443 8.16V38h-5.6v-5.32h5.6Z"/><path fill="#171717" fill-rule="evenodd" d="m7.839 40.783 16.03-28.054L20 6 0 40.783h7.839Zm8.214 0H40L27.99 19.894l-4.02 7.032 3.976 6.914H20.02l-3.967 6.943Z" clip-rule="evenodd"/></svg>
```

## File: dkl-microapp-2-main/public/placeholder.svg
```
<svg xmlns="http://www.w3.org/2000/svg" width="1200" height="1200" fill="none"><rect width="1200" height="1200" fill="#EAEAEA" rx="3"/><g opacity=".5"><g opacity=".5"><path fill="#FAFAFA" d="M600.709 736.5c-75.454 0-136.621-61.167-136.621-136.62 0-75.454 61.167-136.621 136.621-136.621 75.453 0 136.62 61.167 136.62 136.621 0 75.453-61.167 136.62-136.62 136.62Z"/><path stroke="#C9C9C9" stroke-width="2.418" d="M600.709 736.5c-75.454 0-136.621-61.167-136.621-136.62 0-75.454 61.167-136.621 136.621-136.621 75.453 0 136.62 61.167 136.62 136.621 0 75.453-61.167 136.62-136.62 136.62Z"/></g><path stroke="url(#a)" stroke-width="2.418" d="M0-1.209h553.581" transform="scale(1 -1) rotate(45 1163.11 91.165)"/><path stroke="url(#b)" stroke-width="2.418" d="M404.846 598.671h391.726"/><path stroke="url(#c)" stroke-width="2.418" d="M599.5 795.742V404.017"/><path stroke="url(#d)" stroke-width="2.418" d="m795.717 796.597-391.441-391.44"/><path fill="#fff" d="M600.709 656.704c-31.384 0-56.825-25.441-56.825-56.824 0-31.384 25.441-56.825 56.825-56.825 31.383 0 56.824 25.441 56.824 56.825 0 31.383-25.441 56.824-56.824 56.824Z"/><g clip-path="url(#e)"><path fill="#666" fill-rule="evenodd" d="M616.426 586.58h-31.434v16.176l3.553-3.554.531-.531h9.068l.074-.074 8.463-8.463h2.565l7.18 7.181V586.58Zm-15.715 14.654 3.698 3.699 1.283 1.282-2.565 2.565-1.282-1.283-5.2-5.199h-6.066l-5.514 5.514-.073.073v2.876a2.418 2.418 0 0 0 2.418 2.418h26.598a2.418 2.418 0 0 0 2.418-2.418v-8.317l-8.463-8.463-7.181 7.181-.071.072Zm-19.347 5.442v4.085a6.045 6.045 0 0 0 6.046 6.045h26.598a6.044 6.044 0 0 0 6.045-6.045v-7.108l1.356-1.355-1.282-1.283-.074-.073v-17.989h-38.689v23.43l-.146.146.146.147Z" clip-rule="evenodd"/></g><path stroke="#C9C9C9" stroke-width="2.418" d="M600.709 656.704c-31.384 0-56.825-25.441-56.825-56.824 0-31.384 25.441-56.825 56.825-56.825 31.383 0 56.824 25.441 56.824 56.825 0 31.383-25.441 56.824-56.824 56.824Z"/></g><defs><linearGradient id="a" x1="554.061" x2="-.48" y1=".083" y2=".087" gradientUnits="userSpaceOnUse"><stop stop-color="#C9C9C9" stop-opacity="0"/><stop offset=".208" stop-color="#C9C9C9"/><stop offset=".792" stop-color="#C9C9C9"/><stop offset="1" stop-color="#C9C9C9" stop-opacity="0"/></linearGradient><linearGradient id="b" x1="796.912" x2="404.507" y1="599.963" y2="599.965" gradientUnits="userSpaceOnUse"><stop stop-color="#C9C9C9" stop-opacity="0"/><stop offset=".208" stop-color="#C9C9C9"/><stop offset=".792" stop-color="#C9C9C9"/><stop offset="1" stop-color="#C9C9C9" stop-opacity="0"/></linearGradient><linearGradient id="c" x1="600.792" x2="600.794" y1="403.677" y2="796.082" gradientUnits="userSpaceOnUse"><stop stop-color="#C9C9C9" stop-opacity="0"/><stop offset=".208" stop-color="#C9C9C9"/><stop offset=".792" stop-color="#C9C9C9"/><stop offset="1" stop-color="#C9C9C9" stop-opacity="0"/></linearGradient><linearGradient id="d" x1="404.85" x2="796.972" y1="403.903" y2="796.02" gradientUnits="userSpaceOnUse"><stop stop-color="#C9C9C9" stop-opacity="0"/><stop offset=".208" stop-color="#C9C9C9"/><stop offset=".792" stop-color="#C9C9C9"/><stop offset="1" stop-color="#C9C9C9" stop-opacity="0"/></linearGradient><clipPath id="e"><path fill="#fff" d="M581.364 580.535h38.689v38.689h-38.689z"/></clipPath></defs></svg>
```

## File: dkl-microapp-2-main/styles/globals.css
```css
@tailwind base;
@tailwind components;
@tailwind utilities;

body {
  font-family: Arial, Helvetica, sans-serif;
}

@layer utilities {
  .text-balance {
    text-wrap: balance;
  }
}

@layer base {
  :root {
    --background: 0 0% 100%;
    --foreground: 0 0% 3.9%;
    --card: 0 0% 100%;
    --card-foreground: 0 0% 3.9%;
    --popover: 0 0% 100%;
    --popover-foreground: 0 0% 3.9%;
    --primary: 0 0% 9%;
    --primary-foreground: 0 0% 98%;
    --secondary: 0 0% 96.1%;
    --secondary-foreground: 0 0% 9%;
    --muted: 0 0% 96.1%;
    --muted-foreground: 0 0% 45.1%;
    --accent: 0 0% 96.1%;
    --accent-foreground: 0 0% 9%;
    --destructive: 0 84.2% 60.2%;
    --destructive-foreground: 0 0% 98%;
    --border: 0 0% 89.8%;
    --input: 0 0% 89.8%;
    --ring: 0 0% 3.9%;
    --chart-1: 12 76% 61%;
    --chart-2: 173 58% 39%;
    --chart-3: 197 37% 24%;
    --chart-4: 43 74% 66%;
    --chart-5: 27 87% 67%;
    --radius: 0.5rem;
    --sidebar-background: 0 0% 98%;
    --sidebar-foreground: 240 5.3% 26.1%;
    --sidebar-primary: 240 5.9% 10%;
    --sidebar-primary-foreground: 0 0% 98%;
    --sidebar-accent: 240 4.8% 95.9%;
    --sidebar-accent-foreground: 240 5.9% 10%;
    --sidebar-border: 220 13% 91%;
    --sidebar-ring: 217.2 91.2% 59.8%;
  }
  .dark {
    --background: 0 0% 3.9%;
    --foreground: 0 0% 98%;
    --card: 0 0% 3.9%;
    --card-foreground: 0 0% 98%;
    --popover: 0 0% 3.9%;
    --popover-foreground: 0 0% 98%;
    --primary: 0 0% 98%;
    --primary-foreground: 0 0% 9%;
    --secondary: 0 0% 14.9%;
    --secondary-foreground: 0 0% 98%;
    --muted: 0 0% 14.9%;
    --muted-foreground: 0 0% 63.9%;
    --accent: 0 0% 14.9%;
    --accent-foreground: 0 0% 98%;
    --destructive: 0 62.8% 30.6%;
    --destructive-foreground: 0 0% 98%;
    --border: 0 0% 14.9%;
    --input: 0 0% 14.9%;
    --ring: 0 0% 83.1%;
    --chart-1: 220 70% 50%;
    --chart-2: 160 60% 45%;
    --chart-3: 30 80% 55%;
    --chart-4: 280 65% 60%;
    --chart-5: 340 75% 55%;
    --sidebar-background: 240 5.9% 10%;
    --sidebar-foreground: 240 4.8% 95.9%;
    --sidebar-primary: 224.3 76.3% 48%;
    --sidebar-primary-foreground: 0 0% 100%;
    --sidebar-accent: 240 3.7% 15.9%;
    --sidebar-accent-foreground: 240 4.8% 95.9%;
    --sidebar-border: 240 3.7% 15.9%;
    --sidebar-ring: 217.2 91.2% 59.8%;
  }
}

@layer base {
  * {
    @apply border-border;
  }
  body {
    @apply bg-background text-foreground;
  }
}
```

## File: dkl-microapp-2-main/supabase/functions/geocode-properties/index.ts
```typescript
// Setup type definitions for built-in Supabase Runtime APIs
import "jsr:@supabase/functions-js/edge-runtime.d.ts"
import { createClient } from "jsr:@supabase/supabase-js@2"

// Configuration
const BATCH_SIZE = 10 // Number of listings to process in one go
const DELAY_BETWEEN_REQUESTS_MS = 200 // Delay to avoid hitting Mapbox API rate limits

// CORS headers
const corsHeaders = {
  "Access-Control-Allow-Origin": "*",
  "Access-Control-Allow-Headers": "authorization, x-client-info, apikey, content-type",
  "Access-Control-Allow-Methods": "POST, OPTIONS",
}

async function geocodeAddress(address: string, mapboxApiKey: string) {
  const url = `https://api.mapbox.com/geocoding/v5/mapbox.places/${encodeURIComponent(address)}.json?access_token=${mapboxApiKey}&limit=1`
  try {
    const response = await fetch(url)
    if (!response.ok) {
      console.error(`Mapbox API error: ${response.status} ${await response.text()}`)
      return null
    }
    const data = await response.json()
    if (data.features && data.features.length > 0) {
      const [longitude, latitude] = data.features[0].center
      return {
        latitude,
        longitude,
      }
    }
    return null
  } catch (error) {
    console.error("Error geocoding address:", error)
    return null
  }
}

Deno.serve(async (req) => {
  // Handle OPTIONS request for CORS preflight
  if (req.method === "OPTIONS") {
    return new Response("ok", {
      headers: corsHeaders,
    })
  }

  try {
    const supabaseUrl = Deno.env.get("SUPABASE_URL")
    const serviceRoleKey = Deno.env.get("SUPABASE_SERVICE_ROLE_KEY")
    const mapboxApiKey = Deno.env.get("MAPBOX_ACCESS_TOKEN")

    if (!supabaseUrl || !serviceRoleKey || !mapboxApiKey) {
      throw new Error("Missing environment variables: SUPABASE_URL, SUPABASE_SERVICE_ROLE_KEY, or MAPBOX_ACCESS_TOKEN")
    }

    // Create a Supabase client with the service role key for admin privileges
    const supabaseAdmin = createClient(supabaseUrl, serviceRoleKey)

    // Fetch listings that need geocoding
    // UPDATED: Changed from 'properties' to 'listings'
    const { data: listingsToGeocode, error: fetchError } = await supabaseAdmin
      .from("listings")
      .select("id, address_line_1, city, state, latitude, longitude")
      .or("latitude.is.null,longitude.is.null") // Listings missing either lat or lng
      .not("address_line_1", "is", null) // Must have address_line_1
      .not("city", "is", null) // Must have city
      .not("state", "is", null) // Must have state
      .limit(BATCH_SIZE)

    if (fetchError) {
      console.error("Error fetching listings:", fetchError) // UPDATED: Message text
      throw fetchError
    }

    if (!listingsToGeocode || listingsToGeocode.length === 0) {
      return new Response(
        JSON.stringify({
          success: true,
          message: "No listings found needing geocoding in this batch.", // UPDATED: Message text
          propertiesFound: 0, // Kept for client compatibility
          geocodedCount: 0,
          failedCount: 0,
          details: [],
        }),
        {
          headers: {
            ...corsHeaders,
            "Content-Type": "application/json",
          },
          status: 200,
        },
      )
    }

    let geocodedCount = 0
    let failedCount = 0
    const processingDetails = []

    for (const listing of listingsToGeocode) {
      // UPDATED: Variable name
      // Ensure all parts of the address are present before attempting to geocode
      if (!listing.address_line_1 || !listing.city || !listing.state) {
        processingDetails.push({
          id: listing.id,
          status: "skipped",
          reason: "Missing address components",
        })
        failedCount++
        continue
      }

      // Construct the full address string
      const fullAddress = `${listing.address_line_1}, ${listing.city}, ${listing.state}`
      const coordinates = await geocodeAddress(fullAddress, mapboxApiKey)

      if (coordinates) {
        // UPDATED: Changed from 'properties' to 'listings'
        const { error: updateError } = await supabaseAdmin
          .from("listings")
          .update({
            latitude: coordinates.latitude,
            longitude: coordinates.longitude,
          })
          .eq("id", listing.id)

        if (updateError) {
          console.error(`Error updating listing ${listing.id}:`, updateError) // UPDATED: Message text
          failedCount++
          processingDetails.push({
            id: listing.id,
            status: "failed_update",
            address: fullAddress,
            error: updateError.message,
          })
        } else {
          geocodedCount++
          processingDetails.push({
            id: listing.id,
            status: "success",
            address: fullAddress,
            coordinates,
          })
        }
      } else {
        failedCount++
        processingDetails.push({
          id: listing.id,
          status: "failed_geocode",
          address: fullAddress,
        })
        console.warn(`Failed to geocode address for listing ${listing.id}: ${fullAddress}`) // UPDATED: Message text
      }

      // Add a small delay between requests to Mapbox
      if (listingsToGeocode.indexOf(listing) < listingsToGeocode.length - 1) {
        await new Promise((resolve) => setTimeout(resolve, DELAY_BETWEEN_REQUESTS_MS))
      }
    }

    return new Response(
      JSON.stringify({
        success: true,
        message: `Batch processing complete. Processed: ${listingsToGeocode.length}, Geocoded: ${geocodedCount}, Failed: ${failedCount}.`,
        propertiesFound: listingsToGeocode.length, // Kept for client compatibility
        geocodedCount,
        failedCount,
        details: processingDetails,
      }),
      {
        headers: {
          ...corsHeaders,
          "Content-Type": "application/json",
        },
        status: 200,
      },
    )
  } catch (err) {
    console.error("Main function error:", err)
    return new Response(
      JSON.stringify({
        success: false,
        error: err?.message ?? String(err),
        propertiesFound: 0, // Kept for client compatibility
        geocodedCount: 0,
        failedCount: 0,
      }),
      {
        headers: {
          ...corsHeaders,
          "Content-Type": "application/json",
        },
        status: 500,
      },
    )
  }
})
```

## File: dkl-microapp-2-main/supabase/migrations/001_add_user_field_mappings.sql
```sql
-- Create user_field_mappings table
CREATE TABLE IF NOT EXISTS public.user_field_mappings (
    id UUID DEFAULT gen_random_uuid() PRIMARY KEY,
    user_id UUID NOT NULL REFERENCES auth.users(id) ON DELETE CASCADE,
    target_table_name VARCHAR(255) NOT NULL, -- e.g., 'properties', 'builders'
    target_database_column VARCHAR(255) NOT NULL, -- e.g., 'mls_number', 'status'
    source_csv_header VARCHAR(255) NOT NULL, -- Normalized CSV header provided by user
    created_at TIMESTAMP WITH TIME ZONE DEFAULT TIMEZONE('utc', NOW()),
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT TIMEZONE('utc', NOW()),
    CONSTRAINT user_field_mappings_user_table_csv_header_unique UNIQUE (user_id, target_table_name, source_csv_header)
);

COMMENT ON TABLE public.user_field_mappings IS 'Stores user-defined mappings from CSV headers to database columns.';
COMMENT ON COLUMN public.user_field_mappings.target_table_name IS 'The name of the database table (e.g., ''properties'', ''builders'').';
COMMENT ON COLUMN public.user_field_mappings.target_database_column IS 'The name of the column in the target_table_name.';
COMMENT ON COLUMN public.user_field_mappings.source_csv_header IS 'The user-defined CSV header (normalized) that maps to the target_database_column.';

-- Create indexes
CREATE INDEX IF NOT EXISTS idx_user_field_mappings_user_table_db_column
ON public.user_field_mappings(user_id, target_table_name, target_database_column);

-- Enable RLS
ALTER TABLE public.user_field_mappings ENABLE ROW LEVEL SECURITY;

-- RLS Policies
CREATE POLICY "Users can manage their own field mappings"
ON public.user_field_mappings
FOR ALL
USING (auth.uid() = user_id);

-- Trigger for updated_at
DROP TRIGGER IF EXISTS update_user_field_mappings_updated_at ON public.user_field_mappings;
CREATE TRIGGER update_user_field_mappings_updated_at
BEFORE UPDATE ON public.user_field_mappings
FOR EACH ROW
EXECUTE FUNCTION update_updated_at_column();
```

## File: dkl-microapp-2-main/supabase/migrations/002_add_mapbox_key_to_user_settings.sql
```sql
-- Add mapbox_api_key column to user_settings table
    ALTER TABLE public.user_settings
    ADD COLUMN IF NOT EXISTS mapbox_api_key TEXT NULL;

    COMMENT ON COLUMN public.user_settings.mapbox_api_key IS 'Stores the Mapbox API key for the user';

    -- Output a success message
    SELECT 'Column mapbox_api_key added to user_settings successfully.' AS result;
```

## File: dkl-microapp-2-main/supabase/migrations/003_update_existing_mappings.sql
```sql
-- Description: Updates existing user field mappings from the old 'properties' table name to the new 'listings' table name.
    -- This ensures that previously saved CSV import mappings continue to work after the table rename.
    UPDATE public.user_field_mappings
    SET target_table_name = 'listings'
    WHERE target_table_name = 'properties';

    -- Description: Updates the foreign key relationship in social_post_properties.
    -- This renames the relationship name that Supabase uses for joins from 'properties' to 'listings'.
    -- Note: This assumes the constraint was named 'social_post_properties_property_id_fkey'.
    -- You may need to verify the actual constraint name in your Supabase dashboard.
    ALTER TABLE public.social_post_properties
    DROP CONSTRAINT IF EXISTS social_post_properties_property_id_fkey,
    ADD CONSTRAINT social_post_properties_property_id_fkey
        FOREIGN KEY (property_id)
        REFERENCES public.listings(id)
        ON DELETE CASCADE;
```

## File: dkl-microapp-2-main/supabase/schema.sql
```sql
-- Main schema definition for the Attio clone project
-- Drop existing tables if they exist (optional, for a clean slate during development)
DROP TABLE IF EXISTS public.social_post_properties CASCADE;
DROP TABLE IF EXISTS public.social_posts CASCADE;
DROP TABLE IF EXISTS public.csv_uploads CASCADE;
DROP TABLE IF EXISTS public.user_field_mappings CASCADE;
DROP TABLE IF EXISTS public.listings CASCADE; -- Changed from properties
DROP TABLE IF EXISTS public.builders CASCADE;
DROP TABLE IF EXISTS public.user_settings CASCADE;

-- Extensions
CREATE EXTENSION IF NOT EXISTS "uuid-ossp" WITH SCHEMA extensions;

-- Builders Table
CREATE TABLE public.builders (
    id uuid DEFAULT extensions.uuid_generate_v4() PRIMARY KEY,
    name TEXT NOT NULL,
    company_name TEXT,
    phone TEXT,
    email TEXT,
    website TEXT,
    address TEXT,
    city TEXT,
    state TEXT,
    zip_code TEXT,
    years_in_business INTEGER,
    total_projects INTEGER,
    active_projects INTEGER,
    specialties TEXT[],
    price_range_min NUMERIC,
    price_range_max NUMERIC,
    rating NUMERIC,
    notes TEXT,
    metadata JSONB,
    created_at TIMESTAMPTZ DEFAULT now() NOT NULL,
    updated_at TIMESTAMPTZ DEFAULT now() NOT NULL
);

-- Listings Table (formerly Properties)
CREATE TABLE public.listings (
    id uuid DEFAULT extensions.uuid_generate_v4() PRIMARY KEY,
    mls_number TEXT UNIQUE, -- Assuming MLS number should be unique for listings
    category TEXT,
    status TEXT,
    type TEXT,
    dom INTEGER,
    cdom INTEGER,
    list_date DATE,
    agreement_date DATE,
    off_market_date DATE,
    settled_date DATE,
    original_price NUMERIC,
    list_price NUMERIC,
    sold_price NUMERIC,
    street_number TEXT,
    street_direction TEXT,
    street_name TEXT,
    unit_number TEXT,
    city TEXT,
    state TEXT,
    zip_code TEXT,
    county TEXT,
    mls_area TEXT,
    subdivision TEXT,
    list_agent_name TEXT,
    list_agent_code TEXT,
    list_office_name TEXT,
    list_office_code TEXT,
    list_office_phone TEXT,
    selling_agent TEXT,
    selling_agent_code TEXT,
    selling_office_name TEXT,
    selling_office_code TEXT,
    selling_office_phone TEXT,
    final_financing TEXT,
    final_short_sale BOOLEAN,
    final_third_party_approval BOOLEAN,
    final_bank_owned BOOLEAN,
    tax_annual_total NUMERIC,
    tax_year INTEGER,
    acres_total NUMERIC,
    land_use_code TEXT,
    ownership TEXT,
    senior_community BOOLEAN,
    condo_coop_assoc BOOLEAN,
    hoa BOOLEAN,
    one_time_association_fee NUMERIC,
    association_fee NUMERIC,
    association_fee_frequency TEXT,
    age INTEGER,
    interior_sqft INTEGER,
    property_condition TEXT,
    bedrooms INTEGER,
    baths_full INTEGER,
    baths_half INTEGER,
    design TEXT,
    style TEXT,
    number_of_stories TEXT,
    floor_number TEXT,
    basement BOOLEAN,
    garage_spaces INTEGER,
    fireplace BOOLEAN,
    laundry TEXT,
    other_rooms TEXT,
    room_count INTEGER,
    central_air BOOLEAN,
    waterfront BOOLEAN,
    new_construction BOOLEAN,
    model_name TEXT,
    originating_mls TEXT,
    above_grade_sqft INTEGER,
    below_grade_sqft INTEGER,
    home_built TEXT,
    basement_footprint_pct NUMERIC,
    basement_finished_pct NUMERIC,
    builder_id uuid REFERENCES public.builders(id) ON DELETE SET NULL,
    development_status TEXT,
    metadata JSONB,
    created_at TIMESTAMPTZ DEFAULT now() NOT NULL,
    updated_at TIMESTAMPTZ DEFAULT now() NOT NULL,
    in_social_queue BOOLEAN DEFAULT FALSE,
    owner_name TEXT,
    construction_completed_yn BOOLEAN,
    year_built INTEGER,
    year_built_source TEXT,
    imported_builder_name TEXT,
    occupant_type TEXT,
    occupant_name TEXT,
    previous_list_price NUMERIC,
    architect_name TEXT,
    structure_type TEXT,
    block_lot TEXT,
    remarks_private TEXT,
    remarks_public TEXT,
    year_major_reno_remodel INTEGER,
    change_info TEXT,
    close_date DATE,
    close_price NUMERIC,
    close_sale_type TEXT,
    foundation_details TEXT,
    land_assessed_value NUMERIC,
    list_picture_url TEXT,
    lot_features TEXT[],
    lot_size_sqft NUMERIC,
    address_line_1 TEXT, -- Combined address for easier geocoding if components are missing
    latitude NUMERIC,
    longitude NUMERIC,
    last_sold_date DATE,
    last_sold_price NUMERIC,
    property_type TEXT, -- Retained, ensure it's used consistently
    description TEXT, -- Retained
    new_construction_details TEXT -- Retained
);

-- User Settings Table
CREATE TABLE public.user_settings (
    id uuid DEFAULT extensions.uuid_generate_v4() PRIMARY KEY,
    user_id uuid REFERENCES auth.users(id) ON DELETE CASCADE UNIQUE NOT NULL,
    theme TEXT DEFAULT 'light'::text,
    notifications_enabled BOOLEAN DEFAULT true,
    email_notifications BOOLEAN DEFAULT true,
    default_view TEXT DEFAULT 'grid'::text,
    items_per_page INTEGER DEFAULT 50,
    metadata JSONB,
    created_at TIMESTAMPTZ DEFAULT now() NOT NULL,
    updated_at TIMESTAMPTZ DEFAULT now() NOT NULL,
    openai_api_key TEXT,
    openai_model TEXT,
    primary_color_hex TEXT,
    primary_foreground_color_hex TEXT,
    mapbox_api_key TEXT
);

-- CSV Uploads Table
CREATE TABLE public.csv_uploads (
    id uuid DEFAULT extensions.uuid_generate_v4() PRIMARY KEY,
    user_id uuid REFERENCES auth.users(id) ON DELETE SET NULL,
    filename TEXT,
    upload_date TIMESTAMPTZ DEFAULT now() NOT NULL,
    records_processed INTEGER,
    records_created INTEGER,
    records_updated INTEGER,
    records_failed INTEGER,
    status TEXT,
    error_log TEXT,
    metadata JSONB
);

-- Social Posts Table
CREATE TABLE public.social_posts (
    id uuid DEFAULT extensions.uuid_generate_v4() PRIMARY KEY,
    user_id uuid REFERENCES auth.users(id) ON DELETE CASCADE,
    title TEXT NOT NULL,
    description TEXT,
    status TEXT DEFAULT 'draft'::text NOT NULL, -- e.g., draft, scheduled, posted, error
    post_url TEXT, -- URL of the live post
    content_type TEXT, -- e.g., 'Single Property', 'Multi Property', 'Market Update'
    format_type TEXT, -- e.g., 'Carousel', 'Post', 'Reel', 'Story'
    created_at TIMESTAMPTZ DEFAULT now() NOT NULL,
    updated_at TIMESTAMPTZ DEFAULT now() NOT NULL
);

-- Social Post Properties Junction Table
CREATE TABLE public.social_post_properties (
    id uuid DEFAULT extensions.uuid_generate_v4() PRIMARY KEY,
    social_post_id uuid REFERENCES public.social_posts(id) ON DELETE CASCADE NOT NULL,
    property_id uuid REFERENCES public.listings(id) ON DELETE CASCADE NOT NULL, -- Changed from properties
    image_complete BOOLEAN DEFAULT FALSE,
    description_complete BOOLEAN DEFAULT FALSE,
    contacted_complete BOOLEAN DEFAULT FALSE,
    image_urls TEXT[], -- Array of URLs for images specific to this property in this post
    description TEXT, -- Description specific to this property in this post
    created_at TIMESTAMPTZ DEFAULT now() NOT NULL,
    UNIQUE (social_post_id, property_id) -- Ensure a property is linked only once per post
);

-- User Field Mappings Table
CREATE TABLE public.user_field_mappings (
    id uuid DEFAULT extensions.uuid_generate_v4() PRIMARY KEY,
    user_id uuid REFERENCES auth.users(id) ON DELETE CASCADE NOT NULL,
    target_table_name TEXT NOT NULL, -- e.g., 'listings', 'builders'
    target_database_column TEXT NOT NULL,
    source_csv_header TEXT NOT NULL,
    created_at TIMESTAMPTZ DEFAULT now() NOT NULL,
    updated_at TIMESTAMPTZ DEFAULT now() NOT NULL,
    UNIQUE (user_id, target_table_name, source_csv_header) -- A CSV header can only map to one DB column for a user and table
    -- Consider adding: UNIQUE (user_id, target_table_name, target_database_column) if a DB column can only be mapped by one CSV header
);

-- Function to update 'updated_at' column
CREATE OR REPLACE FUNCTION public.update_updated_at_column()
RETURNS TRIGGER AS $$
BEGIN
   NEW.updated_at = now();
   RETURN NEW;
END;
$$ language 'plpgsql';

-- Triggers for 'updated_at'
CREATE TRIGGER update_builders_updated_at BEFORE UPDATE ON public.builders FOR EACH ROW EXECUTE FUNCTION public.update_updated_at_column();
CREATE TRIGGER update_listings_updated_at BEFORE UPDATE ON public.listings FOR EACH ROW EXECUTE FUNCTION public.update_updated_at_column(); -- Changed
CREATE TRIGGER update_user_settings_updated_at BEFORE UPDATE ON public.user_settings FOR EACH ROW EXECUTE FUNCTION public.update_updated_at_column();
CREATE TRIGGER update_social_posts_updated_at BEFORE UPDATE ON public.social_posts FOR EACH ROW EXECUTE FUNCTION public.update_updated_at_column();
CREATE TRIGGER update_user_field_mappings_updated_at BEFORE UPDATE ON public.user_field_mappings FOR EACH ROW EXECUTE FUNCTION public.update_updated_at_column();

-- Enable Row Level Security (RLS) for all tables
ALTER TABLE public.builders ENABLE ROW LEVEL SECURITY;
ALTER TABLE public.listings ENABLE ROW LEVEL SECURITY; -- Changed
ALTER TABLE public.user_settings ENABLE ROW LEVEL SECURITY;
ALTER TABLE public.csv_uploads ENABLE ROW LEVEL SECURITY;
ALTER TABLE public.social_posts ENABLE ROW LEVEL SECURITY;
ALTER TABLE public.social_post_properties ENABLE ROW LEVEL SECURITY;
ALTER TABLE public.user_field_mappings ENABLE ROW LEVEL SECURITY;

-- Policies for user_settings
DROP POLICY IF EXISTS "Allow individual read access on user_settings" ON public.user_settings;
CREATE POLICY "Allow individual read access on user_settings" ON public.user_settings
    FOR SELECT USING (auth.uid() = user_id);

DROP POLICY IF EXISTS "Allow individual update access on user_settings" ON public.user_settings;
CREATE POLICY "Allow individual update access on user_settings" ON public.user_settings
    FOR UPDATE USING (auth.uid() = user_id) WITH CHECK (auth.uid() = user_id);

DROP POLICY IF EXISTS "Allow individual insert access on user_settings" ON public.user_settings;
CREATE POLICY "Allow individual insert access on user_settings" ON public.user_settings
    FOR INSERT WITH CHECK (auth.uid() = user_id);

-- Policies for builders (assuming builders are public or managed by auth users)
DROP POLICY IF EXISTS "Allow public read access on builders" ON public.builders;
CREATE POLICY "Allow public read access on builders" ON public.builders
    FOR SELECT USING (true); -- Or auth.role() = 'authenticated' if only for logged-in users

DROP POLICY IF EXISTS "Allow authenticated users to insert builders" ON public.builders;
CREATE POLICY "Allow authenticated users to insert builders" ON public.builders
    FOR INSERT TO authenticated WITH CHECK (true);

DROP POLICY IF EXISTS "Allow authenticated users to update builders" ON public.builders;
CREATE POLICY "Allow authenticated users to update builders" ON public.builders
    FOR UPDATE TO authenticated USING (true) WITH CHECK (true); -- More specific ownership checks can be added

DROP POLICY IF EXISTS "Allow authenticated users to delete builders" ON public.builders;
CREATE POLICY "Allow authenticated users to delete builders" ON public.builders
    FOR DELETE TO authenticated USING (true); -- More specific ownership checks can be added


-- Policies for listings (assuming listings are public or managed by auth users)
DROP POLICY IF EXISTS "Allow public read access on listings" ON public.listings;
CREATE POLICY "Allow public read access on listings" ON public.listings
    FOR SELECT USING (true); -- Or auth.role() = 'authenticated'

DROP POLICY IF EXISTS "Allow authenticated users to insert listings" ON public.listings;
CREATE POLICY "Allow authenticated users to insert listings" ON public.listings
    FOR INSERT TO authenticated WITH CHECK (true);

DROP POLICY IF EXISTS "Allow authenticated users to update listings" ON public.listings;
CREATE POLICY "Allow authenticated users to update listings" ON public.listings
    FOR UPDATE TO authenticated USING (true) WITH CHECK (true);

DROP POLICY IF EXISTS "Allow authenticated users to delete listings" ON public.listings;
CREATE POLICY "Allow authenticated users to delete listings" ON public.listings
    FOR DELETE TO authenticated USING (true);


-- Policies for csv_uploads (user-specific)
DROP POLICY IF EXISTS "Allow individual access on csv_uploads" ON public.csv_uploads;
CREATE POLICY "Allow individual access on csv_uploads" ON public.csv_uploads
    FOR ALL USING (auth.uid() = user_id) WITH CHECK (auth.uid() = user_id);

-- Policies for social_posts (user-specific)
DROP POLICY IF EXISTS "Allow individual access on social_posts" ON public.social_posts;
CREATE POLICY "Allow individual access on social_posts" ON public.social_posts
    FOR ALL USING (auth.uid() = user_id) WITH CHECK (auth.uid() = user_id);

-- Policies for social_post_properties (derived from social_posts ownership)
DROP POLICY IF EXISTS "Allow access based on social_post ownership" ON public.social_post_properties;
CREATE POLICY "Allow access based on social_post ownership" ON public.social_post_properties
    FOR ALL USING (
        EXISTS (
            SELECT 1 FROM public.social_posts sp
            WHERE sp.id = social_post_id AND sp.user_id = auth.uid()
        )
    ) WITH CHECK (
         EXISTS (
            SELECT 1 FROM public.social_posts sp
            WHERE sp.id = social_post_id AND sp.user_id = auth.uid()
        )
    );

-- Policies for user_field_mappings (user-specific)
DROP POLICY IF EXISTS "Allow individual access on user_field_mappings" ON public.user_field_mappings;
CREATE POLICY "Allow individual access on user_field_mappings" ON public.user_field_mappings
    FOR ALL USING (auth.uid() = user_id) WITH CHECK (auth.uid() = user_id);

-- Seed initial data (optional)
-- Example: INSERT INTO public.user_settings (user_id, theme) VALUES ('your-user-id', 'dark');
```

## File: dkl-microapp-2-main/supabase/seed-social-posts.sql
```sql
-- Insert a sample social post
INSERT INTO social_posts (
  title, 
  description, 
  status, 
  user_id
) VALUES (
  'Luxury Homes Showcase', 
  'Featuring our top luxury properties in the DC area',
  'draft',
  (SELECT auth.uid())
);

-- Get the ID of the social post we just created
DO $$
DECLARE
  social_post_id UUID;
BEGIN
  SELECT id INTO social_post_id FROM social_posts ORDER BY created_at DESC LIMIT 1;
  
  -- Add properties to the social post
  INSERT INTO social_post_properties (
    social_post_id,
    property_id,
    image_complete,
    description_complete,
    contacted_complete
  )
  SELECT 
    social_post_id,
    id,
    CASE WHEN random() > 0.5 THEN true ELSE false END,
    CASE WHEN random() > 0.5 THEN true ELSE false END,
    CASE WHEN random() > 0.5 THEN true ELSE false END
  FROM properties
  WHERE mls_number IN ('DC2024001', 'MD2024002', 'VA2024003')
  AND in_social_queue = true;
  
  -- Remove these properties from the queue
  UPDATE properties
  SET in_social_queue = false
  WHERE mls_number IN ('DC2024001', 'MD2024002', 'VA2024003');
END $$;
```

## File: dkl-microapp-2-main/supabase/social-schema.sql
```sql
-- Create social_posts table
CREATE TABLE IF NOT EXISTS social_posts (
  id UUID DEFAULT gen_random_uuid() PRIMARY KEY,
  title VARCHAR(255) NOT NULL,
  description TEXT,
  status VARCHAR(50) DEFAULT 'draft', -- 'draft', 'completed', 'posted'
  post_url VARCHAR(500),
  created_at TIMESTAMP WITH TIME ZONE DEFAULT TIMEZONE('utc', NOW()),
  updated_at TIMESTAMP WITH TIME ZONE DEFAULT TIMEZONE('utc', NOW()),
  user_id UUID REFERENCES auth.users(id)
);

-- Create social_post_properties table (junction table)
CREATE TABLE IF NOT EXISTS social_post_properties (
  id UUID DEFAULT gen_random_uuid() PRIMARY KEY,
  social_post_id UUID REFERENCES social_posts(id) ON DELETE CASCADE,
  property_id UUID REFERENCES properties(id) ON DELETE CASCADE,
  image_complete BOOLEAN DEFAULT false,
  description_complete BOOLEAN DEFAULT false,
  contacted_complete BOOLEAN DEFAULT false,
  created_at TIMESTAMP WITH TIME ZONE DEFAULT TIMEZONE('utc', NOW()),
  UNIQUE(social_post_id, property_id)
);

-- Add social_queue column to properties
ALTER TABLE properties ADD COLUMN IF NOT EXISTS in_social_queue BOOLEAN DEFAULT false;

-- Create indexes
CREATE INDEX IF NOT EXISTS idx_social_posts_user_id ON social_posts(user_id);
CREATE INDEX IF NOT EXISTS idx_social_posts_status ON social_posts(status);
CREATE INDEX IF NOT EXISTS idx_social_post_properties_post_id ON social_post_properties(social_post_id);
CREATE INDEX IF NOT EXISTS idx_social_post_properties_property_id ON social_post_properties(property_id);
CREATE INDEX IF NOT EXISTS idx_properties_social_queue ON properties(in_social_queue);

-- Create updated_at trigger for social_posts
DROP TRIGGER IF EXISTS update_social_posts_updated_at ON social_posts;
CREATE TRIGGER update_social_posts_updated_at BEFORE UPDATE ON social_posts
  FOR EACH ROW EXECUTE FUNCTION update_updated_at_column();

-- Enable RLS
ALTER TABLE social_posts ENABLE ROW LEVEL SECURITY;
ALTER TABLE social_post_properties ENABLE ROW LEVEL SECURITY;

-- Create RLS policies
CREATE POLICY "Users can manage own social posts" ON social_posts
  FOR ALL USING (auth.uid() = user_id);

CREATE POLICY "Users can manage social post properties" ON social_post_properties
  FOR ALL USING (
    EXISTS (
      SELECT 1 FROM social_posts 
      WHERE social_posts.id = social_post_properties.social_post_id 
      AND social_posts.user_id = auth.uid()
    )
  );
```

## File: dkl-microapp-2-main/supabase/update-schema.sql
```sql
-- Ensure builder_id column exists in properties table
ALTER TABLE properties ADD COLUMN IF NOT EXISTS builder_id UUID REFERENCES builders(id);

-- Create index for better performance
CREATE INDEX IF NOT EXISTS idx_properties_builder_id ON properties(builder_id);

-- Update some existing properties to have builders assigned
UPDATE properties 
SET builder_id = (
  SELECT id FROM builders 
  WHERE name = 'Toll Brothers' 
  LIMIT 1
)
WHERE mls_number IN ('DC2024001', 'MD2024002', 'VA2024003');

UPDATE properties 
SET builder_id = (
  SELECT id FROM builders 
  WHERE name = 'Ryan Homes' 
  LIMIT 1
)
WHERE mls_number IN ('DC2024004', 'MD2024005', 'VA2024006');
```

## File: dkl-microapp-2-main/types/supabase.ts
```typescript
export type Json = string | number | boolean | null | { [key: string]: Json | undefined } | Json[]

export interface Database {
  public: {
    Tables: {
      builders: {
        Row: {
          id: string
          name: string
          company_name: string | null
          phone: string | null
          email: string | null
          website: string | null
          address: string | null
          city: string | null
          state: string | null
          zip_code: string | null
          years_in_business: number | null
          total_projects: number | null
          active_projects: number | null
          specialties: string[] | null
          price_range_min: number | null
          price_range_max: number | null
          rating: number | null
          notes: string | null
          metadata: Json | null
          created_at: string
          updated_at: string
        }
        Insert: Omit<Database["public"]["Tables"]["builders"]["Row"], "id" | "created_at" | "updated_at"> & {
          id?: string
          created_at?: string
          updated_at?: string
        }
        Update: Partial<Database["public"]["Tables"]["builders"]["Row"]>
      }
      listings: {
        // Renamed from properties
        Row: {
          id: string
          mls_number: string | null
          category: string | null
          status: string | null
          type: string | null
          dom: number | null
          cdom: number | null
          list_date: string | null
          agreement_date: string | null
          off_market_date: string | null
          settled_date: string | null
          original_price: number | null
          list_price: number | null
          sold_price: number | null
          street_number: string | null
          street_direction: string | null
          street_name: string | null
          unit_number: string | null
          city: string | null
          state: string | null
          zip_code: string | null
          county: string | null
          mls_area: string | null
          subdivision: string | null
          list_agent_name: string | null
          list_agent_code: string | null
          list_office_name: string | null
          list_office_code: string | null
          list_office_phone: string | null
          selling_agent: string | null
          selling_agent_code: string | null
          selling_office_name: string | null
          selling_office_code: string | null
          selling_office_phone: string | null
          final_financing: string | null
          final_short_sale: boolean | null
          final_third_party_approval: boolean | null
          final_bank_owned: boolean | null
          tax_annual_total: number | null
          tax_year: number | null
          acres_total: number | null
          land_use_code: string | null
          ownership: string | null
          senior_community: boolean | null
          condo_coop_assoc: boolean | null
          hoa: boolean | null
          one_time_association_fee: number | null
          association_fee: number | null
          association_fee_frequency: string | null
          age: number | null
          interior_sqft: number | null
          property_condition: string | null
          bedrooms: number | null
          baths_full: number | null
          baths_half: number | null
          design: string | null
          style: string | null
          number_of_stories: string | null
          floor_number: string | null
          basement: boolean | null
          garage_spaces: number | null
          fireplace: boolean | null
          laundry: string | null
          other_rooms: string | null
          room_count: number | null
          central_air: boolean | null
          waterfront: boolean | null
          new_construction: boolean | null
          model_name: string | null
          originating_mls: string | null
          above_grade_sqft: number | null
          below_grade_sqft: number | null
          home_built: string | null
          basement_footprint_pct: number | null
          basement_finished_pct: number | null
          builder_id: string | null
          development_status: string | null
          metadata: Json | null
          created_at: string
          updated_at: string
          in_social_queue: boolean | null
          owner_name: string | null
          construction_completed_yn: boolean | null
          year_built: number | null
          year_built_source: string | null
          imported_builder_name: string | null
          occupant_type: string | null
          occupant_name: string | null
          previous_list_price: number | null
          architect_name: string | null
          structure_type: string | null
          block_lot: string | null
          remarks_private: string | null
          remarks_public: string | null
          year_major_reno_remodel: number | null
          change_info: string | null
          close_date: string | null
          close_price: number | null
          close_sale_type: string | null
          foundation_details: string | null
          land_assessed_value: number | null
          list_picture_url: string | null
          lot_features: string[] | null
          lot_size_sqft: number | null
          address_line_1: string | null
          latitude: number | null
          longitude: number | null
          last_sold_date: string | null
          last_sold_price: number | null
          property_type: string | null // Retained from previous, ensure it's in schema if used
          description: string | null // Retained from previous, ensure it's in schema if used
          new_construction_details: string | null // Retained from previous
        }
        Insert: Omit<Database["public"]["Tables"]["listings"]["Row"], "id" | "created_at" | "updated_at"> & {
          // Renamed
          id?: string
          created_at?: string
          updated_at?: string
        }
        Update: Partial<Database["public"]["Tables"]["listings"]["Row"]> // Renamed
      }
      user_settings: {
        Row: {
          id: string
          user_id: string
          theme: string
          notifications_enabled: boolean
          email_notifications: boolean
          default_view: string
          items_per_page: number
          metadata: Json | null
          created_at: string
          updated_at: string
          openai_api_key: string | null
          openai_model: string | null
          primary_color_hex: string | null
          primary_foreground_color_hex: string | null
          mapbox_api_key: string | null
        }
        Insert: Omit<Database["public"]["Tables"]["user_settings"]["Row"], "id" | "created_at" | "updated_at"> & {
          id?: string
          created_at?: string
          updated_at?: string
          openai_api_key?: string | null
          openai_model?: string | null
          primary_color_hex?: string | null
          primary_foreground_color_hex?: string | null
          mapbox_api_key?: string | null
        }
        Update: Partial<Database["public"]["Tables"]["user_settings"]["Row"]> & {
          openai_api_key?: string | null
          openai_model?: string | null
          primary_color_hex?: string | null
          primary_foreground_color_hex?: string | null
          mapbox_api_key?: string | null
        }
      }
      csv_uploads: {
        Row: {
          id: string
          user_id: string | null
          filename: string | null
          upload_date: string
          records_processed: number | null
          records_created: number | null
          records_updated: number | null
          records_failed: number | null
          status: string | null
          error_log: string | null
          metadata: Json | null
        }
        Insert: Omit<Database["public"]["Tables"]["csv_uploads"]["Row"], "id" | "upload_date"> & {
          id?: string
          upload_date?: string
        }
        Update: Partial<Database["public"]["Tables"]["csv_uploads"]["Row"]>
      }
      social_posts: {
        Row: {
          id: string
          title: string
          description: string | null
          status: string
          post_url: string | null
          created_at: string
          updated_at: string
          user_id: string | null
          content_type: string | null
          format_type: string | null
        }
        Insert: Omit<Database["public"]["Tables"]["social_posts"]["Row"], "id" | "created_at" | "updated_at"> & {
          id?: string
          created_at?: string
          updated_at?: string
          content_type?: string | null
          format_type?: string | null
        }
        Update: Partial<Database["public"]["Tables"]["social_posts"]["Row"]> & {
          content_type?: string | null
          format_type?: string | null
        }
      }
      social_post_properties: {
        // Name remains, but property_id now refers to listings.id
        Row: {
          id: string
          social_post_id: string
          property_id: string // This ID now points to a row in the 'listings' table
          image_complete: boolean
          description_complete: boolean
          contacted_complete: boolean
          created_at: string
          image_urls: string[] | null // Added from social-post-property-item.tsx
          description: string | null // Added from social-post-property-item.tsx
        }
        Insert: Omit<Database["public"]["Tables"]["social_post_properties"]["Row"], "id" | "created_at"> & {
          id?: string
          created_at?: string
        }
        Update: Partial<Database["public"]["Tables"]["social_post_properties"]["Row"]>
      }
      user_field_mappings: {
        Row: {
          id: string
          user_id: string
          target_table_name: string // This will now store 'listings' for new mappings
          target_database_column: string
          source_csv_header: string
          created_at: string
          updated_at: string
        }
        Insert: Omit<Database["public"]["Tables"]["user_field_mappings"]["Row"], "id" | "created_at" | "updated_at"> & {
          id?: string
          created_at?: string
          updated_at?: string
        }
        Update: Partial<
          Omit<Database["public"]["Tables"]["user_field_mappings"]["Row"], "id" | "user_id" | "created_at">
        >
      }
    }
    Functions: {
      update_updated_at_column: {
        Args: Record<string, unknown>
        Returns: unknown
      }
    }
    Enums: {}
    CompositeTypes: {}
  }
}
```

## File: dkl-microapp-2-main/.gitignore
```
# See https://help.github.com/articles/ignoring-files/ for more about ignoring files.

# dependencies
/node_modules

# next.js
/.next/
/out/

# production
/build

# debug
npm-debug.log*
yarn-debug.log*
yarn-error.log*
.pnpm-debug.log*

# env files
.env*

# vercel
.vercel

# typescript
*.tsbuildinfo
next-env.d.ts
```

## File: dkl-microapp-2-main/components.json
```json
{
  "$schema": "https://ui.shadcn.com/schema.json",
  "style": "default",
  "rsc": true,
  "tsx": true,
  "tailwind": {
    "config": "tailwind.config.ts",
    "css": "app/globals.css",
    "baseColor": "neutral",
    "cssVariables": true,
    "prefix": ""
  },
  "aliases": {
    "components": "@/components",
    "utils": "@/lib/utils",
    "ui": "@/components/ui",
    "lib": "@/lib",
    "hooks": "@/hooks"
  },
  "iconLibrary": "lucide"
}
```

## File: dkl-microapp-2-main/next.config.mjs
```
/** @type {import('next').NextConfig} */
const nextConfig = {
  eslint: {
    ignoreDuringBuilds: true,
  },
  typescript: {
    ignoreBuildErrors: true,
  },
  images: {
    unoptimized: true,
  },
}

export default nextConfig
```

## File: dkl-microapp-2-main/package.json
```json
{
  "name": "real-estate-platform",
  "version": "0.1.0",
  "private": true,
  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start",
    "lint": "next lint"
  },
  "dependencies": {
    "@ai-sdk/openai": "latest",
    "@radix-ui/react-alert-dialog": "^1.0.5",
    "@radix-ui/react-avatar": "^1.0.4",
    "@radix-ui/react-checkbox": "latest",
    "@radix-ui/react-dialog": "latest",
    "@radix-ui/react-dropdown-menu": "^2.0.6",
    "@radix-ui/react-label": "^2.0.2",
    "@radix-ui/react-progress": "latest",
    "@radix-ui/react-select": "latest",
    "@radix-ui/react-slot": "^1.0.2",
    "@radix-ui/react-switch": "latest",
    "@radix-ui/react-tabs": "latest",
    "@radix-ui/react-toast": "latest",
    "@supabase/supabase-js": "latest",
    "@tanstack/react-table": "latest",
    "ai": "latest",
    "class-variance-authority": "^0.7.1",
    "clsx": "^2.1.1",
    "jsr:": "supabase",
    "lucide-react": "^0.454.0",
    "mapbox-gl": "latest",
    "next": "14.2.16",
    "papaparse": "latest",
    "react": "^18",
    "react-dom": "^18",
    "react-dropzone": "latest",
    "recharts": "latest",
    "tailwind-merge": "^2.5.5",
    "tailwindcss-animate": "^1.0.7",
    "zod": "latest"
  },
  "devDependencies": {
    "@types/node": "^22",
    "@types/react": "^18",
    "@types/react-dom": "^18",
    "autoprefixer": "^10.0.1",
    "eslint": "^8",
    "eslint-config-next": "14.1.0",
    "postcss": "^8.5",
    "tailwindcss": "^3.3.0",
    "typescript": "^5"
  }
}
```

## File: dkl-microapp-2-main/postcss.config.mjs
```
/** @type {import('postcss-load-config').Config} */
const config = {
  plugins: {
    tailwindcss: {},
  },
};

export default config;
```

## File: dkl-microapp-2-main/README.md
```markdown
# Attio clone project

*Automatically synced with your [v0.dev](https://v0.dev) deployments*

[![Deployed on Vercel](https://img.shields.io/badge/Deployed%20on-Vercel-black?style=for-the-badge&logo=vercel)](https://vercel.com/alexander-leanos-projects/v0-attio-clone-project-a0)
[![Built with v0](https://img.shields.io/badge/Built%20with-v0.dev-black?style=for-the-badge)](https://v0.dev/chat/projects/D4LOmdOGoSu)

## Overview

This repository will stay in sync with your deployed chats on [v0.dev](https://v0.dev).
Any changes you make to your deployed app will be automatically pushed to this repository from [v0.dev](https://v0.dev).

## Deployment

Your project is live at:

**[https://vercel.com/alexander-leanos-projects/v0-attio-clone-project-a0](https://vercel.com/alexander-leanos-projects/v0-attio-clone-project-a0)**

## Build your app

Continue building your app on:

**[https://v0.dev/chat/projects/D4LOmdOGoSu](https://v0.dev/chat/projects/D4LOmdOGoSu)**

## How It Works

1. Create and modify your project using [v0.dev](https://v0.dev)
2. Deploy your chats from the v0 interface
3. Changes are automatically pushed to this repository
4. Vercel deploys the latest version from this repository
```

## File: dkl-microapp-2-main/tailwind.config.ts
```typescript
import type { Config } from "tailwindcss"

const config: Config = {
  darkMode: ["class"],
  content: [
    "./pages/**/*.{js,ts,jsx,tsx,mdx}",
    "./components/**/*.{js,ts,jsx,tsx,mdx}",
    "./app/**/*.{js,ts,jsx,tsx,mdx}",
    "*.{js,ts,jsx,tsx,mdx}",
  ],
  theme: {
    extend: {
      colors: {
        background: "hsl(var(--background))",
        foreground: "hsl(var(--foreground))",
        card: {
          DEFAULT: "hsl(var(--card))",
          foreground: "hsl(var(--card-foreground))",
        },
        popover: {
          DEFAULT: "hsl(var(--popover))",
          foreground: "hsl(var(--popover-foreground))",
        },
        primary: {
          DEFAULT: "hsl(var(--primary))",
          foreground: "hsl(var(--primary-foreground))",
        },
        secondary: {
          DEFAULT: "hsl(var(--secondary))",
          foreground: "hsl(var(--secondary-foreground))",
        },
        muted: {
          DEFAULT: "hsl(var(--muted))",
          foreground: "hsl(var(--muted-foreground))",
        },
        accent: {
          DEFAULT: "hsl(var(--accent))",
          foreground: "hsl(var(--accent-foreground))",
        },
        destructive: {
          DEFAULT: "hsl(var(--destructive))",
          foreground: "hsl(var(--destructive-foreground))",
        },
        border: "hsl(var(--border))",
        input: "hsl(var(--input))",
        ring: "hsl(var(--ring))",
        chart: {
          "1": "hsl(var(--chart-1))",
          "2": "hsl(var(--chart-2))",
          "3": "hsl(var(--chart-3))",
          "4": "hsl(var(--chart-4))",
          "5": "hsl(var(--chart-5))",
        },
        sidebar: {
          DEFAULT: "hsl(var(--sidebar-background))",
          foreground: "hsl(var(--sidebar-foreground))",
          primary: "hsl(var(--sidebar-primary))",
          "primary-foreground": "hsl(var(--sidebar-primary-foreground))",
          accent: "hsl(var(--sidebar-accent))",
          "accent-foreground": "hsl(var(--sidebar-accent-foreground))",
          border: "hsl(var(--sidebar-border))",
          ring: "hsl(var(--sidebar-ring))",
        },
        blueishGreen: {
          // Ensure this is correctly defined
          DEFAULT: "#14b8a6", // teal-500
          foreground: "#ffffff", // White text on teal-500
          50: "#f0fdfa",
          100: "#ccfbf1",
          200: "#99f6e4",
          300: "#5eead4",
          400: "#2dd4bf",
          500: "#14b8a6",
          600: "#0d9488",
          700: "#0f766e",
          800: "#115e59",
          900: "#134e4a",
          950: "#042f2e",
        },
      },
      borderRadius: {
        lg: "var(--radius)",
        md: "calc(var(--radius) - 2px)",
        sm: "calc(var(--radius) - 4px)",
      },
      keyframes: {
        "accordion-down": {
          from: { height: "0" },
          to: { height: "var(--radix-accordion-content-height)" },
        },
        "accordion-up": {
          from: { height: "var(--radix-accordion-content-height)" },
          to: { height: "0" },
        },
      },
      animation: {
        "accordion-down": "accordion-down 0.2s ease-out",
        "accordion-up": "accordion-up 0.2s ease-out",
      },
    },
  },
  plugins: [require("tailwindcss-animate")],
}
export default config
```

## File: dkl-microapp-2-main/tsconfig.json
```json
{
  "compilerOptions": {
    "lib": ["dom", "dom.iterable", "esnext"],
    "allowJs": true,
    "target": "ES6",
    "skipLibCheck": true,
    "strict": true,
    "noEmit": true,
    "esModuleInterop": true,
    "module": "esnext",
    "moduleResolution": "bundler",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "jsx": "preserve",
    "incremental": true,
    "plugins": [
      {
        "name": "next"
      }
    ],
    "paths": {
      "@/*": ["./*"]
    }
  },
  "include": ["next-env.d.ts", "**/*.ts", "**/*.tsx", ".next/types/**/*.ts"],
  "exclude": ["node_modules"]
}
```
