<script lang="ts">
  import BarChart from "../../../components/charts/bar-chart-2.svelte";
  import { getWidgetColor } from "../dashboard-helpers";
  import type { Widget } from "../../../modules/dashboard/widget";

  export let widget: Widget;
</script>

<style>
  .chart-value {
    height: 100%;
    flex-grow: 1;
    flex-shrink: 0;
    display: flex;
    width: 100%;
    display: column;
    justify-content: stretch;
  }
</style>

{#if widget}
  <div class="chart-value">
    <BarChart
      height={100}
      showSelected={false}
      type={widget.type == 'linechart' ? 'line' : 'bar'}
      color={getWidgetColor(widget)}
      labels={widget.stats.chart.values.map((point) => point.x)}
      points={widget.stats.chart.values}
      hideXTicks={widget.size == 'sm'}
      hideYTicks={widget.size == 'sm'}
      ignoreZero={widget.element.obj ? widget.element.obj.ignore_zeros : false}
      yFormat={(y) => {
        if (widget.element.type == 'tracker') {
          return widget.element.obj.displayValue(y);
        } else {
          return y;
        }
      }} />
  </div>
{/if}
