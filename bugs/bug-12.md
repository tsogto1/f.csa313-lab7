# BUG-12: Буруу JSON POST хүсэлтэд HTTP 400-ийн оронд 200 OK буцаана

Орчин: Уншлагын жагсаалт v2.0; Node.js v20.19.2; Chromium 154.0.8037.57 (headless); Debian GNU/Linux 13.6 x86_64; 2026-10-20; Asia/Ulaanbaatar. UI viewport 1440 × 1000, өөрөөр заагаагүй бол.

Урьдчилсан нөхцөл: Багшийн өөрчлөгдөөгүй app.js файлыг репозиторийн үндсэн хавтаст байрлуулсан. Өөрийн өмнөх app процессыг зогсоож, `node app.js`-ийг шинээр асаасан; анхны «Тунгалаг Тамир», «Clean Code», «The Pragmatic Programmer» гэсэн 3 номтой. UI-д `http://localhost:3000`-г нээнэ. Хэрэв Node-ийн олон хувилбартай бол `node -v` нь v20.19.2 гэдгийг эхлээд батална.

## Дахин гаргах алхам

1. Шинэ app.js процесс анхны 3 номтой ажиллаж байгааг батална.
2. Репозиторийн үндсэн хавтсаас доорх curl командыг илгээнэ. Request файлд JSON биш «буруу оролт» гэсэн UTF-8 текст байна.
3. HTTP статусын мөр болон response body-г шалгана.

Давтах команд (зөвхөн локал тестийн аппад; хэрэглэгчийн заавраас хойш бид дахин ажиллуулаагүй):

```sh
curl -sS --max-time 10 -i -X POST http://localhost:3000/api/books \
  -H 'Content-Type: application/json' \
  --data-binary @evidence/bug-12-request.txt
```

Хүлээгдэж байсан: «API: буруу JSON биетэй POST хүсэлтэд 400 алдаа буцаана»: HTTP 400, буруу оролтыг илэрхийлсэн хариу байна.

Бодит үр дүн: HTTP/1.1 200 OK болон `{"result":"OK"}` буцсан. Номын тоо 3 хэвээр байсан ч клиентэд амжилттай хариу өгсөн. Нээлттэй {, trailing comma, single-quote JSON хувилбарууд ч HTTP 200 буцаасан; бүгд нэг malformed-JSON согог. Нотолгоог хэрэглэгчийн API зогсоох заавраас ӨМНӨ цуглуулсан, түүнээс хойш болон шинэ clone дээр энэ хүсэлтийг дахин илгээгээгүй.

Ноцтой байдал: **Major — буруу хүсэлтийг API амжилттай мэт мэдээлж, клиент алдаагаа ялгах боломжгүй болгоно.**

## Хавсралт

- [bug-12-curl.txt](../evidence/bug-12-curl.txt)
- [bug-12-request.txt](../evidence/bug-12-request.txt)
- [bug-12-first-observation.json](../evidence/bug-12-first-observation.json)

- [Орчны мэдээлэл](../evidence/environment.json)
- [Session report](../session-report.md)

Олдсон аялал: **Saboteur**.
