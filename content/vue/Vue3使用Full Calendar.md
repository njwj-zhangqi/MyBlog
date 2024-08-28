```bash
pnpm install @fullcalendar/vue3 @fullcalendar/core @fullcalendar/daygrid @fullcalendar/timegrid @fullcalendar/interaction

```

本地化
```js
import zhCnLocale from "@fullcalendar/core/locales/zh-cn";

export default defineComponent({
components: {
  FullCalendar,
},
setup() {
  const calendarOptions = ref({
	plugins: [dayGridPlugin, timeGridPlugin, interactionPlugin],
	locale: zhCnLocale,
	initialView: "dayGridMonth",
	headerToolbar: {
	  left: "prev,next today",
	  center: "title",
	  right: "dayGridMonth,timeGridWeek,timeGridDay",
	},
	events: [
	  // 示例事件数据
	  { title: "会议", start: "2024-08-29", end: "2024-08-29" },
	],
	// 更多配置...
  });

  return {
	calendarOptions,
  };
},
});
```