# Контракт API — команда 3

GET https://domrf-ai-training-2026.github.io/team-3-dashboard/data.json

Все данные вымышлены. Публичный read-only JSON, без ключа. CORS не требуется между проектами одной организации, поскольку их origin одинаков: https://domrf-ai-training-2026.github.io. Для форков на другом origin проверьте CORS в браузере. Не используйте режим no-cors: он не даёт читать JSON.

## Общий формат

schema_version: строка 1.0; team_id: число 3; synthetic: true; updated_at: ISO UTC; units: единицы; records: массив записей. Ключ строки: period + office_id.

- period — Неделя до
- office_id — Код офиса
- office — Офис
- city — Город
- clients — Клиенты (чел.)
- repeat_visits — Повторные визиты (чел.)
- wait_minutes_total — Ожидание, сумма мин. (мин.)
- responses — Ответы на опрос (шт.)
- rating_sum — Сумма оценок (баллы)

Доля повторных = repeat_visits / clients. Среднее ожидание = wait_minutes_total / clients. Оценка = rating_sum / responses; не среднее средних офисов.

## Пример чтения

```js
const response = await fetch(API_URL, {cache: 'no-store'});
if (!response.ok) throw new Error('HTTP ' + response.status);
const payload = await response.json();
if (payload.schema_version !== '1.0' || !Array.isArray(payload.records))
  throw new Error('Неверный формат API');
```

Держите видимыми источник, updated_at и время успешного чтения. При ошибке не подменяйте результат нулями и не оставляйте старые цифры без отметки. Публикация коммита и распространение кэша Pages занимают время; проверяйте успешный deploy и updated_at.

## Принимаемый источник

Команда 4: https://domrf-ai-training-2026.github.io/team-4-dashboard/data.json

Добавьте число менеджеров из API команды 4 и вычислите клиентов на сотрудника за выбранный период.
