
Обратите внимание, что в некоторых случаях в сервисах не определяется `selector` в спецификации. Сервис без `selector` не будет создавать соответствующий объект конечной точки (Endpoint). Таким образом, пользователь может вручную назначить сервис определённым конечным точкам. Использование `type: ExternalName` — это другой вариант использования, когда не нужно определять селектор в сервисе.

