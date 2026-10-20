# Нотолгооны тайлбар

- `environment.json`: бодитоор хэрэглэсэн хувилбарууд, багшийн аппын checksum, charter commit.
- `session-summary.json`: 60 минутын бодит эхлэх/дуусах цаг болон campaign бүрийн тоо.
- `bug-NN-curl.txt`: curl -i-ийн бүтэн stdout/stderr; HTTP хариу ирсэн тохиолдолд статусын мөртэй. `bug-12-curl.txt` нь `HTTP/1.1 200 OK` ба `{"result":"OK"}`-ийг агуулна.
- `bug-13-curl.txt`: HTTP хариу ирээгүй тул статусын мөр байхгүй, curl exit 52-ийн бүтэн алдаа; `bug-13-after-curl.txt` нь дараах connection failed алдаа. `bug-13-observations.json`-д session доторх 3 давталт бий.
- `bug-NN-request.*`: яг илгээсэн request body; нууц утга агуулаагүй.
- `*-campaign.jsonl`, `final-ui-replay.jsonl`: кейс бүрийн бодит цаг, оролт, DOM/HTTP ажиглалт. Нэг JSON object нь нэг мөр.
- `final-ui-replay.jsonl`-ийн `reproduced: true` нь **аппын согог давтагдсан** гэсэн утга, чанарын шаардлага passed биш.
- `ui-only-campaign.jsonl`-ийн even кейсүүд нь input дотор Enter дарах ажиглалт; odd кейсүүд нь товч дарсан эерэг control. Нэмэх товчийг focus хийгээд Enter дарах эерэг control нь final replay-д тусдаа бий.
- `session-monitor.jsonl`: үе үе read-only хуудас ажигласан лог; хэрэглэгчийн шинэ заавраас хойш шууд stats API уншилтгүй `mode: ui-only-after-user-request` бичлэгүүдтэй.
- `session-monitor-interrupted.jsonl`: monitor хэрэгслийн алдаа/давхар writer-тай эх логийг өөрчлөлтгүй хадгалсан архив; зарим мөр нь давхар бичигдсэн тул valid JSONL гэж parse хийхгүй, аппын test failure гэж тооцохгүй.
- `../screenshots/bug-01.png`–`bug-11.png`: бодит Chromium screenshot. BUG-08 нь baseline BUG-01 зургийн өөрчлөлтгүй хуулбар; Unicode ялгааг `bug-08-label.json` батална. BUG-07 full-page зураг нь 2709 px өргөн.

Хэрэглэгч API туршилтыг зогсоохыг хүссэнээс хойш шинэ API probe хийгээгүй. API-ийн хоёр тайлан өмнө бүртгэсэн raw нотолгоонд тулгуурлана.
