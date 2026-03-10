---
title: 速度单位换算
---

# 速度单位换算Table

---

```sql speeds
select 
    cast(m_s as double) as x, 
    cast(km_h as double) as y_kmh, 
    cast(mph as double) as y_mph, 
    cast(knots as double) as y_knots,
    scenario 
from speed_things.speed_conversion 
where m_s > 0 
order by m_s
```

<ECharts config={
    {
        tooltip: { trigger: 'axis' },
        legend: { data: ['km/h', 'mph', 'knots'] },
        grid: { bottom: '10%', containLabel: true },
        xAxis: {
            type: 'log',
            name: 'm/s',
            nameLocation: 'middle',
            nameGap: 25,
            minorTick: { show: true },
            splitLine: { show: true }
        },
        yAxis: {
            type: 'log',
            minorTick: { show: true },
            splitLine: { show: true }
        },
        series: [
            {
                name: 'km/h',
                type: 'line',
                data: speeds.map(d => [d.x, d.y_kmh]),
                symbolSize: 8
            },
            {
                name: 'mph',
                type: 'line',
                data: speeds.map(d => [d.x, d.y_mph]),
                symbolSize: 8
            },
            {
                name: 'knots',
                type: 'line',
                data: speeds.map(d => [d.x, d.y_knots]),
                symbolSize: 8
            }
        ]
    }
}/>
