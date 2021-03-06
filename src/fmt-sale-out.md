Допустимые значения для параметра Morion-Skynet-Tag в заголовке HTTP запроса:

```
	data.sale-out.monthly.ua // Данные за месяц из Украины
	data.sale-out.monthly.kz // Данные за месяц из Казахстана
	data.sale-out.weekly.ua  // Данные за неделю из Украины
	data.sale-out.daily.ua   // Данные за день из Украины
	data.sale-out.daily.kz   // Данные за день из Казахстана
	data.sale-out.daily.by   // Данные за день из Беларуси
```

Пример:

```
	Morion-Skynet-Tag: data.sale-out.monthly.ua
```

Формат приема-передачи данных:

```
{
	"meta": {
		// Данные формируются источником данных
		"id": "string",   // Идентификатор торговой точки (внешний код)
		"name": "string", // Название торговой точки
		"head": "string", // Название торговой сети (юр. лица)
		"addr": "string", // Адрес торговой точки
		"edrp": "string", // ЕДРПОУ (ОКПО)
		"time": "string", // Время отправки данных строкой ISO 8601 (RFC3339) 2015-02-17T01:15:25+02:00
		"time_range": ["", ""], // Временной диапазон строкой ISO 8601 (RFC3339) 2015-02-17T01:15:25+02:00

		// Добавляется сервером распознавания (если связь установлена)
		"rel_id": "string",  // ID_ADDRESS
		"rel_sha": "string", // SHA1(len1024("name/head: addr"))

		// Объект добавляется сервисом распознавания (всегда)
		"sky_key": "string",  // Ключ исходного отправителя
		"sky_tag": "string",  // Значение Morion-Skynet-Tag
		"sky_sha": "string",  // SHA1(data[{},...])
		"sky_time": "string", // Время приема данных строкой ISO 8601 (RFC3339) 2015-02-17T01:15:25+02:00

		// Добавляется сервисом проверки данных (всегда)
		"chk_code": 0,          // Код статуса результата проверки (int)
		"chk_time": "string",   // Время проверки данных строкой ISO 8601 (RFC3339) 2015-02-17T01:15:25+02:00
		"chk_qty_all": 0,       // Количество строк (товарных позиций всего) (int)
		"chk_qty_rel": 0,       // Количество связей (распознанных товаров) (int)
		"chk_qty_nil": 0,       // Количество пустых (нераспознанных товаров) (int)
		"chk_qty_err": 0,       // Количество ошибок при проверке позиций (int)
		"chk_pct_err": 0.0,     // Процент ошибок в связанных товарах (float)
		"chk_pct_err_max": 0.0, // Процент ошибок в связанных товарах максимально допустимый (float)
		"chk_pct_nil": 0.0,     // Процент нераспознанных товаров (float)
		"chk_pct_nil_max": 0.0  // Процент нераспознанных товаров максимально допустимый (float)
	},
	"data": [{
		// Данные формируются источником данных
		"id": "string",   // Идентификатор товара в торговой точке (внешний код)
		"name": "string", // Товар, полное наименование препарата + производитель (через пробел)
		"quant": 0.0,     // Количество расхода (float)
		"price": 0.0,     // Цена расхода (float)
		"balance": 0.0,   // Остаток на конец периода (float)
		"reimbur": 0,     // Возмещение 0 или 1 (int) тольео для sale-out

		"q_inp": 0.0,     // Количество прихода (float)
		"p_inp": 0.0,     // Цена прихода (float)

		// Добавляется сервером распознавания (если связь установлена)
		"rel_id": "string",    // ID_DRUG
		"rel_id_s": "string",  // ID_ADDRESS
		"rel_sha": "string",   // SHA1(name)
		"rel_sha_s": "string", // SHA1(supp)

		// Добавляется сервисом проверки данных (если облом)
		"err_code": 0,      // Код статуса результата проверки (int)
		"err_coef": 0.0,    // Коэффициент (множитель) эксперта
		"err_prc_fix": 0.0, // Цена фиксированная экспертом ("пропускная")
		"err_prc_avg": 0.0, // Цена усредненная за прошлый период
		"err_qty_min": 0.0, // Количество минимальное
		"err_qty_max": 0.0  // Количество максимальное
	}]
}
```