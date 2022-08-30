# Vasco Backend Challenge

Welcome to Vasco's backend challenge.

## Instructions

First, clone this repo (do **not** fork it).

```zsh
git clone https://github.com/vascohq/jobs
cd backend
```

Then install all required dependencies:

```zsh
yarn install
```

For each level, write code that makes the `level.test.ts` pass. **Solve the levels in ascending order!**

```zsh
yarn workspace level1 test
```

When you are done, see how to submit your challenge [here](../README.md#sending-your-results).

## Context

You are tasks to implement a few [tRPC](https://trpc.io/) procedures around Vasco's business requirements, although simplified. The API will be consumed in a revenue forecast UI similar to a Google Sheet.

The challenge is separated in levels and they become more complex over time, so you will probably have to re-use some code and adapt it to the new requirements. A good way to solve this is by writing [Clean Code](https://gist.github.com/wojteklu/73c6914cc446146b8b533c0988cf8d29), adding new layers of abstraction when they become necessary and possibly write tests so you don't break what you have already done.

Don't hesitate to write shameless code at first, and then refactor it in the next levels.

For higher levels we are interested in seeing code that is clean, extensible and robust, so don't overlook edge cases, use exceptions where needed.

## Levels

### 1. Stats per month

```json
// GET /trpc/targets.perMonth
// Input: { month: 1, year: 2022 }
{
  "recurringRevenue": 105000.00,
  "churnRate": 0.1,
  "downgradeRate": 0.1,
  "upgradeRate": 0.1
}
```

### 2. Stats per quarter

```json
// GET /trpc/targets.perQuarter
// Input: { quarter: 1, year: 2022 }
{
  "recurringRevenue": 120000.00,
  "churnRate": 0.1,
  "downgradeRate": 0.1,
  "upgradeRate": 0.1
}
```

### 3. Targets per teams

```diff
// GET /trpc/targets.perMonth
// GET /trpc/targets.perQuarter
{
  "recurringRevenue": 5000.00,
  "churnRate": 0.01,
  "downgradeRate": 0.03,
  "upgradeRate": 0.02,
+ "acquisitionTarget": 5000.00,
+ "expansionTarget": 2000.00
}
```

Formula for acquisition target:

```
netRetentionRate =  1 - downgradeRate + upgradeRate - churnRate
acquisitionTarget = recurringRevenue(t-1) * (1 - netRetentionRate)
expansionTarget = 
```