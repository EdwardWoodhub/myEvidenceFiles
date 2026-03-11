---
title: 调用官方LineCharts之效果展示
---

# 速度单位换算Table

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
