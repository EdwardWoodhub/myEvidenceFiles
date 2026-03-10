---
title: 速度单位换算全景指南
---

# 速度单位换算全景指南

## 3. 可视化分析

```sql m_s, km_h, mph, knots, mach, scenario
select 
    m_s, 
    km_h, 
    mph, 
    knots, 
    mach,
    scenario 
from speed_things.speed_conversion
order by m_s
```
