---
title: 速度单位换算
---

# 速度单位换算全景指南

| 场景描述 | m/s | km/h | mph | kn |
| :--- | :--- | :--- | :--- | :--- |
| **正常步行** | 1.39 | 5.0 | 3.1 | 2.7 |
| **高铁巡航** | 83.3 | 300.0 | 186.4 | 162.0 |
| **音障参考** | 340.3 | 1225.0 | 761.2 | 661.5 |
| **航天器再入** | 8507.5 | 30625.0 | 19031.0 | 16537.0 |

---

```sql speeds
-- 注意：FROM 后面必须对应文件夹名和文件名
select m_s, km_h, mph, knots, scenario 
from speed_things.speed_conversion
order by m_s
```

<LineChart
data={speeds}
x="m_s"
y={['km_h', 'mph', 'knots']}
markers={true}
tooltipTitle="scenario"
/>


<LineChart
    data={speeds}
    x="m_s"
    y={['km_h', 'mph', 'knots']}
    xLog={true}
    yLog={true}
    markers={true}
    tooltipTitle="scenario"
/>
