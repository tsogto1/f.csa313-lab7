# Session report

Тестер: Х.Цогтбаяр — B232270072; хүсэлтийн дагуу Codex AI агент браузер/API туршилтыг гүйцэтгэж, тэмдэглэл хөтөлсөн. Оюутан өөрөө гараар 60 минут тест хийсэн гэж тайлагнаагүй.

Огноо: 2026-10-20, эхэлсэн 15:25:27 (Asia/Ulaanbaatar, UTC+08:00).
Зорилтот дуусах цаг: 16:25:27; бодит дуусах цагийг session төгсөхөд бүртгэнэ.

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
