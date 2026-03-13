---
title: 调用官方LineCharts之效果展示
---

# 速度单位换算Table

| 典型场景 | 米/秒 (m/s) | 千米/小时 (km/h) | 英里/小时 (mph) | 节 (kn) | 马赫 (Ma) |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **正常步行** | 1.39 | 5.0 | 3.1 | 2.7 | 0.004 |
| **百米冲刺** | 10.0 | 36.0 | 22.4 | 19.4 | 0.029 |
| **大型船舶** | 10.29 | 37.04 | 23.0 | 20.0 | 0.03 |
| **美国公路限速** | 26.8 | 96.6 | 60.0 | 52.1 | 0.079 |
| **中国公路限速** | 27.8 | 100.0 | 62.1 | 54.0 | 0.082 |
| **高铁巡航** | 83.3 | 300.0 | 186.4 | 162.0 | 0.245 |
| **民航客机** | 289.2 | 1041.0 | 647.0 | 562.0 | 0.85 |
| **音障** | 340.3 | 1225.0 | 761.2 | 661.5 | 1.0 |
| **步枪子弹** | 1000.0 | 3600.0 | 2237.0 | 1944.0 | 2.94 |
| **高超音速门槛** | 1701.5 | 6125.0 | 3806.0 | 3307.0 | 5.0 |
| **航天器再入** | 8507.5 | 30625.0 | 19031.0 | 16537.0 | 25.0 |

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


<LineChart
    data={speeds}
    x="m_s"
    y={['km_h', 'mph', 'knots']}
    xType=quantitative
    xLog={true}
    yLog={true}
    xMin=1
    markers={true}
    tooltipTitle="scenario"
/>

---

```sql speeds_log
with base as (
    -- 手动计算 Log10。这样 X 轴的 1 代表 10^1=10, 2 代表 10^2=100
    select 
        log10(m_s) as log_x, 
        log10(km_h) as log_kmh, 
        log10(mph) as log_mph, 
        log10(knots) as log_knots,
        scenario 
    from speed_things.speed_conversion
    where m_s > 0
)
select * from base order by log_x
```

<LineChart
data={speeds_log}
x=log_x
y={['log_kmh', 'log_mph', 'log_knots']}
xLabel="速度 (log10 m/s)"
yLabel="转换值 (log10)"
markers={true}
tooltipTitle="scenario"
/>


