---
title: 速度单位换算
---

# 速度单位换算Table

---

```sql speeds_long
with base as (
    -- 强制转换为双精度浮点数，并统一列名
    select cast(m_s as double) as x_val, cast(km_h as double) as y_val, 'km/h' as unit, scenario from speed_things.speed_conversion
    union all
    select cast(m_s as double) as x_val, cast(mph as double) as y_val, 'mph' as unit, scenario from speed_things.speed_conversion
    union all
    select cast(m_s as double) as x_val, cast(knots as double) as y_val, 'knots' as unit, scenario from speed_things.speed_conversion
)
-- 必须排除 0，且必须全局排序
select * from base 
where x_val > 0 
order by x_val
```

<LineChart
    data={speeds_long}
    x=x_val
    y=y_val
    series=unit
    xLog={true}         
    yLog={true}
    xType=quantitative  xMin=1              yMin=1              markers={true}
    tooltipTitle="scenario"
/>

<ScatterPlot
    data={speeds_long}
    x=x_val
    y=y_val
    series=unit
    xLog={true}
    yLog={true}
    xMin=1
    yMin=1
    connected={true}
    markers={true}
    tooltipTitle="scenario"
/>
