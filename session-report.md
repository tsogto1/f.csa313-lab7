# Session report

Тестер: Х.Цогтбаяр — B232270072; хүсэлтийн дагуу Codex AI агент браузер/API туршилтыг гүйцэтгэж, тэмдэглэл хөтөлсөн. Оюутан өөрөө гараар 60 минут тест хийсэн гэж тайлагнаагүй.

Огноо: 2026-10-20, эхэлсэн 15:25:27 (Asia/Ulaanbaatar, UTC+08:00).
Бодит дуусах цаг: 16:25:27.234 (Asia/Ulaanbaatar, UTC+08:00). Хугацаа: 60 минут (3600.004 секунд).

Mission: Уншлагын жагсаалт аппын чанарыг шинжлэх.

Charter: [charter.md](charter.md) — GUI, талбарын шалгалт, өгөгдлийн бүрэн бүтэн байдал болон API-г Supermodel, Couch Potato, Saboteur аяллаар судлах. Charter-ийн `24c7790` commit session-ээс өмнө GitHub main-д push хийгдсэн.

## Орчин

- Node.js v20.19.2 (хэрэглэгчийн өгсөн хувилбартай тааруулсан).
- Chromium 154.0.8037.57, Playwright Core 1.64.1, headless.
- Debian GNU/Linux 13.6 (trixie), x86_64.
- Үндсэн viewport 1440 × 1000; бусад viewport-ийг тэмдэглэлд тусад нь бичнэ.
- Багшийн app.js: SHA-256 `a2158dc202e62a18f11adcc0feca1d84fb6c6a9ec269b8eb63bc72f10eb27c6c`; эх кодыг уншаагүй, өөрчлөөгүй.
- Аппын өгөгдөл санах ойд; шинэ процессыг эхлүүлэх бүрд анхны 3 номыг батална.
- Цагтай тэмдэглэл нь бодит гүйцэтгэлийн үеэр append хийгдэнэ. Screenshot нь бодит браузерын зураг; API нотолгоо нь curl -i-ийн бүтэн гаралт.

## Тэмдэглэл (он цагийн дарааллаар, session дотор бичсэн түүхий тэмдэглэл)

- 15:25:52 (+0.4 мин) Session эхлэв. Урьдчилсан нээлтээр анхны 3 номтойг баталсан; тоолуур, оны дүрслэл зөрүүтэй харагдсан тул эхний аяллаар шинэ төлөвөөс батална. Charter session-ээс өмнө push хийгдсэн. Эх кодыг уншаагүй.
- 15:26:00 (+0.5 мин) Supermodel: шинэ процесс, 1440×1000. BUG-01: tbody-д 3 мөр байхад «Нийт ном: 4». BUG-02: он 1,971 / 2,008 / 1,999 гэж таслалтай. BUG-03: Устгах товчны computed background rgb(44,122,75), ногоон; шаардлага улаан. screenshot bug-01/02/03 хадгалав. Эдгээр нь ижил дэлгэц дээрх 3 өөр oracle зөрчил.
- 15:26:54 (+1.5 мин) Baseline нэмэх/устгахыг шалгаж байна. Click-ийн дараах шууд DOM snapshot нь fetch дуусахаас өмнөх агшин байж болохыг ажиглав; тулгалтад хүсэлтийн хариу болон UI шинэчлэлтийг хүлээж дахин шалгана. Түр snapshot-оор нэмэлт согог дүгнээгүй.
- 15:27:12 (+1.8 мин) Дараагийн чиглэл: нэмэх→устгахын мессеж, хуучин хувилбарын холбоос, хайлтын baseline, урт оролтын дүрслэл. Браузерын харагдах DOM болон сүлжээний хүсэлт л ажиглаж, app.js-ийн эх кодыг нээгээгүй.
- 15:27:26 (+2.0 мин) BUG-04 батлав: SBTM baseline / Х.Цогтбаяр / 2026 нэмэхэд 4 мөр, Нийт ном 5; шинээр нэмсэн мөрийг устгасны дараа 3 мөр, Нийт ном 4, мессеж «Ном нэмэгдлээ» хэвээр. API POST/GET/stats/DELETE хүсэлтүүдийг runtime сүлжээнээс ажиглав. screenshot bug-04 нь устгасны дараах төлөв.
- 15:28:05 (+2.6 мин) BUG-05: «Хуучин хувилбар» холбоос /old руу очиход HTTP 500, дэлгэц Internal Server Error. BUG-06: Clean/Robert/Тунгалаг хайлт тус бүр 1 мөр, clean/robert/тунгалаг тус бүр 0 мөр — үсгийн хэмжээг ялгаж байна. screenshot bug-05/06 хадгалав. Хайлт зохиолч дээр ажилладаг боловч үсгийн хэмжээнээс үл хамаарах шаардлага зөрчсөн.
- 15:29:08 (+3.7 мин) Baseline reload 30/30: HTTP 200, 3 мөр тогтвортой, бүх тохиолдолд Нийт ном 4; хамгийн удаан ажиглалт 809 ms (750 ms зориудын DOM settle багтсан, performance benchmark биш). Үлдсэн session-ийн турш 5 секунд тутам read-only браузер/API monitor ажиллуулж тасалдал, тоолуурын төлөвийг JSONL-д хадгалж эхлүүлэв; өөрийн зориудын restart-ийг алдаа гэж тооцохгүй.
- 15:29:50 (+4.4 мин) Supermodel viewport 320px: baseline document 373px; 200 ширхэг A гарчгийн дараа document 2419px, table 2418.5px, мөр 4.
- 15:29:52 (+4.4 мин) Supermodel viewport 375px: baseline document 375px; 200 ширхэг A гарчгийн дараа document 2419px, table 2418.5px, мөр 4.
- 15:29:54 (+4.5 мин) Supermodel viewport 768px: baseline document 768px; 200 ширхэг A гарчгийн дараа document 2419px, table 2418.5px, мөр 4.
- 15:29:56 (+4.5 мин) Supermodel viewport 1024px: baseline document 1024px; 200 ширхэг A гарчгийн дараа document 2501px, table 2418.5px, мөр 4.
- 15:29:57 (+4.5 мин) Supermodel viewport 1440px: baseline document 1440px; 200 ширхэг A гарчгийн дараа document 2709px, table 2418.5px, мөр 4.
- 15:29:59 (+4.5 мин) Supermodel viewport 1920px: baseline document 1920px; 200 ширхэг A гарчгийн дараа document 2949px, table 2418.5px, мөр 4.
- 15:30:30 (+5.1 мин) BUG-07 батлав: гарчигт 200 ширхэг A, зохиолч Урт оролтын зохиолч, он 2020 нэмэхэд desktop 1440 px viewport дээр document 2709 px, table 2418.5 px болж хэвтээ overflow гарлаа. 320/375/768/1024/1920 px дээр мөн давтагдав. screenshot bug-07 нь 1440 px дээрх full-page бодит зураг. Шинэ согогийг эх кодоос таамаглаагүй.
- 15:31:08 (+5.7 мин) Supermodel-ийн өргөтгөсөн campaign эхлэв: viewport, Latin/Монгол/emoji/combining Unicode, урт гарчиг/зохиолч, хайлт, reload, устгах дарааллын төлөвүүдийг UI-ээр шалгана. Үйлдлийн дараа бодит DOM settle болон мессежийн тогтвортой байдлыг ажиглана.
- 15:31:18 (+5.9 мин) UI campaign {"case":1,"width":1440,"size":1,"seed":"Latin","addRows":4,"allRows":4,"reloadRows":4,"deleteRows":3,"documentWidth":1440,"searchRows":[1,0,1]}
- 15:31:50 (+6.4 мин) UI campaign {"case":4,"width":375,"size":1,"seed":"Latin","addRows":4,"allRows":4,"reloadRows":4,"deleteRows":3,"documentWidth":375,"searchRows":[1,0,1]}
- 15:32:21 (+6.9 мин) UI campaign {"case":7,"width":1440,"size":10,"seed":"Latin","addRows":4,"allRows":4,"reloadRows":4,"deleteRows":3,"documentWidth":1440,"searchRows":[1,0,1]}
- 15:32:52 (+7.4 мин) UI campaign {"case":10,"width":375,"size":10,"seed":"Latin","addRows":4,"allRows":4,"reloadRows":4,"deleteRows":3,"documentWidth":375,"searchRows":[1,0,1]}
- 15:33:23 (+7.9 мин) UI campaign {"case":13,"width":1440,"size":50,"seed":"Latin","addRows":4,"allRows":4,"reloadRows":4,"deleteRows":3,"documentWidth":1483,"searchRows":[1,0,1]}
- 15:33:37 (+8.2 мин) Хэрэгслийн issue: read-only monitor дахь Node fetch Response.status-ийг метод мэт дуудсан TypeError илрэв. Энэ нь аппын согог биш; өмнөх JSONL бичлэгийг хэвээр хадгалж, monitor-ийг засаж restart хийв. Browser HTTP/rows хэмжилтүүд байсан ч эхний stats талбарууд дутуу. Үндсэн UI campaign зогсоогүй.
- 15:33:54 (+8.5 мин) UI campaign {"case":16,"width":375,"size":50,"seed":"Latin","addRows":4,"allRows":4,"reloadRows":4,"deleteRows":3,"documentWidth":1092,"searchRows":[1,0,1]}
- 15:34:26 (+9.0 мин) UI campaign {"case":19,"width":1440,"size":100,"seed":"Latin","addRows":4,"allRows":4,"reloadRows":4,"deleteRows":3,"documentWidth":2500,"searchRows":[1,0,1]}
- 15:34:43 (+9.3 мин) BUG-08: нэмэх товчны текст «Нэмэx»; сүүлийн тэмдэгт Latin x (U+0078), зөв Монгол «Нэмэх»-ийн Cyrillic х (U+0445) биш. Runtime DOM codepoint-ийг evidence/bug-08-label.json-д хадгалав. screenshot bug-08 нь анхны baseline-ийн өөрчлөлтгүй хуулбар; үсгийн энэ ялгаа харагдах байдлаараа төстэй ч шаардлага текст үсгийн алдаагүй байхыг заасан.
- 15:34:58 (+9.5 мин) UI campaign {"case":22,"width":375,"size":100,"seed":"Latin","addRows":4,"allRows":4,"reloadRows":4,"deleteRows":3,"documentWidth":2009,"searchRows":[1,0,1]}
- 15:35:29 (+10.0 мин) UI campaign {"case":25,"width":1440,"size":200,"seed":"Latin","addRows":4,"allRows":4,"reloadRows":4,"deleteRows":3,"documentWidth":4533,"searchRows":[1,0,1]}
- 15:36:00 (+10.6 мин) UI campaign {"case":28,"width":375,"size":200,"seed":"Latin","addRows":4,"allRows":4,"reloadRows":4,"deleteRows":3,"documentWidth":3842,"searchRows":[1,0,1]}
- 15:36:32 (+11.1 мин) UI campaign {"case":31,"width":1440,"size":400,"seed":"Latin","addRows":4,"allRows":4,"reloadRows":4,"deleteRows":3,"documentWidth":8600,"searchRows":[1,0,1]}
- 15:37:05 (+11.6 мин) UI campaign {"case":34,"width":375,"size":400,"seed":"Latin","addRows":4,"allRows":4,"reloadRows":4,"deleteRows":3,"documentWidth":7507,"searchRows":[1,0,1]}
- 15:37:17 (+11.8 мин) Monitor の補足: SIGTERM 後も旧 monitor の catch loop が続き、新 monitor と同じファイルに書いて一部 JSONL が競合した。両方の自分の monitor を停止し、元ファイルを session-monitor-interrupted.jsonl として未変更で保存。新しい session-monitor.jsonl に分離して再開。アプリの障害として数えない。GUI campaign は継続。
- 15:37:34 (+12.1 мин) Өмнөх тэмдэглэлийн Монгол тайлбар: SIGTERM-ийн дараа хуучин monitor-ийн catch loop үргэлжилж шинэ monitor-той нэг файлд давхар бичсэн. Өөрийн хоёр monitor-ийг зогсоож, эх логийг session-monitor-interrupted.jsonl нэрээр өөрчлөлтгүй хадгалсан; тусдаа шинэ session-monitor.jsonl-д дахин эхлүүлсэн. Аппын алдаа биш; үндсэн GUI campaign тасраагүй.
- 15:37:37 (+12.2 мин) UI campaign {"case":37,"width":1440,"size":1,"seed":"Монгол","addRows":4,"allRows":4,"reloadRows":4,"deleteRows":3,"documentWidth":1440,"searchRows":[1,0,1]}
- 15:38:09 (+12.7 мин) UI campaign {"case":40,"width":375,"size":1,"seed":"Монгол","addRows":4,"allRows":4,"reloadRows":4,"deleteRows":3,"documentWidth":375,"searchRows":[1,0,1]}
- 15:38:40 (+13.2 мин) UI campaign {"case":43,"width":1440,"size":10,"seed":"Монгол","addRows":4,"allRows":4,"reloadRows":4,"deleteRows":3,"documentWidth":1440,"searchRows":[1,0,1]}
- 15:39:11 (+13.7 мин) UI campaign {"case":46,"width":375,"size":10,"seed":"Монгол","addRows":4,"allRows":4,"reloadRows":4,"deleteRows":3,"documentWidth":375,"searchRows":[1,0,1]}
- 15:39:43 (+14.3 мин) UI campaign {"case":49,"width":1440,"size":50,"seed":"Монгол","addRows":4,"allRows":4,"reloadRows":4,"deleteRows":3,"documentWidth":1483,"searchRows":[1,0,1]}
- 15:40:14 (+14.8 мин) UI campaign {"case":52,"width":375,"size":50,"seed":"Монгол","addRows":4,"allRows":4,"reloadRows":4,"deleteRows":3,"documentWidth":1092,"searchRows":[1,0,1]}
- 15:40:45 (+15.3 мин) UI campaign {"case":55,"width":1440,"size":100,"seed":"Монгол","addRows":4,"allRows":4,"reloadRows":4,"deleteRows":3,"documentWidth":2500,"searchRows":[1,0,1]}
- 15:41:03 (+15.6 мин) Supermodel нэмэлт read-only хайлт: тусдаа браузер context-д seed номуудыг үг/бүтэн нэр/зохиолч, тусгай тэмдэгт, regex-төст оролт, урт хайлтаар шалгаж эхлэв. Үндсэн campaign-ийн өгөгдлийг өөрчлөхгүй. Monitor-ийн connection refused/fetch failed нь campaign-ийн зориудын процесс restart-тай давхацдаг; тусдаа availability согог гэж дүгнээгүй.
- 15:41:17 (+15.8 мин) UI campaign {"case":58,"width":375,"size":100,"seed":"Монгол","addRows":4,"allRows":4,"reloadRows":4,"deleteRows":3,"documentWidth":2009,"searchRows":[1,0,1]}
- 15:41:48 (+16.4 мин) UI campaign {"case":61,"width":1440,"size":200,"seed":"Монгол","addRows":4,"allRows":4,"reloadRows":4,"deleteRows":3,"documentWidth":4533,"searchRows":[1,0,1]}
- 15:42:16 (+16.8 мин) Тусдаа read-only хайлтын 24 probe дуусав: JavaScript pageerror 0. Clean Code/Robert C. Martin/Тунгалаг Тамир/Ч.Лодойдамба тус бүр seed мөрөө олсон; & нь D.Thomas & A.Hunt-ыг олсон; regex-төст болон 1000 A тэмдэгттэй хайлт 0 мөртэй, browser алдаагүй. CODE нь 0 мөр — BUG-06-ийн хувилбар. evidence/search-special-characters.json хадгалагдав.
- 15:42:19 (+16.9 мин) UI campaign {"case":64,"width":375,"size":200,"seed":"Монгол","addRows":4,"allRows":4,"reloadRows":4,"deleteRows":3,"documentWidth":3842,"searchRows":[1,0,1]}
- 15:42:50 (+17.4 мин) UI campaign {"case":67,"width":1440,"size":400,"seed":"Монгол","addRows":4,"allRows":4,"reloadRows":4,"deleteRows":3,"documentWidth":8600,"searchRows":[1,0,1]}
- 15:43:22 (+17.9 мин) UI campaign {"case":70,"width":375,"size":400,"seed":"Монгол","addRows":4,"allRows":4,"reloadRows":4,"deleteRows":3,"documentWidth":7507,"searchRows":[1,0,1]}
- 15:43:53 (+18.4 мин) UI campaign {"case":73,"width":1440,"size":1,"seed":"日本語","addRows":4,"allRows":4,"reloadRows":4,"deleteRows":3,"documentWidth":1440,"searchRows":[1,0,1]}
- 15:44:14 (+18.8 мин) Дараагийн Couch Potato campaign-ийг үндсэн browser driver-ийн дараалалд оруулав; Supermodel-ийн 20 минутын хил дээр дуусмагц хоосон/оны/давхардлын шалгалт шууд эхэлнэ. API Saboteur-ийг 35 дахь минутаас эхлүүлэхээр төлөвлөсөн хэвээр.
- 15:44:24 (+19.0 мин) UI campaign {"case":76,"width":375,"size":1,"seed":"日本語","addRows":4,"allRows":4,"reloadRows":4,"deleteRows":3,"documentWidth":375,"searchRows":[1,0,1]}
- 15:44:56 (+19.5 мин) UI campaign {"case":79,"width":1440,"size":10,"seed":"日本語","addRows":4,"allRows":4,"reloadRows":4,"deleteRows":3,"documentWidth":1440,"searchRows":[1,0,1]}
- 15:45:27 (+20.0 мин) UI campaign {"case":82,"width":375,"size":10,"seed":"日本語","addRows":4,"allRows":4,"reloadRows":4,"deleteRows":3,"documentWidth":375,"searchRows":[1,0,1]}
- 15:45:27 (+20.0 мин) Supermodel campaign дуусав: 82 шинэ төлөвөөс эхэлсэн бүрэн UI дараалал; дэлгэрэнгүй JSONL evidence-д.
- 15:45:27 (+20.0 мин) Couch Potato эхлэв: хоосон/зайтай талбар, 1000–2100 бүхэл оны хил ба формат, ижил гарчиг+зохиолчийн давхардлыг шинэ апп бүрээс UI-ээр шалгана. Хил доторх утгуудыг эерэг control болгон хамруулна.
- 15:45:34 (+20.1 мин) BUG-09 олдов: all-empty дутуу талбартай ном нэмэгдсэн; screenshot bug-09, first-observation хадгалав.
- 15:45:35 (+20.1 мин) Couch Potato {"case":1,"round":1,"kind":"required","name":"all-empty","year":"","accepted":true,"rows":4,"persistedRows":4,"candidate":"BUG-09"}
- 15:45:43 (+20.3 мин) Couch Potato {"case":2,"round":1,"kind":"required","name":"missing-title","year":"2020","accepted":true,"rows":4,"persistedRows":4,"candidate":"BUG-09"}
- 15:45:51 (+20.4 мин) Couch Potato {"case":3,"round":1,"kind":"required","name":"missing-author","year":"2020","accepted":true,"rows":4,"persistedRows":4,"candidate":"BUG-09"}
- 15:45:58 (+20.5 мин) Couch Potato {"case":4,"round":1,"kind":"required","name":"missing-year","year":"","accepted":true,"rows":4,"persistedRows":4,"candidate":"BUG-09"}
- 15:46:06 (+20.7 мин) Couch Potato {"case":5,"round":1,"kind":"required","name":"title-only","year":"","accepted":true,"rows":4,"persistedRows":4,"candidate":"BUG-09"}
- 15:46:14 (+20.8 мин) Couch Potato {"case":6,"round":1,"kind":"required","name":"author-only","year":"","accepted":true,"rows":4,"persistedRows":4,"candidate":"BUG-09"}
- 15:46:22 (+20.9 мин) Couch Potato {"case":7,"round":1,"kind":"required","name":"year-only","year":"2020","accepted":true,"rows":4,"persistedRows":4,"candidate":"BUG-09"}
- 15:46:30 (+21.1 мин) Couch Potato {"case":8,"round":1,"kind":"required","name":"blank-spaces","year":"   ","accepted":true,"rows":4,"persistedRows":4,"candidate":"BUG-09"}
- 15:46:38 (+21.2 мин) Couch Potato {"case":9,"round":1,"kind":"required","name":"blank-tabs","year":"\t","accepted":true,"rows":4,"persistedRows":4,"candidate":"BUG-09"}
- 15:46:45 (+21.3 мин) BUG-10 олдов: year="999" хүлээн авч Validation BookValidation Author999Устгах дүрслэв; screenshot bug-10.
- 15:46:46 (+21.3 мин) Couch Potato {"case":10,"round":1,"kind":"year","name":"year-\"999\"","year":"999","accepted":true,"rows":4,"persistedRows":4,"candidate":"BUG-10"}
- 15:47:10 (+21.7 мин) Couch Potato {"case":13,"round":1,"kind":"year","name":"year-\"1971\"","year":"1971","accepted":true,"rows":4,"persistedRows":4,"candidate":null}
- 15:47:33 (+22.1 мин) Couch Potato {"case":16,"round":1,"kind":"year","name":"year-\"2101\"","year":"2101","accepted":true,"rows":4,"persistedRows":4,"candidate":"BUG-10"}
- 15:47:49 (+22.4 мин) Couch Potato {"case":18,"round":1,"kind":"year","name":"year-\"-1\"","year":"-1","accepted":true,"rows":4,"persistedRows":4,"candidate":"BUG-10"}
- 15:47:57 (+22.5 мин) Couch Potato {"case":19,"round":1,"kind":"year","name":"year-\"2020.5\"","year":"2020.5","accepted":true,"rows":4,"persistedRows":4,"candidate":"BUG-10"}
- 15:48:05 (+22.6 мин) Couch Potato {"case":20,"round":1,"kind":"year","name":"year-\"2020abc\"","year":"2020abc","accepted":true,"rows":4,"persistedRows":4,"candidate":"BUG-10"}
- 15:48:13 (+22.8 мин) Couch Potato {"case":21,"round":1,"kind":"year","name":"year-\"abc\"","year":"abc","accepted":true,"rows":4,"persistedRows":4,"candidate":"BUG-10"}
- 15:48:21 (+22.9 мин) Couch Potato {"case":22,"round":1,"kind":"year","name":"year-\"1e3\"","year":"1e3","accepted":true,"rows":4,"persistedRows":4,"candidate":null}
- 15:48:45 (+23.3 мин) Couch Potato {"case":25,"round":1,"kind":"year","name":"year-\"Infinity\"","year":"Infinity","accepted":true,"rows":4,"persistedRows":4,"candidate":null}
- 15:49:09 (+23.7 мин) Couch Potato {"case":28,"round":1,"kind":"year","name":"year-\"02020\"","year":"02020","accepted":true,"rows":4,"persistedRows":4,"candidate":null}
- 15:49:32 (+24.1 мин) Couch Potato {"case":31,"round":1,"kind":"year","name":"year-\"-2020\"","year":"-2020","accepted":true,"rows":4,"persistedRows":4,"candidate":null}
- 15:49:56 (+24.5 мин) Couch Potato {"case":34,"round":1,"kind":"year","name":"year-\"٢٠٢٠\"","year":"٢٠٢٠","accepted":true,"rows":4,"persistedRows":4,"candidate":null}
- 15:50:11 (+24.7 мин) BUG-11 олдов: exact-seed ижил гарчиг+зохиолчтой ном дахин нэмэгдэв; screenshot bug-11.
- 15:50:12 (+24.7 мин) Couch Potato {"case":36,"round":1,"kind":"duplicate","name":"exact-seed","year":"2008","accepted":true,"rows":4,"persistedRows":4,"candidate":"BUG-11"}
- 15:50:17 (+24.8 мин) Оны нэмэлт ажиглалт: 999/2101/-1/2020.5 хадгалагдсан; abc болон 2020abc нь NaN, Infinity нь ∞ гэж дүрслэгдсэн. 1000/2100 хязгаарын зөв утгууд ч нэмэгдсэн. Энэ бүхнийг BUG-10-ийн хувилбар болгон нэгтгэнэ; тус бүрт шинэ дугаар үүсгэхгүй.
- 15:50:20 (+24.9 мин) Couch Potato {"case":37,"round":1,"kind":"duplicate","name":"same-title-author-new-year","year":"1999","accepted":true,"rows":4,"persistedRows":4,"candidate":"BUG-11"}
- 15:50:43 (+25.3 мин) Couch Potato {"case":40,"round":1,"kind":"duplicate","name":"mongolian-seed","year":"1971","accepted":true,"rows":4,"persistedRows":4,"candidate":"BUG-11"}
- 15:51:07 (+25.7 мин) Couch Potato {"case":43,"round":2,"kind":"required","name":"all-empty","year":"","accepted":true,"rows":4,"persistedRows":4,"candidate":"BUG-09"}
- 15:51:15 (+25.8 мин) Couch Potato {"case":44,"round":2,"kind":"required","name":"missing-title","year":"2020","accepted":true,"rows":4,"persistedRows":4,"candidate":"BUG-09"}
- 15:51:23 (+25.9 мин) Couch Potato {"case":45,"round":2,"kind":"required","name":"missing-author","year":"2020","accepted":true,"rows":4,"persistedRows":4,"candidate":"BUG-09"}
- 15:51:31 (+26.1 мин) Couch Potato {"case":46,"round":2,"kind":"required","name":"missing-year","year":"","accepted":true,"rows":4,"persistedRows":4,"candidate":"BUG-09"}
- 15:51:39 (+26.2 мин) Couch Potato {"case":47,"round":2,"kind":"required","name":"title-only","year":"","accepted":true,"rows":4,"persistedRows":4,"candidate":"BUG-09"}
- 15:51:47 (+26.3 мин) Couch Potato {"case":48,"round":2,"kind":"required","name":"author-only","year":"","accepted":true,"rows":4,"persistedRows":4,"candidate":"BUG-09"}
- 15:51:55 (+26.5 мин) Couch Potato {"case":49,"round":2,"kind":"required","name":"year-only","year":"2020","accepted":true,"rows":4,"persistedRows":4,"candidate":"BUG-09"}
- 15:52:02 (+26.6 мин) Couch Potato {"case":50,"round":2,"kind":"required","name":"blank-spaces","year":"   ","accepted":true,"rows":4,"persistedRows":4,"candidate":"BUG-09"}
- 15:52:10 (+26.7 мин) Couch Potato {"case":51,"round":2,"kind":"required","name":"blank-tabs","year":"\t","accepted":true,"rows":4,"persistedRows":4,"candidate":"BUG-09"}
- 15:52:18 (+26.9 мин) Couch Potato {"case":52,"round":2,"kind":"year","name":"year-\"999\"","year":"999","accepted":true,"rows":4,"persistedRows":4,"candidate":"BUG-10"}
- 15:52:42 (+27.2 мин) Couch Potato {"case":55,"round":2,"kind":"year","name":"year-\"1971\"","year":"1971","accepted":true,"rows":4,"persistedRows":4,"candidate":null}
- 15:53:05 (+27.6 мин) Couch Potato {"case":58,"round":2,"kind":"year","name":"year-\"2101\"","year":"2101","accepted":true,"rows":4,"persistedRows":4,"candidate":"BUG-10"}
- 15:53:21 (+27.9 мин) Couch Potato {"case":60,"round":2,"kind":"year","name":"year-\"-1\"","year":"-1","accepted":true,"rows":4,"persistedRows":4,"candidate":"BUG-10"}
- 15:53:29 (+28.0 мин) Couch Potato {"case":61,"round":2,"kind":"year","name":"year-\"2020.5\"","year":"2020.5","accepted":true,"rows":4,"persistedRows":4,"candidate":"BUG-10"}
- 15:53:38 (+28.2 мин) Couch Potato {"case":62,"round":2,"kind":"year","name":"year-\"2020abc\"","year":"2020abc","accepted":true,"rows":4,"persistedRows":4,"candidate":"BUG-10"}
- 15:53:46 (+28.3 мин) Couch Potato {"case":63,"round":2,"kind":"year","name":"year-\"abc\"","year":"abc","accepted":true,"rows":4,"persistedRows":4,"candidate":"BUG-10"}
- 15:53:54 (+28.4 мин) Couch Potato {"case":64,"round":2,"kind":"year","name":"year-\"1e3\"","year":"1e3","accepted":true,"rows":4,"persistedRows":4,"candidate":null}
- 15:54:17 (+28.8 мин) Couch Potato {"case":67,"round":2,"kind":"year","name":"year-\"Infinity\"","year":"Infinity","accepted":true,"rows":4,"persistedRows":4,"candidate":null}
- 15:54:41 (+29.2 мин) Couch Potato {"case":70,"round":2,"kind":"year","name":"year-\"02020\"","year":"02020","accepted":true,"rows":4,"persistedRows":4,"candidate":null}
- 15:55:05 (+29.6 мин) Couch Potato {"case":73,"round":2,"kind":"year","name":"year-\"-2020\"","year":"-2020","accepted":true,"rows":4,"persistedRows":4,"candidate":null}
- 15:55:29 (+30.0 мин) Couch Potato {"case":76,"round":2,"kind":"year","name":"year-\"٢٠٢٠\"","year":"٢٠٢٠","accepted":true,"rows":4,"persistedRows":4,"candidate":null}
- 15:55:32 (+30.1 мин) 30 минутын checkpoint: session үргэлжилж байна; энэ мөчид түүхий тэмдэглэл, орчны мэдээлэл болон эхний campaign-уудын snapshot-ийг тусдаа git commit, push хийж ажлын явцыг хадгалж байна. API Saboteur болон эцсийн replay хараахан гүйцээгүй; энэ нь дууссан session report биш.
- 15:55:45 (+30.3 мин) Couch Potato {"case":78,"round":2,"kind":"duplicate","name":"exact-seed","year":"2008","accepted":true,"rows":4,"persistedRows":4,"candidate":"BUG-11"}
- 15:55:53 (+30.4 мин) Couch Potato {"case":79,"round":2,"kind":"duplicate","name":"same-title-author-new-year","year":"1999","accepted":true,"rows":4,"persistedRows":4,"candidate":"BUG-11"}
- 15:56:17 (+30.8 мин) Couch Potato {"case":82,"round":2,"kind":"duplicate","name":"mongolian-seed","year":"1971","accepted":true,"rows":4,"persistedRows":4,"candidate":"BUG-11"}
- 15:56:41 (+31.2 мин) Couch Potato {"case":85,"round":3,"kind":"required","name":"all-empty","year":"","accepted":true,"rows":4,"persistedRows":4,"candidate":"BUG-09"}
- 15:56:49 (+31.4 мин) Couch Potato {"case":86,"round":3,"kind":"required","name":"missing-title","year":"2020","accepted":true,"rows":4,"persistedRows":4,"candidate":"BUG-09"}
- 15:56:57 (+31.5 мин) Couch Potato {"case":87,"round":3,"kind":"required","name":"missing-author","year":"2020","accepted":true,"rows":4,"persistedRows":4,"candidate":"BUG-09"}
- 15:57:05 (+31.6 мин) Couch Potato {"case":88,"round":3,"kind":"required","name":"missing-year","year":"","accepted":true,"rows":4,"persistedRows":4,"candidate":"BUG-09"}
- 15:57:13 (+31.8 мин) Couch Potato {"case":89,"round":3,"kind":"required","name":"title-only","year":"","accepted":true,"rows":4,"persistedRows":4,"candidate":"BUG-09"}
- 15:57:21 (+31.9 мин) Couch Potato {"case":90,"round":3,"kind":"required","name":"author-only","year":"","accepted":true,"rows":4,"persistedRows":4,"candidate":"BUG-09"}
- 15:57:29 (+32.0 мин) Couch Potato {"case":91,"round":3,"kind":"required","name":"year-only","year":"2020","accepted":true,"rows":4,"persistedRows":4,"candidate":"BUG-09"}
- 15:57:37 (+32.2 мин) Couch Potato {"case":92,"round":3,"kind":"required","name":"blank-spaces","year":"   ","accepted":true,"rows":4,"persistedRows":4,"candidate":"BUG-09"}
- 15:57:45 (+32.3 мин) Couch Potato {"case":93,"round":3,"kind":"required","name":"blank-tabs","year":"\t","accepted":true,"rows":4,"persistedRows":4,"candidate":"BUG-09"}
- 15:57:53 (+32.4 мин) Couch Potato {"case":94,"round":3,"kind":"year","name":"year-\"999\"","year":"999","accepted":true,"rows":4,"persistedRows":4,"candidate":"BUG-10"}
- 15:58:17 (+32.8 мин) Couch Potato {"case":97,"round":3,"kind":"year","name":"year-\"1971\"","year":"1971","accepted":true,"rows":4,"persistedRows":4,"candidate":null}
- 15:58:41 (+33.2 мин) Couch Potato {"case":100,"round":3,"kind":"year","name":"year-\"2101\"","year":"2101","accepted":true,"rows":4,"persistedRows":4,"candidate":"BUG-10"}
- 15:58:57 (+33.5 мин) Couch Potato {"case":102,"round":3,"kind":"year","name":"year-\"-1\"","year":"-1","accepted":true,"rows":4,"persistedRows":4,"candidate":"BUG-10"}
- 15:59:05 (+33.6 мин) Couch Potato {"case":103,"round":3,"kind":"year","name":"year-\"2020.5\"","year":"2020.5","accepted":true,"rows":4,"persistedRows":4,"candidate":"BUG-10"}
- 15:59:13 (+33.8 мин) Couch Potato {"case":104,"round":3,"kind":"year","name":"year-\"2020abc\"","year":"2020abc","accepted":true,"rows":4,"persistedRows":4,"candidate":"BUG-10"}
- 15:59:21 (+33.9 мин) Couch Potato {"case":105,"round":3,"kind":"year","name":"year-\"abc\"","year":"abc","accepted":true,"rows":4,"persistedRows":4,"candidate":"BUG-10"}
- 15:59:29 (+34.0 мин) Couch Potato {"case":106,"round":3,"kind":"year","name":"year-\"1e3\"","year":"1e3","accepted":true,"rows":4,"persistedRows":4,"candidate":null}
- 15:59:53 (+34.4 мин) Couch Potato {"case":109,"round":3,"kind":"year","name":"year-\"Infinity\"","year":"Infinity","accepted":true,"rows":4,"persistedRows":4,"candidate":null}
- 16:00:17 (+34.8 мин) Couch Potato {"case":112,"round":3,"kind":"year","name":"year-\"02020\"","year":"02020","accepted":true,"rows":4,"persistedRows":4,"candidate":null}
- 16:00:33 (+35.1 мин) Couch Potato campaign дуусав: 114 шинэ төлөвөөс эхэлсэн UI туршилт; давталтын нийт тоо ба нэрлэсэн кейсүүд JSONL-д.
- 16:00:33 (+35.1 мин) Saboteur эхлэв: curl -i ашиглан буруу JSON, зөв JSON control, дутуу талбар, оны төрөл/хязгаар, давхардал, Unicode, HTML-төст текст шалгана. Бүх хүсэлт шинэ процессын анхны 3 номоос; бүтэн HTTP хариу JSONL болон анхны кейс бүрийн текст файлд хадгална.
- 16:00:34 (+35.1 мин) BUG-12 олдов: malformed-text буруу JSON-д HTTP 200 буцав, 400 биш. Бүтэн curl -i гаралт bug-12-curl.txt-д хадгалав.
- 16:00:40 (+35.2 мин) Saboteur {"case":1,"round":1,"name":"malformed-text","http":200,"exit":0,"malformed":true,"candidate":"BUG-12","rows":3,"renderError":null}
- 16:00:48 (+35.3 мин) Saboteur {"case":2,"round":1,"name":"malformed-open-brace","http":200,"exit":0,"malformed":true,"candidate":"BUG-12","rows":3,"renderError":null}
- 16:00:55 (+35.5 мин) Saboteur {"case":3,"round":1,"name":"malformed-trailing-comma","http":200,"exit":0,"malformed":true,"candidate":"BUG-12","rows":3,"renderError":null}
- 16:01:02 (+35.6 мин) Saboteur {"case":4,"round":1,"name":"malformed-single-quotes","http":200,"exit":0,"malformed":true,"candidate":"BUG-12","rows":3,"renderError":null}
- 16:01:09 (+35.7 мин) Saboteur {"case":5,"round":1,"name":"malformed-empty-body","http":201,"exit":0,"malformed":true,"candidate":"BUG-12","rows":4,"renderError":null}
- 16:01:24 (+35.9 мин) Saboteur {"case":7,"round":1,"name":"missing-all-fields","http":201,"exit":0,"malformed":false,"candidate":null,"rows":4,"renderError":null}
- 16:01:45 (+36.3 мин) Saboteur {"case":10,"round":1,"name":"string-root","http":201,"exit":0,"malformed":false,"candidate":null,"rows":4,"renderError":null}
- 16:02:07 (+36.7 мин) Saboteur {"case":13,"round":1,"name":"year-under-bound","http":201,"exit":0,"malformed":false,"candidate":null,"rows":4,"renderError":null}
- 16:02:29 (+37.0 мин) Saboteur {"case":16,"round":1,"name":"year-over-bound","http":201,"exit":0,"malformed":false,"candidate":null,"rows":4,"renderError":null}
- 16:02:51 (+37.4 мин) Saboteur {"case":19,"round":1,"name":"year-object","http":201,"exit":0,"malformed":false,"candidate":null,"rows":4,"renderError":null}
- 16:03:13 (+37.8 мин) Saboteur {"case":22,"round":1,"name":"html-text","http":201,"exit":0,"malformed":false,"candidate":null,"rows":4,"renderError":null}
- 16:03:35 (+38.1 мин) Saboteur {"case":25,"round":2,"name":"malformed-text","http":200,"exit":0,"malformed":true,"candidate":"BUG-12","rows":3,"renderError":null}
- 16:03:43 (+38.3 мин) Saboteur {"case":26,"round":2,"name":"malformed-open-brace","http":200,"exit":0,"malformed":true,"candidate":"BUG-12","rows":3,"renderError":null}
- 16:03:50 (+38.4 мин) Saboteur {"case":27,"round":2,"name":"malformed-trailing-comma","http":200,"exit":0,"malformed":true,"candidate":"BUG-12","rows":3,"renderError":null}
- 16:03:57 (+38.5 мин) Saboteur {"case":28,"round":2,"name":"malformed-single-quotes","http":200,"exit":0,"malformed":true,"candidate":"BUG-12","rows":3,"renderError":null}
- 16:04:05 (+38.6 мин) Saboteur {"case":29,"round":2,"name":"malformed-empty-body","http":201,"exit":0,"malformed":true,"candidate":"BUG-12","rows":4,"renderError":null}
- 16:04:19 (+38.9 мин) Saboteur {"case":31,"round":2,"name":"missing-all-fields","http":201,"exit":0,"malformed":false,"candidate":null,"rows":4,"renderError":null}
- 16:04:40 (+39.2 мин) Saboteur {"case":34,"round":2,"name":"string-root","http":201,"exit":0,"malformed":false,"candidate":null,"rows":4,"renderError":null}
- 16:05:02 (+39.6 мин) Saboteur {"case":37,"round":2,"name":"year-under-bound","http":201,"exit":0,"malformed":false,"candidate":null,"rows":4,"renderError":null}
- 16:05:24 (+39.9 мин) Saboteur {"case":40,"round":2,"name":"year-over-bound","http":201,"exit":0,"malformed":false,"candidate":null,"rows":4,"renderError":null}
- 16:05:45 (+40.3 мин) Saboteur {"case":43,"round":2,"name":"year-object","http":201,"exit":0,"malformed":false,"candidate":null,"rows":4,"renderError":null}
- 16:06:07 (+40.7 мин) Saboteur {"case":46,"round":2,"name":"html-text","http":201,"exit":0,"malformed":false,"candidate":null,"rows":4,"renderError":null}
- 16:06:29 (+41.0 мин) Saboteur {"case":49,"round":3,"name":"malformed-text","http":200,"exit":0,"malformed":true,"candidate":"BUG-12","rows":3,"renderError":null}
- 16:06:36 (+41.2 мин) Saboteur {"case":50,"round":3,"name":"malformed-open-brace","http":200,"exit":0,"malformed":true,"candidate":"BUG-12","rows":3,"renderError":null}
- 16:06:44 (+41.3 мин) Saboteur {"case":51,"round":3,"name":"malformed-trailing-comma","http":200,"exit":0,"malformed":true,"candidate":"BUG-12","rows":3,"renderError":null}
- 16:06:51 (+41.4 мин) Saboteur {"case":52,"round":3,"name":"malformed-single-quotes","http":200,"exit":0,"malformed":true,"candidate":"BUG-12","rows":3,"renderError":null}
- 16:06:58 (+41.5 мин) Saboteur {"case":53,"round":3,"name":"malformed-empty-body","http":201,"exit":0,"malformed":true,"candidate":"BUG-12","rows":4,"renderError":null}
- 16:07:12 (+41.8 мин) Saboteur {"case":55,"round":3,"name":"missing-all-fields","http":201,"exit":0,"malformed":false,"candidate":null,"rows":4,"renderError":null}
- 16:07:34 (+42.1 мин) Saboteur {"case":58,"round":3,"name":"string-root","http":201,"exit":0,"malformed":false,"candidate":null,"rows":4,"renderError":null}
- 16:07:56 (+42.5 мин) Saboteur {"case":61,"round":3,"name":"year-under-bound","http":201,"exit":0,"malformed":false,"candidate":null,"rows":4,"renderError":null}
- 16:08:17 (+42.8 мин) Saboteur {"case":64,"round":3,"name":"year-over-bound","http":201,"exit":0,"malformed":false,"candidate":null,"rows":4,"renderError":null}
- 16:08:39 (+43.2 мин) Saboteur {"case":67,"round":3,"name":"year-object","http":201,"exit":0,"malformed":false,"candidate":null,"rows":4,"renderError":null}
- 16:09:01 (+43.6 мин) Saboteur {"case":70,"round":3,"name":"html-text","http":201,"exit":0,"malformed":false,"candidate":null,"rows":4,"renderError":null}
- 16:09:23 (+43.9 мин) Saboteur {"case":73,"round":4,"name":"malformed-text","http":200,"exit":0,"malformed":true,"candidate":"BUG-12","rows":3,"renderError":null}
- 16:09:30 (+44.1 мин) Saboteur {"case":74,"round":4,"name":"malformed-open-brace","http":200,"exit":0,"malformed":true,"candidate":"BUG-12","rows":3,"renderError":null}
- 16:09:37 (+44.2 мин) Saboteur {"case":75,"round":4,"name":"malformed-trailing-comma","http":200,"exit":0,"malformed":true,"candidate":"BUG-12","rows":3,"renderError":null}
- 16:09:45 (+44.3 мин) Saboteur {"case":76,"round":4,"name":"malformed-single-quotes","http":200,"exit":0,"malformed":true,"candidate":"BUG-12","rows":3,"renderError":null}
- 16:09:52 (+44.4 мин) Saboteur {"case":77,"round":4,"name":"malformed-empty-body","http":201,"exit":0,"malformed":true,"candidate":"BUG-12","rows":4,"renderError":null}
- 16:10:02 (+44.6 мин) Хэрэглэгчийн шинэ заавар: эвдэлж болзошгүй API хандалтгүйгээр үргэлжлүүлж дуусгах. Saboteur-ийн үлдсэн campaign-ийг шууд зогсоож, өөрийн driver/app процессыг хаав. Өмнөх нотолгоог хадгална; цааш буруу JSON/type зэрэг API probe дахин илгээхгүй, үлдсэн session-ийг хэвийн UI үйлдлээр үргэлжлүүлнэ. Charter-ийн API хамралтыг энэ заавраар хязгаарлав.
- 16:11:03 (+45.6 мин) Шинэ UI-only driver болон зөвхөн хуудас ажиглах monitor эхлэв; шууд API stats GET-ийг ч monitor-оос хасав. Зогсоох хүртэл 78 API probe (24 нэрлэсэн оролт) дууссан; цааш API replay хийхгүй. Анхны session эхлэх/дуусах хугацааг өөрчлөөгүй.
- 16:11:29 (+46.0 мин) Хэрэглэгчийн шинэ хязгаарлалтаар UI-only campaign: хүчинтэй ном, keyboard Enter, Unicode/emoji/combining, зохиолчоор хайх, Бүгд, reload, хэвийн устгах. Шууд API хүсэлтгүй.
- 16:11:40 (+46.2 мин) UI-only {"case":1,"title":"Монгол ном 📚","keyboardEnter":false,"addRows":4,"searchCounts":[1,1,0,0],"allRows":4,"reloadRows":4,"deletedRows":3}
- 16:11:54 (+46.5 мин) Өмнөх хадгалсан API логийг сүлжээний хүсэлтгүйгээр шалгав: null root JSON нь 16:01:30 / 16:04:26 / 16:07:19 ажиглалтад curl 52 Empty reply, дараагийн GET curl 7, UI ERR_CONNECTION_REFUSED үүсгэсэн. Үүнийг BUG-13 сервер хүрэх боломжгүй болох тусдаа зөрчил гэж тэмдэглэж, өмнөх raw нотолгоог bug-13 файлуудад архивлав. Шинээр давтахгүй; хэрэглэгчийн хязгаарлалт хүчинтэй.
- 16:12:12 (+46.8 мин) UI-only {"case":4,"title":"日本語の本","keyboardEnter":true,"addRows":3,"searchCounts":[0,0,0,0],"allRows":3,"reloadRows":3,"deletedRows":3}
- 16:12:45 (+47.3 мин) UI-only {"case":7,"title":"Book with spaces","keyboardEnter":false,"addRows":4,"searchCounts":[1,1,0,0],"allRows":4,"reloadRows":4,"deletedRows":3}
- 16:13:14 (+47.8 мин) UI-only нэмэлт ажиглалт: оны input дотор Enter дарахад ном нэмэгдэхгүй (even кейсүүдэд 3 мөр хэвээр), товч дарсан odd кейсүүдэд 4 мөр болж байна. Input-оос implicit submit нь өгсөн спецификацид заагаагүй тул одоогоор тусдаа баталсан согог гэж тооцохгүй. Эцсийн UI replay-д нэмэх товчийг focus хийгээд Enter дарах keyboard activation-ийг тусад нь шалгана.
- 16:13:17 (+47.8 мин) UI-only {"case":10,"title":"Emoji 😀📖","keyboardEnter":true,"addRows":3,"searchCounts":[0,0,0,0],"allRows":3,"reloadRows":3,"deletedRows":3}
- 16:13:49 (+48.4 мин) UI-only {"case":13,"title":"Кирилл ба Latin","keyboardEnter":false,"addRows":4,"searchCounts":[1,1,0,0],"allRows":4,"reloadRows":4,"deletedRows":3}
- 16:14:21 (+48.9 мин) UI-only {"case":16,"title":"Нэг тэмдэг А","keyboardEnter":true,"addRows":3,"searchCounts":[0,0,0,1],"allRows":3,"reloadRows":3,"deletedRows":3}
- 16:14:54 (+49.5 мин) UI-only {"case":19,"title":"Café","keyboardEnter":false,"addRows":4,"searchCounts":[1,1,0,0],"allRows":4,"reloadRows":4,"deletedRows":3}
- 16:15:26 (+50.0 мин) UI-only {"case":22,"title":"Ном — урт зураас","keyboardEnter":true,"addRows":3,"searchCounts":[0,0,0,0],"allRows":3,"reloadRows":3,"deletedRows":3}
- 16:15:59 (+50.5 мин) UI-only {"case":25,"title":"Монгол ном 📚","keyboardEnter":false,"addRows":4,"searchCounts":[1,1,0,0],"allRows":4,"reloadRows":4,"deletedRows":3}
- 16:16:31 (+51.1 мин) UI-only {"case":28,"title":"日本語の本","keyboardEnter":true,"addRows":3,"searchCounts":[0,0,0,0],"allRows":3,"reloadRows":3,"deletedRows":3}
- 16:17:03 (+51.6 мин) UI-only {"case":31,"title":"Book with spaces","keyboardEnter":false,"addRows":4,"searchCounts":[1,1,0,0],"allRows":4,"reloadRows":4,"deletedRows":3}
- 16:17:20 (+51.9 мин) UI-only товчоор илгээсэн эерэг хяналтууд: нэмэхэд 4 мөр, reload-д 4 мөр, устгасны дараа 3 мөр; шинэ API probe хийгээгүй. Input-Enter кейсийг button activation control-оос ялгаж тайлагнана. Session төгсөх 16:25:27 цаг хэвээр.
- 16:17:36 (+52.2 мин) UI-only {"case":34,"title":"Emoji 😀📖","keyboardEnter":true,"addRows":3,"searchCounts":[0,0,0,0],"allRows":3,"reloadRows":3,"deletedRows":3}
- 16:18:08 (+52.7 мин) UI-only {"case":37,"title":"Кирилл ба Latin","keyboardEnter":false,"addRows":4,"searchCounts":[1,1,0,0],"allRows":4,"reloadRows":4,"deletedRows":3}
- 16:18:41 (+53.2 мин) UI-only {"case":40,"title":"Нэг тэмдэг А","keyboardEnter":true,"addRows":3,"searchCounts":[0,0,0,1],"allRows":3,"reloadRows":3,"deletedRows":3}
- 16:19:13 (+53.8 мин) UI-only {"case":43,"title":"Café","keyboardEnter":false,"addRows":4,"searchCounts":[1,1,0,0],"allRows":4,"reloadRows":4,"deletedRows":3}
- 16:19:45 (+54.3 мин) UI-only {"case":46,"title":"Ном — урт зураас","keyboardEnter":true,"addRows":3,"searchCounts":[0,0,0,0],"allRows":3,"reloadRows":3,"deletedRows":3}
- 16:20:18 (+54.9 мин) UI-only {"case":49,"title":"Монгол ном 📚","keyboardEnter":false,"addRows":4,"searchCounts":[1,1,0,0],"allRows":4,"reloadRows":4,"deletedRows":3}
- 16:20:29 (+55.0 мин) UI-only өргөтгөсөн campaign дуусав: 50 хэвийн хэрэглэгчийн дараалал. Эцсийн 5 минутын UI replay руу шилжинэ.
- 16:20:29 (+55.0 мин) Эцсийн UI replay эхлэв. BUG-01–11-ийн хэрэглэгчийн алхмыг шинэ төлөвөөс батална; API BUG-12/13-ийг хэрэглэгчийн заавраар дахин ажиллуулахгүй. Expected-defect predicates нь апп зөв гэсэн утга биш, баримтжуулсан зөрчил давтагдсаныг шалгана.
- 16:20:40 (+55.2 мин) UI replay 1: 11/11 баримтжуулсан UI зөрчил давтагдав; keyboard товчийн Enter activation true. API хүсэлт гар аргаар илгээгээгүй.
- 16:20:51 (+55.4 мин) UI replay 2: 11/11 баримтжуулсан UI зөрчил давтагдав; keyboard товчийн Enter activation true. API хүсэлт гар аргаар илгээгээгүй.
- 16:21:02 (+55.6 мин) UI replay 3: 11/11 баримтжуулсан UI зөрчил давтагдав; keyboard товчийн Enter activation true. API хүсэлт гар аргаар илгээгээгүй.
- 16:21:13 (+55.8 мин) UI replay 4: 11/11 баримтжуулсан UI зөрчил давтагдав; keyboard товчийн Enter activation true. API хүсэлт гар аргаар илгээгээгүй.
- 16:21:24 (+56.0 мин) UI replay 5: 11/11 баримтжуулсан UI зөрчил давтагдав; keyboard товчийн Enter activation true. API хүсэлт гар аргаар илгээгээгүй.
- 16:21:35 (+56.1 мин) UI replay 6: 11/11 баримтжуулсан UI зөрчил давтагдав; keyboard товчийн Enter activation true. API хүсэлт гар аргаар илгээгээгүй.
- 16:21:46 (+56.3 мин) UI replay 7: 11/11 баримтжуулсан UI зөрчил давтагдав; keyboard товчийн Enter activation true. API хүсэлт гар аргаар илгээгээгүй.
- 16:21:57 (+56.5 мин) UI replay 8: 11/11 баримтжуулсан UI зөрчил давтагдав; keyboard товчийн Enter activation true. API хүсэлт гар аргаар илгээгээгүй.
- 16:22:08 (+56.7 мин) UI replay 9: 11/11 баримтжуулсан UI зөрчил давтагдав; keyboard товчийн Enter activation true. API хүсэлт гар аргаар илгээгээгүй.
- 16:22:21 (+56.9 мин) UI replay 10: 11/11 баримтжуулсан UI зөрчил давтагдав; keyboard товчийн Enter activation true. API хүсэлт гар аргаар илгээгээгүй.
- 16:22:31 (+57.1 мин) UI replay 11: 11/11 баримтжуулсан UI зөрчил давтагдав; keyboard товчийн Enter activation true. API хүсэлт гар аргаар илгээгээгүй.
- 16:22:42 (+57.3 мин) UI replay 12: 11/11 баримтжуулсан UI зөрчил давтагдав; keyboard товчийн Enter activation true. API хүсэлт гар аргаар илгээгээгүй.
- 16:22:53 (+57.4 мин) UI replay 13: 11/11 баримтжуулсан UI зөрчил давтагдав; keyboard товчийн Enter activation true. API хүсэлт гар аргаар илгээгээгүй.
- 16:23:04 (+57.6 мин) UI replay 14: 11/11 баримтжуулсан UI зөрчил давтагдав; keyboard товчийн Enter activation true. API хүсэлт гар аргаар илгээгээгүй.
- 16:23:15 (+57.8 мин) UI replay 15: 11/11 баримтжуулсан UI зөрчил давтагдав; keyboard товчийн Enter activation true. API хүсэлт гар аргаар илгээгээгүй.
- 16:23:26 (+58.0 мин) UI replay 16: 11/11 баримтжуулсан UI зөрчил давтагдав; keyboard товчийн Enter activation true. API хүсэлт гар аргаар илгээгээгүй.
- 16:23:38 (+58.2 мин) UI replay 17: 11/11 баримтжуулсан UI зөрчил давтагдав; keyboard товчийн Enter activation true. API хүсэлт гар аргаар илгээгээгүй.
- 16:23:49 (+58.4 мин) UI replay 18: 11/11 баримтжуулсан UI зөрчил давтагдав; keyboard товчийн Enter activation true. API хүсэлт гар аргаар илгээгээгүй.
- 16:24:02 (+58.6 мин) UI replay 19: 11/11 баримтжуулсан UI зөрчил давтагдав; keyboard товчийн Enter activation true. API хүсэлт гар аргаар илгээгээгүй.
- 16:24:13 (+58.8 мин) UI replay 20: 11/11 баримтжуулсан UI зөрчил давтагдав; keyboard товчийн Enter activation true. API хүсэлт гар аргаар илгээгээгүй.
- 16:24:24 (+58.9 мин) UI replay 21: 11/11 баримтжуулсан UI зөрчил давтагдав; keyboard товчийн Enter activation true. API хүсэлт гар аргаар илгээгээгүй.
- 16:24:34 (+59.1 мин) UI replay 22: 11/11 баримтжуулсан UI зөрчил давтагдав; keyboard товчийн Enter activation true. API хүсэлт гар аргаар илгээгээгүй.
- 16:24:46 (+59.3 мин) UI replay 23: 11/11 баримтжуулсан UI зөрчил давтагдав; keyboard товчийн Enter activation true. API хүсэлт гар аргаар илгээгээгүй.
- 16:24:56 (+59.5 мин) UI replay 24: 11/11 баримтжуулсан UI зөрчил давтагдав; keyboard товчийн Enter activation true. API хүсэлт гар аргаар илгээгээгүй.
- 16:25:08 (+59.7 мин) UI replay 25: 11/11 баримтжуулсан UI зөрчил давтагдав; keyboard товчийн Enter activation true. API хүсэлт гар аргаар илгээгээгүй.
- 16:25:27 (+60.0 мин) 60 минутын хугацааны хилд хүрэв. UI session дуусав; одоо тайлангийн цаг/саад/задаргааг нэгтгэж, дараа нь bug report болон debrief бичнэ.

## Саадууд (issues)

- Багшийн апп хүлээсэн болон Node хувилбар тааруулсан хугацаа session-ээс өмнө байсан; 60 минутад оруулаагүй.
- Эхний read-only monitor-д Node fetch-ийн `Response.status`-ийг метод мэт дуудсан хэрэгслийн алдаа гарсан. Дараах restart-д хуучин monitor үлдэж логийн зарим мөр давхар бичигдсэн. Эх файлыг `evidence/session-monitor-interrupted.jsonl` гэж өөрчлөлтгүй хадгалж, шинэ логт салгасан. Энэ нь аппын bug биш.
- Campaign-уудын зориудын app restart-тай давхацсан connection refused/fetch failed ажиглалтыг тусдаа аппын согог гэж тооцоогүй. Харин `null` JSON-ийн дараах, гурван удаагийн ижил унтарсан төлөв нь тусдаа хадгалсан curl нотолгоотой BUG-13.
- Хэрэглэгч session-ийн 44.6 дахь минутад эвдэлж болзошгүй API хандалтгүй үргэлжлүүлэхийг хүссэн. Үлдсэн Saboteur campaign-ийг зогсоож, шууд API уншилтыг monitor-оос ч хассан; үлдсэн хугацаанд зөвхөн UI ажилласан.
- API BUG-12/13-ийг энэ заавраас хойш дахин ажиллуулаагүй. Өмнөх session дотор шинэ процессоос олон удаа авсан raw нотолгоог ашигласан. Шинэ clone дээрх шалгалт мөн UI-ээр хязгаарлагдана.
- Талбар дотроос Enter дарах implicit submit нь спецификацид заагаагүй тул баталсан согогт тооцоогүй. Нэмэх товчийг focus хийгээд Enter дарах control бүх 25 replay тойрогт ажилласан.
- Firefox, бодит touch төхөөрөмж, дэлгэц уншигч, өндөр ачаалал болон олон зэрэгцээ хэрэглэгчийг энэ session-д шалгаагүй.

## Хамралт ба үр дүн

| Шалгалт | Бодит гүйцэтгэл | Үр дүнгийн утга |
| --- | --- | --- |
| Baseline дахин нээх | 30 | HTTP 200, 3 мөр; буруу тоолуур 4 тогтвортой |
| Supermodel UI дараалал | 82 | 320–1920 px, Latin/Монгол/Япон, урт гарчиг/зохиолч |
| Тусгай тэмдэгттэй хайлт | 24 | Browser pageerror 0; үсгийн хэмжээ ялгах зөрчил давтав |
| Couch Potato | 114, 42 өөр оролт | Хоосон талбар/он/давхардлын зөрчил; эерэг boundary control орсон |
| Saboteur | 78, 24 өөр оролт | Буруу JSON-ийн хуурамч success, null JSON-ийн дараах хүрэх боломжгүй төлөв; хэрэглэгчийн заавраар зогсоосон |
| Дараах UI-only дараалал | 50 | 25 click-submit хүчинтэй control ажилласан; 25 input-Enter ажиглалтыг тусад нь ялгасан |
| Эцсийн UI replay | 25 × 11 = 275 predicate | 11 баримтжуулсан UI зөрчил бүх 25 тойрогт давтагдсан |
| Keyboard button activation | 25 | Focus хийсэн нэмэх товчийг Enter-ээр идэвхжүүлэх control ажилласан |

275 predicate батлагдсан нь аппын 275 чанарын тест passed гэсэн үг биш: баримтжуулсан согог дахин гарсныг баталсан. Автомат test runner-ийн skipped/expected-failure тоог зохиож мэдээлээгүй. API дахин турших болон дээр дурдсан браузер/төхөөрөмжийн хамралт unrun хэвээр.

Нийт 13 өөр зөрчил: Supermodel BUG-01–08, Couch Potato BUG-09–11, Saboteur BUG-12–13. Хоосон талбарын хувилбаруудыг нэг, оны шалгалтын хувилбаруудыг нэг, буруу JSON-ийн хувилбаруудыг нэг согог болгон нэгтгэсэн.

## Цагийн задаргаа

Setup **10%** (ойролцоогоор 6 мин) · Тест дизайн ба гүйцэтгэл **65%** (39 мин) · Согог судлах **25%** (15 мин).

Энэ нь түүхий тэмдэглэл, setup/restart болон судлах үйлдлүүдэд тулгуурласан SBTM-ийн ойролцоо ангилал; үйлдэл бүрийн CPU хэмжилт биш. Нийт ханын цаг 60 минут бөгөөд тайлан/debrief бичих дараах хугацааг оруулаагүй.
