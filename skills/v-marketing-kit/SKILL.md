---
name: v-marketing-kit
description: |-
  V-Kit (Marketing Kit): реклама, аналитика и подписки через коннектор V-Kit — расход, показы, клики, установки, события, кампании, конверсии, MRR, подписки, выручка, отзывы App Store. Применяй, когда речь о маркетинговых цифрах, даже если источник не назван («сколько потратили», «сколько установок», «что с кампанией», «установки в App Store», «продажи App Store Connect», «отзывы», «воронка App Store»). Работает через коннектор V-Kit (marketing-kit.app); инструменты: mk_meta (Meta Ads), mk_fb_pages (Facebook Pages), mk_instagram (Instagram), mk_tiktok (TikTok Ads), mk_google_ads (Google Ads), mk_ga4 (GA4), mk_search_console (Search Console), mk_appsflyer (AppsFlyer), mk_appsflyer_write (правки OneLink), mk_revenuecat (RevenueCat), mk_app_store_connect (App Store Connect, свои приложения), mk_app_store_connect_write (включение Analytics Reports), mk_apple (App Store, публичные данные); начинай с mk_status.
metadata:
  version: "1.13.4"
  title: V-Kit
---

# V-Kit (Marketing Kit)

Реклама, аналитика и подписки через коннектор V-Kit (сервер marketing-kit.app):
одиннадцать источников, по инструменту на каждый, `mk_appsflyer_write` для правок
OneLink, `mk_app_store_connect_write` для включения Analytics Reports и `mk_status` для проверки подключений. Источник
выбирай по имени инструмента — не ищи обход через соседний.

| Инструмент | Для чего |
|---|---|
| `mk_meta` | Meta Ads (платная реклама в Facebook и Instagram): расход, показы, клики, установки по данным Meta, кампании/адсеты/объявления, счётчики событий, кастомные конверсии |
| `mk_fb_pages` | Facebook Pages: органика страниц — охват, посты, вовлечённость, подписчики |
| `mk_instagram` | Instagram: органика профессионального аккаунта — охват, просмотры, подписчики, посты и reels |
| `mk_tiktok` | TikTok Ads: рекламный расход, показы, клики, конверсии; кампании, группы, объявления |
| `mk_google_ads` | Google Ads: отчёты GAQL и справочники кампаний, групп, объявлений, конверсионных действий |
| `mk_ga4` | Google Analytics 4: события и поведение пользователей, воронки, пользователи и сессии, realtime, метаданные |
| `mk_search_console` | Google Search Console: органический поиск Google — запросы, страницы, клики, показы, CTR, позиция; sitemaps; индексирование URL |
| `mk_appsflyer` | AppsFlyer: установки и in-app события по источникам, сводные и сырые отчёты, дубли покупок приложение ↔ RevenueCat (`purchase_dedup`), OneLink |
| `mk_appsflyer_write` | AppsFlyer: изменение OneLink-ссылок и копия настроек интеграции (только после явного «да» пользователя) |
| `mk_revenuecat` | RevenueCat: подписки — MRR, ARR, активные подписки и триалы, выручка, отток, конверсия триала, LTV, возвраты, продукты и offerings, подписка одного клиента |
| `mk_app_store_connect` | App Store Connect: официальные данные Apple по своим приложениям — загрузки, повторные загрузки и обновления, выручка (proceeds), отчёты по подпискам и их события, воронка App Store (показы → просмотры страницы → загрузки), сессии, краши, отзывы с ответами, версии, эксперименты PPO; задержка D+1 |
| `mk_app_store_connect_write` | App Store Connect: включение Analytics Reports (`analytics_enable`; только после явного «да» пользователя) |
| `mk_apple` | App Store (публичные данные любого приложения, без ключа): версия и дата релиза, рейтинг, отзывы, позиции в топах по странам |
| `mk_status` | Статус сервера: версии, кто вошёл, какие источники авторизованы, состояние API |

Каждый инструмент принимает `{ mode, args }`: `mode` — режим источника,
`args` — его аргументы (режимы и аргументы — в разделах ниже).

## Общие правила — от сервера

Общие правила поведения (начинать с `mk_status`, не вызывать неавторизованный
источник, не выдумывать цифры, какой инструмент когда брать, период и часовой пояс,
большие ответы ссылками, запись только после плана и «да», `api.state`, ошибки 424
как есть, ключи не в чате) приходят от сервера коннектора в `instructions` при
подключении и меняются выкаткой сервера, без обновления плагина. Этот файл —
справочник по источникам: режимы, поля, нюансы. Если правил от сервера у тебя нет,
действуй осторожно: сначала `mk_status`, цифры не выдумывай, ключи в чат не проси,
записывай только после явного «да».

## Какой источник брать

- **Meta Ads** (`mk_meta`) — платная реклама в Facebook и Instagram: расход,
  CPI, кампании, адсеты, объявления.
- **Facebook Pages** (`mk_fb_pages`) — органика страницы: охват, посты,
  вовлечённость, подписчики.
- **Instagram** (`mk_instagram`) — органика профессионального аккаунта:
  охват, просмотры, подписчики, посты и reels.
- **TikTok Ads** (`mk_tiktok`) — рекламный расход, показы, клики и
  конверсии в TikTok. Органического TikTok (видео, подписчики) пока нет —
  скажи об этом, не подменяй его рекламой.
- **Search Console** (`mk_search_console`) — органический поиск Google до
  клика: по каким запросам находят сайт, клики и показы в выдаче, CTR,
  средняя позиция, страницы из поиска, индексирование и sitemap.
- **RevenueCat** (`mk_revenuecat`) — деньги подписок приложения: MRR, ARR,
  активные подписки и триалы, выручка (gross / proceeds), конверсия триала,
  отток, возвраты, LTV, когорты, что с подпиской конкретного пользователя.
- **App Store Connect** (`mk_app_store_connect`) — официальные цифры Apple по
  **своим** приложениям пользователя: загрузки, повторные загрузки и обновления
  по странам и устройствам, выручка (proceeds), отчёты Apple по подпискам и их
  события, воронка магазина (показы → просмотры страницы → загрузки), сессии,
  краши, отзывы с ответами, версии, настройка Product Page Optimization.
  Задержка D+1; Apple считает дни по тихоокеанскому времени.
- **Apple, публичное** (`mk_apple`) — публичные данные **любого** приложения без
  ключа: рейтинг, текущая версия, топы категорий, публичные отзывы, в том числе
  у конкурентов.
- **Google Ads, GA4, AppsFlyer** — как раньше: `mk_google_ads` (реклама
  Google), `mk_ga4` (поведение в приложении и на сайте), `mk_appsflyer`
  (атрибуция: установки и события по медиа-источникам и кампаниям,
  неорганика против органики).

Тонкости выбора, которые не сводятся к имени инструмента: «реклама в инстаграме» —
`mk_meta` (разбивка `publisher_platform`), охват аккаунта — `mk_instagram`; «трафик из
поиска» — `mk_search_console` до клика, `mk_ga4` после. `mk_fb_pages` и `mk_instagram`
работают через подключение Meta, `mk_search_console` — через подключение Google: у
старого подключения в ответе `reauthorize: true` / `missing_scopes` — нажать
«Authorize» у этого провайдера ещё раз на https://marketing-kit.app/connections;
остальные источники провайдера продолжат работать.

## Начало сессии: `mk_status`

В начале сессии, один раз, вызови `mk_status`.

- **Версии.** Сверь `server.version` с версией этого скила (`1.13.4`).
  Сервер новее — скажи одной строкой, что плагин V-Kit обновится сам
  (скил подтягивается вместе с плагином), и работай дальше, не переспрашивай.
- **Первый шаг.** Если в ответе `mk_status` есть `next_step` — скажи пользователю эту
  фразу со ссылкой раньше всего остального.
- **Источники.** `authorized: false` у нужного источника — правила сервера: не вызывай его
  режимы, отправь на https://marketing-kit.app/connections (Google — GA4, Google Ads,
  Search Console; Meta — реклама, Pages, Instagram; TikTok; ключи AppsFlyer,
  RevenueCat, App Store Connect), `note` источника скажи как есть.
- **Нет инструментов `mk_*` в этом чате** (коннектор не подключён или выключен) —
  вызвать нечего, поэтому не ищи обходных путей и не предлагай другие сервисы
  (Supermetrics и т. п.) первым делом. Дай пользователю шаги дословно, по порядку,
  со ссылками:
  1. В чате: **+** (plus) → **Connectors** → **v-marketing-kit** (добавленный до октября 2026 —
     **Marketing Kit**) → **Connect**.
  2. v-marketing-kit там нет: https://claude.ai/customize/connectors → вкладка **Yours** →
     **v-marketing-kit** → **Connect**. Нет и там: **Add custom connector** → Name
     `v-marketing-kit`, URL `https://marketing-kit.app/mcp`, поля OAuth пустые → **Add** → **Connect**.
  3. Плагин: https://claude.ai/customize/plugins/yours → **v-marketing-kit** → вкладка
     **Connectors** → **Connect**. После «Add marketplace» claude.ai показывает **Discover**:
     switch to **Yours** or type “marketing” in the search box (плагин — **v-marketing-kit**). Шаги установки плагина —
     https://marketing-kit.app/install#plugin.
  4. После **Connect**: вход через Google или Meta → **Allow** → открыть **новый чат**.
     Затем источники — на https://marketing-kit.app/connections. Тот же аккаунт работает в
     приложении Claude на компьютере и на телефоне.
  Цифры без инструментов не выдумывай. Запасной вариант — одной строкой в конце и только
  если пользователь сам спросит (например, другой подключённый сервис).
- **Инструменты `mk_*` дважды** (старый плагин или скил Marketing Kit — `marketing-kit` —
  рядом с V-Kit) — скажи удалить старое: https://marketing-kit.app/install#migrate.
- **Вход.** Войти в V-Kit нужно один раз — через коннектор (Connect)
  в Claude (подключение — путь выше): откроется страница marketing-kit.app, вход через Google или Meta.
  Ответ «нужно войти» или `source_not_authorized` — отправь пользователя на
  https://marketing-kit.app/connections. Никогда не проси токен, пароль или код
  в чате.

## Версии API источников (`api`)

Что сказать пользователю при `api.state` не `ok` — в правилах сервера. Для
`api.breaking: unknown` сделай один узкий контрольный запрос, сверь результат с
известным числом из `references/` источника и реши как `yes` или `no`; скажи, что
решил.

## Отказы сервера

Это ответы, а не поломки — прочитай `message` и действуй:

- `source_not_authorized` — источник не подключён или доступ сброшен:
  отправь пользователя на https://marketing-kit.app/connections. Если в
  ответе `reauthorize: true` / `missing_scopes` — провайдера (Meta или
  Google — назван в `message`) нужно авторизовать заново («Authorize» на той
  же странице), остальные его источники при этом работают.
- `source_not_configured` — сервер не настроен владельцем для этого
  источника (нет ключей приложения): скажи об этом, не пытайся обойти.
- `appsflyer_token_missing` — не сохранён токен AppsFlyer: см. раздел про
  ключи ниже.
- `app_store_connect_key_missing` — не сохранён ключ App Store Connect (и
  `app_store_connect_vendor_number_missing` — номер поставщика): см. раздел про
  ключи ниже.
- `revenuecat_key_missing` — не сохранён ключ RevenueCat: см. раздел про ключи
  ниже.
- `invalid_args` — исправь аргументы по `message` и `mode=fields`, один раз.
- `source_error` — источник отказал; скажи `message` и `explanation` как
  есть, не подменяй цифры. `code: "SERVICE_DISABLED"` у GA4, Google Ads или
  Search Console — API не включён в проекте Google Cloud сервиса: в `message`
  название API и ссылка на включение для владельца; это настройка владельца,
  не пользователя, переподключение не поможет.
- `proxy_error` — ответ сервера не дошёл (страница сети перед сервером вместо
  ответа): повтори запрос через минуту, при повторе — `mk_status`.

**Пошаговые инструкции** по каждому источнику — на сайте, ссылкой прямо на
окно инструкции: `https://marketing-kit.app/connections#<источник>` —
`ga4`, `google_ads`, `search_console`, `meta`, `fb_pages`, `instagram`,
`tiktok`, `appsflyer`, `revenuecat`, `app_store_connect`, `apple`. Когда пользователь не знает, как
подключить источник или что значит ошибка, дай эту ссылку.

## Ключи: AppsFlyer, RevenueCat, App Store Connect, Google Ads

Пользователь сохраняет их сам на странице https://marketing-kit.app/connections
(сервер хранит их зашифрованными):

- **AppsFlyer** — API token V2 из AppsFlyer → Security center → API tokens
  (для чтения); для `mk_appsflyer_write` ещё отдельный токен OneLink API.
  Инструкция: https://marketing-kit.app/connections#appsflyer.
- **RevenueCat** — secret API key **V2** с правами только на чтение
  (RevenueCat → Project settings → API keys → + New secret API key, версия V2,
  Charts & Metrics / Customer Information / Project Configuration — Read).
  Ключи v1 и публичные ключи SDK не подходят. Инструкция:
  https://marketing-kit.app/connections#revenuecat.
- **App Store Connect** — командный (team) ключ: Issuer ID, Key ID и файл
  `.p8` (App Store Connect → Users and Access → Integrations → Team Keys) и
  vendor number для продаж и подписок. Сохраняется только на
  https://marketing-kit.app/connections#app-store-connect, файл `.p8` в чат не
  присылают. Роль Admin покрывает всё; для чтения хватает Sales and Reports или
  Finance (продажи, подписки, аналитика) и App Manager (приложения, отзывы,
  версии); включение аналитики — только Admin.
- **Google Ads** — ничего вписывать не нужно: менеджерский аккаунт (MCC) сервер
  определяет сам. Login customer ID на https://marketing-kit.app/connections#google_ads
  (раздел Advanced) — только если кабинет виден через несколько MCC и нужен конкретный.

Не проси токен или ключ в чате: ответ `appsflyer_token_missing` /
`revenuecat_key_missing`, `app_store_connect_key_missing` или `authorized: false` у `appsflyer` / `revenuecat` / `app_store_connect` в
`mk_status` — скажи, где его взять и куда сохранить (дай ссылку на инструкцию), и
жди, пока пользователь сделает это сам.

## Режимы и аргументы по источникам

Аргументы режима — в `args`; обязательные помечены `*`. Свериться с самим
инструментом можно через `mode=fields`.

### `mk_meta` — Meta: режимы

- `fields` — fields and argument schemas of the modes. Аргументы: без аргументов
- `accounts` — the source's available accounts. Аргументы: без аргументов
- `insights` — performance report (spend, impressions, clicks, actions...), level/breakdowns/attribution windows, synchronous or as an async report. Аргументы: period*, level, fields, breakdowns, action_attribution_windows, act_id, force_async, limit, after
- `objects` — campaigns/adsets/ads — status, objective, budgets (in minor units), targeting. Аргументы: level, act_id, effective_status, limit, after
- `events` — event counts for a period with no source breakdown — actions from insights + pixel stats. Аргументы: period*, act_id, pixel_id
- `conversions` — custom conversions of the ad account (cached, not fetched on every report). Аргументы: act_id

### `mk_fb_pages` — Facebook Pages: режимы

- `fields` — reference of live page and post metrics and the deprecated ones to avoid. Аргументы: без аргументов
- `accounts` — Facebook Pages the user manages — id, name, category, followers, tasks (page tokens are never returned). Аргументы: без аргументов
- `page_insights` — page metrics per day for a period (reach, content views, engagements, followers); periods over 90 days are split. Аргументы: period*, page_id*, metrics, metric_period
- `posts` — published posts of a page for a period with reaction, comment and share counts. Аргументы: period*, page_id*, limit
- `post_insights` — insights for 1–25 posts of a page (reach, content views, clicks, reactions by type). Аргументы: page_id*, post_ids*, metrics

### `mk_instagram` — Instagram: режимы

- `fields` — reference of live account and media metrics and the deprecated ones to avoid. Аргументы: без аргументов
- `accounts` — Instagram professional accounts linked to the user's Facebook Pages — username, followers, media count. Аргументы: без аргументов
- `account_insights` — account metrics for a period (reach, views, engaged accounts, interactions, follows); windows of up to 30 days, optional breakdown and daily series. Аргументы: period*, ig_user_id*, metrics, breakdown, time_series
- `media` — posts, reels and carousels of an account published in a period with likes and comments counts. Аргументы: period*, ig_user_id*
- `media_insights` — insights for 1–25 media items (reach, views, saves, shares, interactions); unsupported metrics per media type are reported in errors. Аргументы: media_ids*, metrics

### `mk_tiktok` — TikTok Ads: режимы

- `fields` — reference of report levels, dimensions and metrics (no network). Аргументы: без аргументов
- `accounts` — advertisers authorized for the connection — advertiser_id, name, currency, timezone, status. Аргументы: без аргументов
- `report` — ad performance report (spend, impressions, clicks, conversions...) by advertiser/campaign/ad group/ad, optional daily split; long periods are split into 30-day windows automatically. Аргументы: period*, advertiser_id*, level, daily, metrics, campaign_ids, adgroup_ids
- `objects` — campaigns / ad groups / ads of an advertiser — status, objective, budget. Аргументы: advertiser_id*, level, status

### `mk_google_ads` — Google Ads: режимы

- `fields` — GAQL field metadata (googleAdsFields:search) — check names before a query. Аргументы: names, name_like
- `accounts` — accessible customer_ids (customers:listAccessibleCustomers). Аргументы: refresh
- `report` — arbitrary GAQL report via googleAds:search; a period and LIMIT are required. Аргументы: period*, customer_id*, query*, save
- `objects` — reference lists: campaigns / ad_groups / ads / conversion_actions. Аргументы: customer_id*, object*, status_filter, limit, save

### `mk_ga4` — Google Analytics 4: режимы

- `fields` — fields and argument schemas of the modes. Аргументы: property_id*
- `report` — regular (Core) runReport report — dimensions/metrics/filters/orderBys, a period is required, offset/limit with auto-pagination for large volumes, returnPropertyQuota; the response flags sampling and thresholds. Аргументы: period*, property_id*, dimensions, metrics*, dimension_filter, metric_filter, order_bys, offset, limit, save
- `realtime` — runRealtimeReport for the last ~30 minutes, with its own (Realtime) quota separate from Core reports. Аргументы: property_id*, dimensions, metrics*, dimension_filter, metric_filter, order_bys, limit, save
- `metadata` — the property's available dimensions and metrics (getMetadata), including registered custom customEvent:/customUser: ones — check them before report/realtime when using non-public field names. Аргументы: property_id*
- `accounts` — the source's available accounts. Аргументы: без аргументов

### `mk_search_console` — Google Search Console: режимы

- `fields` — reference of metrics, dimensions, search types, filter operators and data limits. Аргументы: без аргументов
- `sites` — Search Console properties of the Google account (URL-prefix and sc-domain) with the permission level. Аргументы: без аргументов
- `accounts` — same as sites, in the shared accounts shape. Аргументы: без аргументов
- `report` — Search Analytics — clicks, impressions, CTR and average position for a required period by date/query/page/country/device (search type web, image, video, news, discover, googleNews; filters; up to 50 000 rows, paged by 25 000); totals with impression-weighted position. Аргументы: period*, site_url*, dimensions, search_type, filters, aggregation_type, data_state, row_limit, start_row
- `sitemaps` — submitted sitemaps with errors, warnings, last download and submitted URL counts. Аргументы: site_url*, sitemap_index
- `inspect` — URL Inspection — Google index status of one URL (verdict, coverage, canonical, last crawl). Аргументы: site_url*, url*, language_code

### `mk_appsflyer` — AppsFlyer: режимы

- `fields` — reference: aggregate and raw report names, key raw columns, purchase_dedup arguments and output fields. Аргументы: без аргументов
- `accounts` — the account's apps (app_id, platform, name) — App list API (dev.appsflyer.com/hc/reference/app-list-ad-nets-api-get). Аргументы: без аргументов
- `aggregate` — aggregated Pull API reports (daily_report, partners_report, partners_by_date_report, geo_report, geo_by_date_report) — installs and in-app by media source/campaign/adset/geo; a period is required. Аргументы: period*, app_id*, report*, timezone, media_source, category, currency, additional_fields, maximum_rows, save
- `raw` — raw Pull API events row by row (installs_report, in_app_events_report, organic_installs_report, organic_in_app_events_report) — only with the Raw Data module in the plan; PII is stripped by default, include_pii turns it on explicitly. Аргументы: period*, app_id*, report*, timezone, media_source, event_name, geo, additional_fields, maximum_rows, include_pii, save
- `purchase_dedup` — purchase duplicates between the app (SDK) and server-to-server events (RevenueCat): raw in-app events for up to 31 days by Event Source and receipt validation, duplicate groups, signals and the recommended one-source-per-event scheme; counts only, no ids; needs the Raw Data module. Аргументы: period*, app_id*, timezone, event_names, first_purchase_events, match_window_minutes, maximum_rows
- `onelink` — read one short OneLink link by its ID (campaign parameters, template_id) — GET only. Аргументы: shortlink_id*

### `mk_appsflyer_write` — AppsFlyer, изменение OneLink и интеграций: режимы

- `onelink_write` — create/update/delete a short OneLink link (action: create|update|delete). dry_run: true by default — before → after with no changes; applied only with confirm: true. A separate OneLink API token (сохраняется на https://marketing-kit.app/connections#appsflyer). Аргументы: action*, shortlink_id*, data, ttl, brand_domain, dry_run, confirm
- `integration_copy` — copies partner integration settings (general_params, in_app_postbacks_params, including the postback event mapping) from one app to another for one platform — not a setup from scratch, only cloning what is already configured in the UI. dry_run: true by default, applied only with confirm: true. Аргументы: pid*, platform*, from_app_id*, to_app_ids*, dry_run, confirm

### `mk_revenuecat` — RevenueCat: режимы

- `fields` — reference of charts, overview metrics, resolutions, currencies, key permissions and rate limits. Аргументы: без аргументов
- `projects` — RevenueCat projects of the key with their apps (App Store, Play, Stripe…). Аргументы: без аргументов
- `accounts` — same as projects, in the shared accounts shape. Аргументы: без аргументов
- `overview` — key subscription metrics now — MRR, active subscriptions, active trials, revenue, new customers and active users of the last 28 days. Аргументы: project_id, currency
- `revenue` — total revenue of the project for a required period — gross, net of taxes or proceeds. Аргументы: period*, project_id, revenue_type, currency
- `chart` — a RevenueCat chart for a required period (mrr, revenue, actives, trials, churn, conversion_to_paying, trial_conversion, ltv, refunds, cohorts…) by day/week/month with segments and filters; rows date × measure × segment. Аргументы: period*, project_id, chart*, resolution, segment, limit_num_segments, filters, selectors, currency, totals_only
- `chart_options` — segments, filters, resolutions and selectors available for one chart. Аргументы: project_id, chart*
- `products` — products of the project (store identifier, type, duration, trial). Аргументы: project_id, app_id
- `entitlements` — entitlements of the project with their products. Аргументы: project_id
- `offerings` — offerings and packages (which products the paywall shows), the current offering. Аргументы: project_id
- `customer` — one customer by app user id — active entitlements, subscriptions (status, renewal, period, revenue) and purchases; personal data only with include_pii. Аргументы: project_id, app_user_id*, environment, include_pii

### `mk_app_store_connect` — App Store Connect: режимы

- `fields` — reference of modes, report columns, product type identifiers, key roles per mode, latency and rate limit. Аргументы: без аргументов
- `apps` — apps of the App Store Connect team (Apple id, name, bundle id, SKU, primary locale). Аргументы: без аргументов
- `accounts` — same as apps, in the shared accounts shape. Аргументы: без аргументов
- `sales` — Apple's own Sales and Trends for a required period (up to 92 days daily, or monthly) — installs, redownloads, updates, in-app purchases, subscription units, refunds and proceeds per currency (never converted), by date/country/device/product/app/product type; reports are Pacific-time, D+1. Аргументы: period*, app_id, group_by, frequency
- `subscriptions` — subscription reports for a required period (up to 92 days) — report=summary: active subscriptions, trials, billing retry and grace period by day (snapshot); report=events: Subscribe, trial starts and conversions, Cancel, Refund, Reactivate counts by event/date/country/subscription. Аргументы: period*, report, group_by
- `analytics` — App Store Analytics Reports of one app — funnel (impressions, page views, downloads, conversion), by source, sessions, installs/deletions, crashes, or any report by name; says so when analytics_enable has not been run for the app. Аргументы: period*, app_id*, report, report_name, category, group_by
- `reviews` — customer reviews of an app with developer responses, filtered by territory, rating, period and response; average rating and counts; read-only. Аргументы: app_id*, territory, rating, period, has_response, limit
- `versions` — App Store versions of an app (state, release type and date) with optional localized texts, plus app infos (name, subtitle). Аргументы: app_id*, platform, limit, include_localizations
- `experiments` — Product Page Optimization experiments with treatments and custom product pages of an app; the API gives no test results. Аргументы: app_id*

### `mk_app_store_connect_write` — App Store Connect, включение Analytics Reports: режимы

- `analytics_enable` — WRITE (needs an Admin key): creates the ONGOING Analytics Reports request of an app so that analytics has data in 1–2 days; dry_run by default, confirm true only after the user's explicit yes. Аргументы: app_id*, dry_run, confirm

### `mk_apple` — App Store: режимы

- `fields` — fields and argument schemas of the modes. Аргументы: без аргументов
- `accounts` — the source's available accounts. Аргументы: без аргументов
- `lookup` — app metadata by ID (version, rating, release date). Аргументы: id*, country
- `reviews` — latest user reviews. Аргументы: id*, country, page
- `charts` — top apps by country and chart type. Аргументы: country, chartType*, limit, genre, find_id, full

## Источник «Meta» (`mk_meta`)

`mk_meta` — Meta Marketing API (Graph, `ads_read`), только чтение. Модели
эффективности (`insights`), объекты кампаний (`objects`), счётчики событий
(`events`) и кастомные конверсии (`conversions`).

**Вход.** Доступ через подключение Meta на https://marketing-kit.app/connections: пользователь входит и нажимает «Разрешить», токенов не вводит. Источник не авторизован (`authorized: false`, ошибка `source_not_authorized`, в том числе после сброса входа) — отправь пользователя туда. Не предлагай выпускать токены системного пользователя.

**Кабинет.** Рекламный кабинет задаётся аргументом `act_id` (`act_…`); список доступных — `mode=accounts`.

**Атрибуция.** По умолчанию Meta считает установки/конверсии по окну 7 дней
после клика и 1 день после просмотра. Окна `7d_view`/`28d_view` этот пакет
сам убирает из запроса (Meta их больше не возвращает) — смотри
`action_attribution_windows.dropped` в ответе `insights`. Для сверки с
AppsFlyer используй `action_attribution_windows: ["1d_click"]`.

**Данные дописываются.** Цифры за последние 1–3 дня ещё меняются — не
считай их окончательными без предупреждения пользователя.

**`events` — счётчики без источника.** Число каждого события за период есть
(`insights.actions`/`app_custom_event.*` + статистика пикселя), а откуда оно
пришло — SDK приложения, Conversions API или партнёр (AppsFlyer) —
программно недоступно. Ответ этого режима не содержит поля источника
события; двойной счёт с AppsFlyer ищи сверкой чисел, не полагайся на
единственное число как на истину.

**iOS/SKAN.** Часть конверсий на iOS приходит через SKAdNetwork с задержкой
до нескольких дней и без разбивки ниже уровня кампании — резкий провал
последних дней по iOS сам по себе не аномалия.

**Бюджеты в `objects`.** `daily_budget`/`lifetime_budget` — в минорных
единицах валюты кабинета (например, центы для USD); ответ помечает это
`budget_unit: "minor"`.

Подробнее и готовые проверки на расхождения — `references/meta.md`.

Справка по источнику: `references/meta.md`.

## Источник «Facebook Pages» (`mk_fb_pages`)

`mk_fb_pages` — Facebook Pages (Meta Graph API), только чтение: страницы
пользователя (`accounts`), посты (`posts`), insights страницы
(`page_insights`) и постов (`post_insights`). Вход — та же авторизация Meta,
что и у рекламы; нужны разрешения `pages_show_list`, `pages_read_engagement`,
`read_insights`, а на странице у пользователя — задача «Анализ». Если ответ
содержит `reauthorize: true` — попроси переавторизовать Meta на
marketing-kit.app/connections (поставить все галочки в диалоге Facebook).

**Вход.** Доступ через то же подключение Meta на https://marketing-kit.app/connections, что и у рекламы. Источник не авторизован (`source_not_authorized`) — отправь пользователя туда. Если в ответе `reauthorize: true` или `missing_scopes` (Meta подключена без разрешений для Pages) — скажи нажать «Authorize» у Meta ещё раз на https://marketing-kit.app/connections и поставить все галочки; старое рекламное подключение продолжит работать.

**Порядок.** Сначала `accounts` — там `id` страницы; `page_id` обязателен во
всех остальных режимах. Токены страниц в ответах не показываются и не нужны.

**Охват и показы.** `page_total_media_view_unique` — охват (уникальные
люди), `page_media_view` — показы контента. Старые `page_impressions*`,
`post_impressions*`, `page_fans*`, `page_fan_adds/removes` Meta удалила —
не запрашивай их (ответ 100 «invalid metric»); замены — в `mode=fields`.
Охват по дням нельзя складывать в охват за период: сумма дневных значений
завышает его, скажи об этом пользователю.

**Подписчики.** `page_follows` — число подписчиков на конец дня (уровень),
в `totals` берётся последнее значение, а не сумма; приращение —
`page_daily_follows_unique`.

**Ограничения.** Insights есть только у страниц со 100+ подписчиками; период
больше 90 дней пакет режет на куски сам. Данные дописываются — последние
1–2 дня неполные. Если `accounts` вернул пустой список, а страницы у
пользователя есть, возможно, они выданы через Business portfolio — скажи
об этом и предложи проверить доступ.

## Источник «Instagram» (`mk_instagram`)

`mk_instagram` — Instagram (Meta Graph API, вход через Facebook), только чтение:
аккаунты (`accounts`), insights аккаунта (`account_insights`), медиа
(`media`) и insights медиа (`media_insights`). Только профессиональные
аккаунты (Business/Creator), привязанные к странице Facebook. Вход — та же
авторизация Meta, что и у рекламы; нужны `instagram_basic`,
`instagram_manage_insights`, `pages_show_list`, `pages_read_engagement`.
Если ответ содержит `reauthorize: true` — попроси переавторизовать Meta на
marketing-kit.app/connections (поставить все галочки в диалоге Facebook).

**Вход.** Доступ через то же подключение Meta на https://marketing-kit.app/connections, что и у рекламы. Источник не авторизован (`source_not_authorized`) — отправь пользователя туда. Если в ответе `reauthorize: true` или `missing_scopes` (Meta подключена без разрешений для Instagram) — скажи нажать «Authorize» у Meta ещё раз на https://marketing-kit.app/connections и поставить все галочки; старое рекламное подключение продолжит работать.

**Порядок.** Сначала `accounts` — там `ig_user_id`; он обязателен в
`account_insights` и `media`, а `media_ids` для `media_insights` берутся из
`media`.

**Метрики.** `impressions` Instagram удалил — используй `views` (просмотры)
и `reach` (охват, уникальные аккаунты). `profile_views` и `website_clicks`
тоже удалены (замена — `profile_links_taps`), у медиа удалены `plays` и
`video_views`. Охват нельзя складывать между окнами: пакет режет период на
окна до 30 дней и суммирует `total_value`, поэтому сумма `reach` по периоду
длиннее 30 дней завышена — скажи об этом пользователю. Дневные ряды —
`time_series: true` (`reach`, `follower_count`).

**Задержка.** Insights приходят с задержкой до 48 часов; хранятся до 90
дней (медиа — до 2 лет). Аккаунты меньше 100 подписчиков получают
неполный набор метрик, пустой ответ — не ноль.

**Типы медиа.** Часть метрик недоступна альбомам, историям и т. п. — такие
медиа перечислены в `errors` ответа `media_insights`, остальные вернулись.
Истории живут 24 часа и требуют минимум 5 зрителей.

## Источник «TikTok Ads» (`mk_tiktok`)

`mk_tiktok` — TikTok API for Business (v1.3), только чтение: рекламодатели
(`accounts`), отчёты по эффективности (`report`) и объекты кампаний
(`objects`). Органический TikTok (видео, подписчики) этот источник не
покрывает — для него нужна отдельная авторизация аккаунта TikTok, это
следующий шаг (BL-044).

**Вход.** Подключение «Authorize» у TikTok на https://marketing-kit.app/connections: пользователь входит в TikTok и разрешает доступ, токенов не вводит. Источник не авторизован (`source_not_authorized`) — отправь пользователя туда. Ответ `source_not_configured` значит, что владелец сервиса ещё не настроил TikTok — скажи об этом и не пытайся обойти.

**С чего начать.** `accounts` возвращает рекламодателей, которые дали доступ:
`advertiser_id`, название, валюту и часовой пояс. `advertiser_id` обязателен
в `report` и `objects` — не угадывай его, возьми из `accounts`.

**Валюта и часовой пояс.** Расход — в валюте рекламодателя, даты отчёта — в
его часовом поясе (они есть в `accounts` и в ответе `report`), а не в поясе
пары. При сверке с другими источниками (Meta, AppsFlyer) учитывай разницу
поясов и валют.

**Атрибуция.** Конверсии (`conversion`, `cost_per_conversion`) TikTok считает
по окнам атрибуции самого рекламодателя (по умолчанию 7 дней после клика и
1 день после просмотра, зависит от настроек события) — для сверки с
AppsFlyer ожидай расхождение.

**Данные дописываются.** Цифры за последние 1–3 дня ещё меняются; конверсии
приходят с задержкой — не считай свежие дни окончательными.

**Длинные периоды.** Источник отдаёт не больше 30 дней за запрос: пакет сам
режет период на окна по 30 дней. Для периода длиннее 30 дней без `daily: true`
пакет запрашивает дни и суммирует их по объекту (расход, показы, клики,
конверсии; CTR, CPC, CPM и стоимость конверсии пересчитываются). Охват
(`reach`) и другие неаддитивные метрики при таком суммировании не
возвращаются — смотри поле `dropped_metrics` в ответе.

**Идентификаторы.** `campaign_id`, `adgroup_id`, `ad_id` — длинные числа в
виде строк: не превращай их в числа. Бюджеты в `objects` — в валюте
рекламодателя.

## Источник «Google Ads» (`mk_google_ads`)

`mk_google_ads` — Google Ads API (REST, GAQL) напрямую, без клиентской
библиотеки. Только чтение (ADR-0005): режимов изменения нет.

**Вход.** Доступ через подключение Google на https://marketing-kit.app/connections: один раз, сразу для GA4, Google Ads и Search Console. Источник не авторизован (`authorized: false`, ошибка `source_not_authorized`) — отправь пользователя туда; режима `connect` у инструмента нет. Какие аккаунты видны (property в GA4, customer_id в Google Ads) — решают права подключённого Google-аккаунта в самом сервисе.

**Аккаунты.** `mode=accounts` — все кабинеты, которые видит этот Google-аккаунт:
и доступные напрямую, и лежащие под менеджерскими (MCC) — с именем, статусом,
путём (`direct` / `via_manager` с id и именем MCC) и пометкой `deactivated` для
отменённых. Менеджерский аккаунт определяется сам и подставляется как
`login-customer-id` в каждый запрос — просить пользователя вписывать
login customer ID не нужно. Карта кэшируется на час, `refresh: true`
пересобирает её. Вручную заданный login customer ID (override) важнее автоопределения — нужен только если кабинет виден
через несколько MCC и нужен конкретный. `USER_PERMISSION_DENIED` и с найденным
MCC — кабинет не виден этому Google-аккаунту: пусть проверит доступ в Google Ads.

**Поля.** Не угадывай имена GAQL-полей: `mode=fields` с `names` (точные
имена) или `name_like` (подстрока) — вернёт `selectable`/`filterable`/
`data_type`/`enum_values` из `GoogleAdsFieldService`.

#### Режимы с данными

- `report` — произвольный GAQL через `googleAds:search`. Обязателен
  `customer_id`, `query` (`SELECT ... FROM <ресурс> [WHERE ...] LIMIT n`) и
  период ядра. **`LIMIT` в тексте запроса обязателен явно** — без него
  запрос отклоняется до отправки источнику, тяжёлые запросы (`LIMIT`
  больше 10 000, несколько `FROM`, текст на изменение данных) тоже
  отклоняются заранее, с русским объяснением. Фильтр по `segments.date`
  можно не писать самому — период ядра подставится в запрос автоматически;
  если он уже есть в тексте, используется как есть. Ответ добавляет к
  каждому полю `*_micros` соседнее поле без суффикса — уже делённое на
  1 000 000 (валюта счёта — поле `currency` в ответе, `customer.currency_code`
  подставляется в запрос сам, если в нём есть `metrics.cost_micros`).
- `objects` — готовые справочники: `campaigns`, `ad_groups`, `ads`,
  `conversion_actions`. `status_filter` — необязательное условие `WHERE`
  (например, `campaign.status = 'ENABLED'`).

#### Конверсии и деньги

- Конверсии считаются по **дате клика**, не по дате конверсии; окно
  атрибуции задаётся в самом конверсионном действии
  (`references/google_ads.md`).
- `cost_micros` и любое другое поле `*_micros` — микроединицы валюты
  счёта; не дели вручную, инструмент уже возвращает готовое значение
  рядом.

#### Уровень доступа и лимиты

Explorer access (продакшн-аккаунты, без ручной заявки) — 2 880 операций в
день на аккаунт; для редких интерактивных запросов почти всегда
достаточно. При исчерпании квоты источник отвечает 429 — ядро само
повторяет запрос с задержкой; если лимит не снялся — понятная ошибка, а не
пустой ответ. Explorer не даёт создавать аккаунты и управлять
пользователями/биллингом — этому источнику (только чтение) это не нужно.

Справка по источнику: `references/google_ads.md`.

## Источник «Google Analytics 4» (`mk_ga4`)

`mk_ga4` — Google Analytics Data API v1beta (`report`, `realtime`) и Admin
API v1beta (`accounts`, `metadata`). Данные считаются по property (`property_id`
— числовой ID GA4, не Measurement ID `G-XXXX`): список — `mk_ga4 mode=accounts`.

**Вход.** Доступ через подключение Google на https://marketing-kit.app/connections: один раз, сразу для GA4, Google Ads и Search Console. Источник не авторизован (`authorized: false`, ошибка `source_not_authorized`) — отправь пользователя туда; режима `connect` у инструмента нет. Какие аккаунты видны (property в GA4, customer_id в Google Ads) — решают права подключённого Google-аккаунта в самом сервисе.

**Особенности:**

- **`report` — Core-отчёт, `realtime` — отдельная (Realtime) квота.** Не
  путать одно с другим при чтении `property_quota` в ответе.
- **Кастомные поля** — `customEvent:<param>` (событийные) и
  `customUser:<param>` (пользовательские). Запрос с незарегистрированным
  именем падает — сначала `mode=metadata` (он же общий режим `fields`), не
  угадывать имена.
- **Пагинация — только `report`.** `limit` в аргументах — это желаемое число
  строк всего, не размер одного сетевого запроса: свыше 10 000 инструмент сам
  ходит в источник постранично через `offset`, каждый раз не больше 10 000 за
  один вызов источника. `pages_fetched` в ответе — сколько запросов ушло.
- **Сэмплирование и пороги — в каждом ответе `report`/`realtime`:**
  `subject_to_thresholding` (малая выборка, часть данных могла не пройти
  порог приватности), `sampling_metadatas` (отчёт построен по выборке, не по
  всем событиям), `data_loss_from_other_row` (часть комбинаций измерений
  свёрнута в `(other)` из-за кардинальности). Любой из них `true`/непустой —
  скажи об этом при ответе на вопрос пользователя, не подавай цифры как
  точные молча.
- **Данные дописываются 24–48 часов** после события — «за вчера» может
  измениться при повторном запросе.

Справка по источнику: `references/ga4.md`.

## Источник «Google Search Console» (`mk_search_console`)

`mk_search_console` — Google Search Console, органический поиск Google, только чтение:
ресурсы (`sites`), отчёт Search Analytics (`report`), файлы sitemap
(`sitemaps`) и проверка URL в индексе (`inspect`); право — `webmasters.readonly`.

**Вход.** Доступ через то же подключение Google на https://marketing-kit.app/connections, что у GA4 и Google Ads. Источник не авторизован (`source_not_authorized`) — отправь пользователя туда. Если в ответе `reauthorize: true` или `missing_scopes` (Google подключён без права Search Console — подключение старое или галочку сняли) — скажи нажать «Authorize» у Google ещё раз на https://marketing-kit.app/connections и оставить галочку Search Console; GA4 и Google Ads продолжат работать. Ошибка `SERVICE_DISABLED` («Search Console API is not enabled in the Google Cloud project») — дело владельца сервиса, не пользователя: скажи это и не предлагай переподключаться.

**Когда брать.** Вопросы про органический поиск Google: по каким запросам
находят сайт, клики и показы в выдаче, CTR, средняя позиция, какие страницы
получают трафик из поиска, страны и устройства поиска, индексируется ли
страница, что с sitemap. Не путай с GA4: GA4 — поведение на сайте и в
приложении (сессии, события, конверсии) из всех каналов; Search Console — то,
что было **до клика** в выдаче Google. Платный поиск — Google Ads.

**Порядок.** Сначала `sites` — там `site_url` (URL-префикс со слэшем на конце
`https://example.com/` или доменный ресурс `sc-domain:example.com`); передавай
его как есть. Потом `report` с периодом.

**Отчёт.** `dimensions` — `date`, `query`, `page`, `country`, `device`
(`hour`, `searchAppearance` — особые случаи). Без измерений — итог за период.
`search_type` — `web` по умолчанию; у `discover` и `googleNews` нет `query`.
`filters` — список условий AND (`dimension`, `operator`, `expression`), страны —
alpha-3 строчными (`svn`). Строки отсортированы по кликам; `row_limit` по
умолчанию 1000. `ctr` — доля (0.034 = 3.4 %), позицию не складывай и не
усредняй без весов — бери `totals.position` (взвешена показами).

**Задержка и границы.** Данные приходят через 2–3 дня, даты — по
тихоокеанскому времени, хранение — 16 месяцев. Если пользователь спрашивает
«за вчера» — предупреди, что данных может ещё не быть. API отдаёт не больше
50 000 строк в сутки, анонимизированные запросы не возвращаются — сумма по
запросам меньше итога ресурса, это не ошибка.

**Ошибки.** `SERVICE_DISABLED` («Search Console API is not enabled in the
Google Cloud project») — настройка владельца сервиса, не пользователя: скажи
это прямо, GA4 и Google Ads при этом работают. 403 по ресурсу — у аккаунта нет
доступа к этому сайту в Search Console.

## Источник «AppsFlyer» (`mk_appsflyer`)

- Установка = первый запуск приложения с SDK AppsFlyer; пользователи без
  SDK в AppsFlyer не видны вовсе.
- Установки с веба на iOS связываются с кликом не всегда — часть уходит в
  organic; на Android связка через Install Referrer почти полная.
- In-app события приписываются источнику установки, а не последнему клику.
- Период (`period: {start, end}`) обязателен в `aggregate` и `raw`. Часовой
  пояс явный: данные в выбранной таймзоне доступны только с момента её
  настройки в AppsFlyer, до этого источник отдаёт UTC — фактически
  применённый пояс возвращается в ответе как `requested_timezone`.
- `app_id` — обязательный параметр `aggregate`/`raw`, свой на каждую
  платформу (App Store id или пакет Android). Один инструмент AppsFlyer
  может отвечать за несколько приложений аккаунта — не угадывай `app_id`,
  спроси его у пользователя или вызови `mode=accounts`.

#### Режимы

- `aggregate` — отчёты `daily_report`, `partners_report`,
  `partners_by_date_report`, `geo_report`, `geo_by_date_report`: установки
  и in-app в разрезе media source/кампании/адсета/гео.
- `raw` — установки и in-app события построчно (`installs_report`,
  `in_app_events_report`, `organic_installs_report`,
  `organic_in_app_events_report`). **Доступен только при модуле Raw Data в
  тарифе** — без него источник отвечает ошибкой, инструмент возвращает
  понятную русскую ошибку «нет модуля Raw Data», а не пустой результат.
  ПДн (device/рекламные ID, IP, `customer_user_id`) стрипаются по
  умолчанию; `include_pii: true` возвращает их — используй, только если
  пользователь явно попросил и объяснил зачем.
- `onelink` — чтение одной короткой ссылки по `shortlink_id` (параметры
  кампании, `template_id`). Только GET.
- `purchase_dedup` — дубли покупок между приложением (SDK) и
  server-to-server событиями (RevenueCat → AppsFlyer) за период до 31 дня;
  только счётчики, без id. Нужен модуль Raw Data. Рецепт — ниже.

#### Дубли покупок AppsFlyer ↔ RevenueCat (ADR-0035)

Когда спрашивают «покупки задваиваются», «в AppsFlyer выручки больше, чем в
RevenueCat», «правильно ли настроены покупки», «надо ли ставить Purchase
Connector»:

1. `mk_appsflyer` `mode=purchase_dedup`, `args`: `app_id` (iOS и Android — по
   вызову на каждое), `period` (до 31 дня, по умолчанию — последние 7–14
   полных дней), часовой пояс пользователя. Свои имена событий в интеграции
   RevenueCat — передай их в `event_names` (и в `first_purchase_events` для
   первой покупки и старта триала).
2. За те же дни и в том же поясе — `mk_revenuecat` `chart`: `trials_new`,
   `actives_new` (новые платные) и `revenue` (транзакции), `resolution: day`.
   Сравни с `by_day` режима: клиентских первых покупок (`sdk_first_purchase`)
   должно быть около «новые триалы + новые платные без триала»; примерно
   вдвое больше событий, чем у RevenueCat, — признак дубля. Источники считают
   по-разному (атрибуция, пояс, песочница, задержка) — показывай оба числа.
3. Ответ пользователю:
   - **есть ли дубли, сколько, откуда** — из `duplicates` и `signals`:
     `sdk_s2s` (одна покупка пришла из приложения и от RevenueCat; лишних
     событий `extra_events`, лишней выручки `double_revenue_usd`), `sdk_sdk`
     (два клиентских события: ручной `af_purchase` + `validateAndLog` или
     Purchase Connector, либо restore), `s2s_s2s`. `allowed` — не дубль: это
     событие RevenueCat с другим именем и без выручки, так и задумано;
   - **схема «одно событие — один источник»** (`recommended_scheme`):

     | Событие | Кто шлёт в AppsFlyer | Как |
     |---|---|---|
     | первая покупка, старт триала (пользователь в приложении) | приложение (SDK) | `validateAndLogInAppPurchase` на месте ручного вызова `af_purchase` |
     | конверсия триала, продления | RevenueCat S2S | интеграция RevenueCat → AppsFlyer |
     | отмены, возвраты | RevenueCat S2S | интеграция, отрицательная выручка |
     | initial purchase и trial started в интеграции RevenueCat | никто | пустое имя события (не отправляется) или своё имя без выручки |

   - **что поменять в коде приложения:** ручной `af_purchase` заменить на
     `validateAndLogInAppPurchase` **в том же месте** — это замена события
     на проверенное, а не второй источник; Purchase Connector рядом не
     ставить (с `validateAndLog` — снова два клиентских события; AppsFlyer:
     «одна интеграция на приложение»). Форма с `AFSDKPurchaseDetails`
     (`productId`, `transactionId`, `purchaseType`) — с SDK 6.17.8; старая
     форма с ценой и валютой устарела;
   - **что поменять в RevenueCat:** Integrations → AppsFlyer — у Initial
     Purchase и Trial Started очистить имя события или дать своё имя без
     выручки; продления, конверсии, отмены, возвраты оставить.
4. Подводные камни (скажи те, что относятся к ответу):
   - клиентское событие двигает conversion value SKAdNetwork и быстро уходит
     партнёрам для оптимизации; S2S-события в SKAN попадают, только если в
     SKAN Conversion Studio включено «Record in-app events sent by
     server-to-server API», и то лишь когда приложение открывается в окне
     измерения;
   - RevenueCat в своей инструкции советует убрать **всё** клиентское
     логирование выручки — схема выше не противоречит этому, только если
     первая покупка RevenueCat отключена или без выручки;
   - старт триала с полной ценой в `af_purchase` завышает выручку
     (`trial_logged_with_revenue`): на триале выручка 0;
   - restore purchases не должен вызывать `validateAndLog` — иначе повтор
     (`validated_twice`);
   - TestFlight и песочница не проходят боевую проверку: для тестов —
     `useReceiptValidationSandbox = true` только в тестовой сборке;
   - без сети клиентское событие может не дойти — первая покупка тогда
     видна только в RevenueCat;
   - нет S2S-событий вовсе (`no_s2s_events`) — интеграция RevenueCat
     выключена или не задан `$appsflyerId`: продлений в AppsFlyer нет.
5. Без модуля Raw Data (ошибка «нет модуля Raw Data») — только косвенно:
   `aggregate` `daily_report` (события `af_purchase`) против транзакций
   `revenue` RevenueCat по дням; скажи, что разделить SDK и S2S без Raw Data
   нельзя.

V-Kit здесь только читает и советует: ни в AppsFlyer, ни в
RevenueCat, ни в коде приложения он ничего не меняет.

#### Запись (ADR-0005): только OneLink-ссылки и копия партнёрской интеграции

Режимы записи — у отдельного инструмента `mk_appsflyer_write` (у `mk_appsflyer` их нет); единственная поверхность записи этого источника — по решению владельца. Каждый режим записи: `dry_run: true` по умолчанию —
показывает объект/поля/before → after и ничего не меняет; применяется
только с явным `confirm: true` (спроси у пользователя «да» перед этим —
согласие не переносится с предыдущего вызова); после применения инструмент
сам перечитывает объект и возвращает новое состояние; до/после пишутся в журнал сервера.

- `onelink_write` — создание/обновление/удаление короткой OneLink-ссылки
  (`action: create|update|delete`, `POST/PUT/DELETE
  onelink.appsflyer.com/api/v2.0/shortlinks/{id}`). Требует **отдельный**
  OneLink API-токен (сохраняется на https://marketing-kit.app/connections#appsflyer, не тот же
  токен, что для чтения) — включается через менеджера AppsFlyer (CSM), после
  генерации активируется до 30 минут. 401/403 на этом режиме почти всегда
  означает, что токен ещё не включён CSM или не активировался — не пытайся
  чинить это подстановкой другого токена, скажи пользователю обратиться к
  CSM.
- `integration_copy` — копирует `general_params`/`in_app_postbacks_params`
  партнёра (включая маппинг событий постбэков) с одного приложения на
  другое, одна платформа за вызов. Это **клонирование уже настроенной в UI
  конфигурации**, а не настройка партнёра с нуля — эндпоинт этого не умеет
  (ограничение API, не пакета).

#### Только в интерфейсе AppsFlyer (не ищи обход через API)

Публичный API AppsFlyer не даёт программно менять следующее — если
пользователь просит это сделать, скажи прямо, что нужно зайти в кабинет
AppsFlyer:

- переключение in-app постбэков в Meta и настройку event-mapping «с нуля»
  (без `integration_copy`) — Settings → Integrated Partners;
- окна атрибуции и re-attribution (attribution window) — App Settings;
- шаблоны OneLink (логика редиректов/deep linking) — OneLink Management;
- общие App Settings, не перечисленные выше как доступные через API.

#### Rate limit и повторные запросы

Точные официальные цифры лимита Pull API инструмент не знает надёжно —
подтверждённый источник (`dev.appsflyer.com`) цифр не дал, только сторонний. При превышении
источник отвечает 429, ядро само повторяет запрос с задержкой; если лимит
не снялся — понятная ошибка, а не пустой ответ. Не дроби широкий запрос на
много мелких без нужды: один запрос на весь период быстрее и меньше риска
упереться в лимит.

Справка по источнику: `references/appsflyer.md`.

## Источник «RevenueCat» (`mk_revenuecat`)

`mk_revenuecat` — RevenueCat, подписки внутри приложений, только чтение (REST API v2):
ключевые метрики (`overview`), выручка за период (`revenue`), чарты (`chart`,
`chart_options`), справочник проекта (`projects`, `products`, `entitlements`,
`offerings`) и один клиент по app user id (`customer`).

**Когда брать.** Вопросы про деньги и подписки приложения: MRR, ARR, активные
подписки и триалы, выручка (gross / proceeds), конверсия триала в оплату, отток
(churn), возвраты, LTV, когорты, какой продукт или offering продаётся, что с
подпиской конкретного пользователя. Не путай с AppsFlyer: AppsFlyer — откуда
пришли **установки** и in-app события (атрибуция по медиа-источникам и
кампаниям); RevenueCat — что пользователи **купили и продлили** (без разбивки по
рекламным кампаниям). App Store (`mk_apple`) — только публичная карточка:
рейтинг, отзывы, позиции; продаж там нет. Если спрашивают «сколько заработали с
кампании» — RevenueCat даст выручку, AppsFlyer — установки по кампании; скажи,
что связать их можно только через атрибуцию.

**Порядок.** `overview` — без аргументов (проект ключа берётся сам). Для трендов —
`chart` с периодом, `chart` = `mrr`, `revenue`, `actives`, `trials`, `trials_new`,
`churn`, `conversion_to_paying`, `trial_conversion`, `refund_rate`… (список —
`mode=fields`); сегменты и фильтры чарта — сначала `chart_options`. Точки с
`incomplete: true` — незакрытый период, в тренд не бери; сегменты не складывай.

**Клиент.** `customer` по `app_user_id` — подписки, статус, продление, выручка.
ПДн (атрибуты вроде `$email`, алиасы, id транзакций стора) по умолчанию не
отдаются; `include_pii: true` — только если пользователь явно попросил и
объяснил зачем.

**Ключ.** Нет ключа (`revenuecat_key_missing`) или RevenueCat его не принял
(401 `authentication_error`) — нужен **secret API key V2** с правами только на
чтение: RevenueCat → Project settings → API keys → + New secret API key →
версия V2, Charts & Metrics / Customer Information / Project Configuration — Read
→ Generate; сохранить на https://marketing-kit.app/connections#revenuecat. Ключи v1 и публичные ключи SDK (`appl_…`,
`goog_…`) не подходят. Пошагово: https://marketing-kit.app/connections#revenuecat.
Сервер хранит ключ зашифрованным. 403 `authorization_error` — у ключа нет права на этот
раздел или он от другого проекта. Метрики и чарты — не больше 25 запросов в
минуту на ключ.

## Источник «App Store Connect» (`mk_app_store_connect`)

`mk_app_store_connect` — App Store Connect API, официальные данные Apple по **вашим** приложениям
(командный ключ сохранён на сайте): продажи и загрузки (`sales`), отчёты по подпискам
и их события (`subscriptions`), воронка App Store и источники трафика, сессии, удаления,
краши (`analytics`), отзывы с ответами (`reviews`), версии и состояния (`versions`),
эксперименты Product Page Optimization и custom product pages (`experiments`), список
приложений (`apps`). Единственная запись — `analytics_enable` у отдельного инструмента `mk_app_store_connect_write` (у `mk_app_store_connect` её нет).

**Когда брать.** Нужны цифры из самого App Store Connect: сколько установок, повторных
загрузок и обновлений по странам и устройствам, выручка и возвраты, активные подписки и
пробные, отмены и конверсия триала по отчётам Apple, показы → просмотры страницы →
загрузки, отзывы и ответы на них, что сейчас в App Store по версиям. Не путай:
`mk_apple` — публичные данные **любого** приложения без ключа (рейтинг, текущая версия,
топы); `mk_appsflyer` — атрибуция по медиа-источникам и кампаниям; `mk_revenuecat` —
подписки по всем магазинам, MRR и метрики почти в реальном времени. App Store Connect —
свои приложения, задержка D+1 (отчёт за день готов к ~8:00 по тихоокеанскому времени
следующего дня), без MRR и без разбивки по рекламным кампаниям.

**Порядок.** Сначала `apps` — взять Apple id приложения (`app_id`). `sales`: `period`
до 92 дней (дневные отчёты) или `frequency: MONTHLY`; `group_by` — date, country, device,
product, app, product_type (до двух). Деньги в ответе по валютам выплат и покупателей,
**не пересчитываются**; возвраты — отрицательные единицы; в `missing_dates` — дни без
отчёта (вчера до 8:00 PT отчёта может ещё не быть — скажи об этом, не считай ошибкой).
`subscriptions`: `report: summary` — слепок активных подписок по дням (итог берётся за
последнюю дату, не суммируется), `report: events` — события (новые, триалы, конверсия
триала, отмены, возвраты, реактивации). `analytics`: `report` funnel, sources, sessions,
installs, crashes или custom; данных за последние 2–5 дней может не быть (запаздывание),
у малых приложений — пороги приватности (от 5 пользователей). Удержания (retention)
готовым отчётом в API нет — не выдумывай. `experiments`: результатов тестов (конверсия,
уверенность) в API нет — только настройка и состояние.

**Включение аналитики.** Если `analytics` отвечает `enabled: false`, предложи
`analytics_enable`. Это запись в аккаунт: сначала вызови с `dry_run` (по умолчанию), покажи
пользователю план и дождись явного «да»; только затем повтори с `dry_run: false` и
`confirm: true`. Нужен ключ с ролью Admin; данные появятся через 1–2 дня. Если запрос уже
есть, режим скажет `already_enabled` и ничего не создаст. Ответы на отзывы пока не
поддерживаются.

**Ключ.** Нет ключа (`app_store_connect_key_missing`) — ключ сохраняется один раз на
https://marketing-kit.app/connections#app-store-connect: Issuer ID, Key ID и файл `.p8`
(App Store Connect → Users and Access → Integrations → Team Keys). Нужен командный
(team) ключ, личный не читает продажи. Для `sales` и `subscriptions` ещё номер поставщика
(`app_store_connect_vendor_number_missing`): Payments and Financial Reports, слева вверху.
Роли: `sales`, `subscriptions`, `analytics` — Admin, Sales and Reports или Finance;
`analytics_enable` — только Admin; `apps`, `reviews`, `versions`, `experiments` — Admin,
App Manager, Developer или Marketing. Один ключ на всё — Admin. 401 — Apple не принял
ключ (проверь Issuer ID, Key ID, не отозван ли); 403 — роли не хватает (в тексте названа
нужная); 429 — лимит около 3500 запросов в час на ключ.

## Источник «App Store» (`mk_apple`)

`mk_apple` — публичные API App Store (iTunes Lookup, Customer Reviews RSS, Marketing Tools Charts). Никаких ключей и авторизации не требует.

**Особенности:**

- **Рейтинг** — по стране App Store; общего мирового нет. В странах, где приложение мало устанавливают (например, RU), рейтинг может быть 0 — это не ошибка.
- **Отзывы** — только последние (обычно 3–5), не полная история.
- **Топ-приложения** — два типа: `top-free` и `top-paid`; фильтр по жанру использует legacy RSS API (основные жанры: 6013 = Health & Fitness, 6023 = Food & Drink). Параметр `find_id` найдёт позицию конкретного приложения в топе (например, где приложение занимает место).

## Большие ответы — ссылками

Таблица больше 200 строк, больше 50 КБ или запрос с `args.save: true` — сервер
возвращает сводку (`columns`, `row_count`, `totals`, `preview` — первые 20 строк)
и ссылки `download.csv` и `download.json` (действуют 24 часа, только для вошедшего
пользователя). Ссылки нужны, даже когда строк немного, — повтори с `args.save: true`.

## Запись (только AppsFlyer, `mk_appsflyer_write`)

Все источники, кроме AppsFlyer, только для чтения, а чтение AppsFlyer — это
`mk_appsflyer`. Изменения — отдельный инструмент `mk_appsflyer_write` (режимы
`onelink_write`, `integration_copy`) — работай так:

1. Вызови сначала с `dry_run: true` (по умолчанию) и покажи пользователю, что
   именно изменится: объект, поле, **было → станет**.
2. Применяй только после явного «да» на **это** изменение — вызовом с
   `dry_run: false` и `confirm: true`. Одно «да» — одно изменение; согласие
   на прошлое не переносится. Сам `confirm: true` не ставь никогда.
3. После применения перечитай объект и подтверди пользователю новое
   состояние. Ответ с `dry_run: true, applied: false` на запрос с
   `confirm: true` значит, что сервер ничего не применил — не выдавай это за
   выполненное.

## Запись: включение Analytics Reports (`mk_app_store_connect_write`)

Единственная запись в App Store Connect — режим `analytics_enable`: создаёт
ONGOING-запрос Analytics Reports, без которого `analytics` отвечает `enabled:
false`. Работай так:

1. Вызови сначала с `dry_run: true` (по умолчанию), покажи пользователю план и
   дождись явного «да» на это включение.
2. Только после «да» повтори с `dry_run: false` и `confirm: true`. Сам
   `confirm: true` не ставь никогда. Нужен ключ с ролью Admin.
3. Скажи, что данные появятся через 1–2 дня. Никогда не включай аналитику
   сам, «заодно».

Ответы на отзывы пока не поддерживаются — только чтение отзывов.

## Чего не делать

- Не используй Supermetrics и браузер для данных, которые есть в этих источниках. Пока инструментов V-Kit нет — не предлагай их первым делом, только путь к **Connect** (см. выше).
- Не отдавай сырые персональные данные (ID устройств, IP, `customer_user_id`,
  `$email` клиента RevenueCat), если пользователь явно не попросил и не объяснил зачем.
