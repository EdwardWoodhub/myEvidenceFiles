<script>
    import { ECharts } from '@evidence-dev/core-components';

    // 1. 定义接口属性 (Props)
    export let data;
    export let x;              // X轴列名 (例如 "m_s")
    export let y = [];         // Y轴列名数组 (例如 ["km_h", "mph"])
    export let title = "";     // 图表标题
    export let xLabel = "";    // X轴标签 (留空则使用 x 列名)
    export let yLabel = "";    // Y轴标签
    export let showLegend = true;

    // 2. 数据预处理：Log轴不能处理 <= 0 的值，这里做自动过滤
    $: cleanData = data ? data.filter(d => d[x] > 0) : [];

    // 3. 动态配置 ECharts
    $: config = {
        title: { 
            text: title, 
            left: 'center',
            textStyle: { fontWeight: 'normal', fontSize: 16 }
        },
        tooltip: { 
            trigger: 'axis',
            confine: true, // 解决小屏幕下 tooltip 溢出问题
            backgroundColor: 'rgba(255, 255, 255, 0.9)'
        },
        legend: { 
            show: showLegend, 
            top: '10%',
            icon: 'circle'
        },
        grid: { 
            top: '22%', 
            bottom: '15%', 
            left: '10%',
            right: '10%',
            containLabel: true 
        },
        xAxis: {
            type: 'log',
            name: xLabel || x,
            nameLocation: 'middle',
            nameGap: 30,
            minorTick: { show: true }, // 对数轴的细分刻度是灵魂
            splitLine: { 
                show: true, 
                lineStyle: { type: 'dashed', color: '#e0e0e0' } 
            }
        },
        yAxis: {
            type: 'log',
            name: yLabel,
            minorTick: { show: true },
            splitLine: { 
                show: true, 
                lineStyle: { type: 'dashed', color: '#e0e0e0' } 
            }
        },
        series: (Array.isArray(y) ? y : [y]).map(col => ({
            name: col,
            type: 'line',
            // 自动映射坐标对 [x, y]
            data: cleanData.map(d => [Number(d[x]), Number(d[col])]),
            symbolSize: 8,
            emphasis: { focus: 'series' } // 鼠标悬停时高亮该线条
        }))
    };
</script>

<div class="chart-container">
    {#if cleanData.length > 0}
        <ECharts {config} />
    {:else}
        <div class="empty-state">
            <p>LogLogChart: 等待数据中或数据不包含正数...</p>
        </div>
    {/if}
</div>

<style>
    .chart-container {
        width: 100%;
        margin: 20px 0;
    }
    .empty-state {
        height: 300px;
        display: flex;
        align-items: center;
        justify-content: center;
        border: 1px dashed #ccc;
        color: #666;
        font-family: sans-serif;
    }
</style>
