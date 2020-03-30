---
title: Requirements 
---

```text
interface Requirement{
  name: String!
}

type Any implements Requirement {name: String!} 
type Latest implements Requirement {name: String!}

type GT implements Requirement{
  name: String!
  version: String!
}

type GTE implements Requirement{
  name: String!
  version: String!
}

type LT implements Requirement{
  name: String!
  version: String!
}

type LTE implements Requirement{
  name: String!
  version: String!
}
```
