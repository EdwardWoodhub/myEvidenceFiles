---
title: 速度单位换算
---

# 速度单位换算Table

---

```sql speeds
-- 这里把所有转换后的数值都统一命名为 val
with unpivoted as (
    select m_s, km_h as val, 'km/h' as unit, scenario 
    from speed_things.speed_conversion
    union all
    select m_s, mph as val, 'mph' as unit, scenario 
    from speed_things.speed_conversion
    union all
    select m_s, knots as val, 'knots' as unit, scenario 
    from speed_things.speed_conversion
)
select * from unpivoted 
order by unit, m_s
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

<ScatterPlot
    data={speeds}
    x="m_s"
    y="val" 
    series="unit"
    xLog={true}
    yLog={true}
    xMin={1}
    connected={true}
    markers={true}
    tooltipTitle="scenario"
/>
