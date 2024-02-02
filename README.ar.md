# tg-بحث-بوت

<!-- ALL-CONTRIBUTORS-BADGE:START - Do not remove or modify this section -->

[![All Contributors](https://img.shields.io/badge/all_contributors-4-orange.svg?style=flat-square)](#contributors-)

<!-- ALL-CONTRIBUTORS-BADGE:END -->

**روبوت Telegram يمكن استخدامه للبحث عن روابط فيديو مغناطيسية متنوعة. وهو يدعم عمليات مثل التجميع وتصدير السجلات وحفظ الروابط المغناطيسية تلقائيًا. ويمكن تهيئته يدويًا لحظر محتوى NSFW والوصول إلى الإنترنت بالوكالة.**

تم تصميم الروبوت استنادًا إلى Python3، ويدعم النشر بنقرة واحدة باستخدام Docker، وينفذ وظائف التخزين المؤقت من خلال Redis.

## مقدمة الوظيفة

يتم فرز الوظائف التالية حسب وقت اكتمال التطوير، وسيتم إضافة وظائف جديدة بشكل مستمر في المستقبل.

-   يدعم الحصول على معلومات الفيديو الأساسية وروابط المغناطيس - 2022/11/25
-   دعم وكيل التكوين - 2022/11/26
-   دعم تصفية الروابط المغناطيسية (غير خاضعة للرقابة => hd => الترجمة) - 2022/11/26
-   دعم السماح للروبوتات بحفظ الروابط المغناطيسية المثالية إلى Pikpak تلقائيًا - 2022/12/29
-   支持获取预览视频和完整视频 - 2022/12/31
-   دعم الحصول على لقطات فيديو - 2023/01/01
-   دعم مجموعة الممثلين ومقاطع الفيديو - 2023/01/04
-   دعم النشر عبر عامل الإرساء - 2023/01/08
-   يدعم الحصول على تصنيفات الممثلين وتقييمات الأفلام - 2023/01/20
-   يدعم الوصول العشوائي إلى مقاطع الفيديو عالية الدرجات وأحدث مقاطع الفيديو - 2023/01/25
-   دعم الحصول على أسماء الممثلين الصينية من خلال ويكيبيديا - 2023/02/18
-   دعم ترجمة العناوين اليابانية - 2023/02/18
-   دعم البحث عن الممثلين - 2023/02/18
-   دعم التخزين المؤقت من خلال redis - 2023/03/17

## درس تعليمي

أولاً، تحتاج إلى تنزيل رمز المشروع محليًا، ثم تكوين الروبوت وتحريره`~/.tg_search_bot/config.yaml`：

```yaml
# TG 对话 ID
tg_chat_id:
# TG 机器人 Token
tg_bot_token:
# 全局是否使用代理 1 是 | 0 否
use_proxy:
# 访问 dmm 时是否使用代理，如果全局使用代理，则忽略该字段 1 是 | 0 否
use_proxy_dmm:
# 代理服务器地址，如果不使用代理，则忽略该字段
proxy_addr:
# 是否使用 Pikpak 自动发送功能 1 是 | 0 否
use_pikpak:
# 配置 TG API，如果不使用 Pikpak 自动发送功能，则忽略以下两个字段，可在这里申请 API: https://my.telegram.org/apps
tg_api_id:
tg_api_hash:
# 是否使用缓存 1 是 | 0 否
use_cache:
# redis 地址，如果不使用缓存，则忽略以下两个字段
redis_host:
redis_port:
# nsfw 1 是 | 0 否
enable_nsfw: 0
```

ملاحظة: إذا كنت تريد استخدام وظيفة الإرسال التلقائي في Pikpak، فستحتاج إلى ترخيصها يدويًا أولاً.[الروبوت الرسمي Pikpak](https://t.me/PikPak6_Bot)، ثم قم بتسجيل الدخول عند تشغيل الروبوت لأول مرة. (رمز دعوة بيكباك الخاص بي: 99492001، أدخل للحصول على العضوية)

أخيرًا، قم بتشغيل الروبوت: (توجد ملفات مثل السجلات والسجلات في`~/.tg_search_bot`تحت المحتويات)

```sh
# 方法一: 通过 docker 运行：(推荐)
docker-compose up -d
# 方法二: 通过普通方法运行:（Python >=3.10, 如果使用缓存的话需先开启 redis 服务）
pip install -r requirements.txt && python3 bot.py
```

## خطوات التطوير

أستخدم python-3.10.9 للتطوير، يرجى استخدام python &lt;= 3.10 للتطوير، بالإضافة إلى ذلك، يوصى باستخدام تطوير بيئة python الافتراضية لتجنب المشكلات غير الضرورية. فيما يلي خطوات التطوير الخاصة بي كمرجع فقط:

```shell
# python=3.10.9
git clone https://github.com/akynazh/tg-search-bot.git
cd tg-search-bot
python3 -m venv venv
source ./venv/bin/activate
pip3 install -r requirements.txt
```

ثم يمكنك البدء في كتابة التعليمات البرمجية. عند الانتهاء، تذكر كتابة أو تشغيل نسخة اختبارية (في`tests/test.py`وسط). يرجى التأكد من عدم وجود مشكلة في الاختبار قبل إرسال الرمز~

## الجميع

-   النسخة الإنجليزية
-   يدعم البحث عن الفيديو المزيد من مواقع الويب المغناطيسية (حاليًا يتم دعم The Pirate Bay فقط)
-   الميزات الأخرى التي ترغب في رؤيتها تظهر...

## شكر وتقدير

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->

<!-- prettier-ignore-start -->

<!-- markdownlint-disable -->

<table>
  <tbody>
    <tr>
      <td align="center" valign="top" width="14.28%"><a href="https://akynazh.site"><img src="https://avatars.githubusercontent.com/u/78672905?v=4?s=100" width="100px;" alt="Jack Bryant"/><br /><sub><b>Jack Bryant</b></sub></a><br /><a href="#maintenance-akynazh" title="Maintenance">🚧</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/z-hhh"><img src="https://avatars.githubusercontent.com/u/8455958?v=4?s=100" width="100px;" alt="zhhh"/><br /><sub><b>zhhh</b></sub></a><br /><a href="https://github.com/akynazh/tg-search-bot/commits?author=z-hhh" title="Code">💻</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://allcontributors.org"><img src="https://avatars.githubusercontent.com/u/46410174?v=4?s=100" width="100px;" alt="All Contributors"/><br /><sub><b>All Contributors</b></sub></a><br /><a href="https://github.com/akynazh/tg-search-bot/commits?author=all-contributors" title="Documentation">📖</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/JackBryant286"><img src="https://avatars.githubusercontent.com/u/113345781?v=4?s=100" width="100px;" alt="Jack Bryant"/><br /><sub><b>Julia</b></sub></a><br /><a href="https://github.com/akynazh/tg-search-bot/commits?author=JackBryant286" title="Code">💻</a></td>
    </tr>
  </tbody>
</table>

<!-- markdownlint-restore -->

<!-- prettier-ignore-end -->

<!-- ALL-CONTRIBUTORS-LIST:END -->

إذا كنت تريد أيضًا المساهمة في المجتمع، فيرجى التحقق من ذلك[الجميع](https://github.com/akynazh/tg-search-bot#todo)، وعلى أساس[خطوات التطوير](https://github.com/akynazh/tg-search-bot#开发步骤)من أجل التنمية، نرحب بالقضايا والعلاقات العامة.
