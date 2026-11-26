## @write-requirements نوشتن نیازمندی‌ها <a id="write-the-requirements"></a>

- نیازمندی‌ها (requirements) را بر اساس بخش‌های محصول گروه‌بندی کنید، یک
  فایل برای هر بخش: `pm/<lang>/<quarter>/requirements/<area>.md`، نام بخش
  به انگلیسی و به شکل kebab case
- به هر نیازمندی یک شناسه `req-<area>-<abc>` بدهید: `<abc>` کدی سه‌حرفی با
  حروف کوچک است که نیازمندی را خلاصه می‌کند، مثلاً `req-results-lst` برای
  فهرست نتایج. این کد در بخش خود در همه فصل‌ها یکتاست؛ پیشوند آن را از
  شناسه‌های تصمیم‌ها جدا نگه می‌دارد
- هرگز عدد در شناسه نیازمندی نگذارید: ترتیب نیازمندی‌ها بدون شماره‌گذاری
  دوباره تغییر می‌کند. هرگز یک شناسه را دوباره به کار نبرید یا تغییر نام
  ندهید
- برای ارجاع به چند نیازمندی از یک بخش، اولین شناسه کامل و کد بقیه را
  بنویسید: `req-results-lst, imp, exp`
- هر نیازمندی را در بخش (section) جداگانه بنویسید:

```markdown
## req-results-lst: Result list right after the race

- Status: accepted
- Priority: must
- Statement: The result list is ready two seconds after the last finisher
- Why: [results without desktop software](../goals/results-without-desktop-software.md),
  topic `timing`
- Acceptance: a race with 500 finishers shows the list within two seconds
```

- `Status` — `proposed`، `accepted`، `done` یا `dropped`
- `Priority` — `must`، `should` یا `could`؛ آنچه اصلاً خواسته نمی‌شود
  `dropped` است
- `Statement` — یک جمله درباره اینکه محصول چه باید بکند یا چه باید باشد،
  هرگز چگونه
- `Why` — هدفی که به آن خدمت می‌کند و موضوعی که از آن می‌آید
- `Acceptance` — بررسی‌هایی که آن را اثبات می‌کنند؛ در صورت نیاز برای هر
  بررسی یک بند
- نیازمندی را در همان‌جا تغییر دهید و بنویسید چه چیزی و چه زمانی تغییر
  کرد؛ نیازمندی‌ای که جایگزین می‌شود `dropped` می‌شود و به جانشین خود
  پیوند می‌دهد
- یک نیازمندی `done` که خراب شده یک باگ است، نه یک نیازمندی جدید
