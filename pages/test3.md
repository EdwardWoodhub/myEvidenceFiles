# 速度单位换算全景图

```sql speeds
select m_s, km_h, mph, knots from speed_things.speed_conversion where m_s > 0
```

<LogLogChart 
    data={speeds} 
    x="m_s" 
    y={['km_h', 'mph', 'knots']} 
    title="速度单位换算全景（双对数坐标）"
    xLabel="单位: m/s"
/>
