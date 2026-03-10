---
title: 速度单位换算
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
-- 通过 UNION 把宽表转成长表，这是让散点图画出多条线的唯一方法
with long_data as (
    select m_s, km_h as val, 'km/h' as unit, scenario from speed_things.speed_conversion
    union all
    select m_s, mph as val, 'mph' as unit, scenario from speed_things.speed_conversion
    union all
    select m_s, knots as val, 'knots' as unit, scenario from speed_things.speed_conversion
)
select * from long_data order by m_s
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
