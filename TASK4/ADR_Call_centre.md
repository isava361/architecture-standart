### <a name="_b7urdng99y53"></a>**Название задачи:**
Архитектура предоставления данных о ставках по депозитам для внутреннего и партнёрского кол-центров
### <a name="_hjk0fkfyohdk"></a>**Автор:**
Савельев Иван
### <a name="_uanumrh8zrui"></a>**Дата:**
02.08.2025
### <a name="_3bfxc9a45514"></a>**Функциональные требования**
Опишите здесь верхнеуровневые Use Cases. Их нужно оформить в виде таблицы с пошаговым описанием:

|**№**|**Действующие лица или системы**|**Use Case**|**Описание**|
| :-: | :- | :- | :- |
|1|Сотрудник внутреннего кол-центра, клиент, система кол-центра|Консультация клиента по актуальным ставкам|1. Клиент звонит в кол-центр банка 2. Сотрудник открывает данные по ставкам в своей системе 3. Система в реальном времени отображает актуальные ставки по депозитам, полученные из внутренней системы банка 4. Сотрудник консультирует клиента, используя точные и свежие данные|
|2|Сотрудник партнёрского кол-центра, клиент, система партнерского кол-центра|Консультация клиента по ставкам|1. Клиент звонит на горячую линию (звонок перенаправляется партнёру) 2. Сотрудник партнёрского кол-центра открывает свою систему 3. Система отображает ставки по депозитам, загруженные из файла, который банк предоставил ранее 4. Сотрудник консультирует клиента|
|3|Система банка, Система партнёрского кол-центра|Автоматическая передача актуальных ставок партнёру|1. В банке изменяются ставки по депозитам. 2. Внутренняя система банка автоматически формирует файл в формате CSV с новыми ставками 3. Система выгружает этот файл на защищённый файловый ресурс (SFTP-сервер) 4. Система партнёра по расписанию забирает файл с ресурса и обновляет данные у себя|

### <a name="_u8xz25hbrgql"></a>**Нефункциональные требования**
Опишите здесь нефункциональные требования и архитектурно значимые требования.

|**№**|**Требование**|
| :-: | :- |
|1|Своевременность данных: Сотрудники внутреннего кол-центра должны иметь доступ к ставкам в режиме реального времени. Данные для партнёрского кол-центра могут обновляться с некоторой периодичностью (раз в день)|
|2|Безопасность: Передача данных партнёру должна осуществляться по защищённому каналу. Доступ к API для внутреннего кол-центра должен быть авторизован|
|3|Надежность: Процесс выгрузки файла для партнёра должен быть автоматизирован и надёжен. Необходимо предусмотреть логирование и оповещения в случае сбоев|
|4|Ограничения: Партнёрский кол-центр не может использовать API для получения данных и готов работать только с файлами|
### <a name="_qmphm5d6rvi3"></a>**Решение**
Диаграмма контекста:
https://editor.plantuml.com/uml/nLHDYzDG5DttLpoxIc7Q8BXoDSmu8k90QQlRaAOP9vYc9Kbr1X4wxQ12bJ9k13U3k70RQsCpgMd_mdt_oFDUMgOV6NKXcCKBkU-zSyuzzzxiUhxk-fscdRjbEORTQPZisFVRtbrLTVKNfQUMVzofTppJDLgERpf-oMWrrRQjE-9EqVCRjbLNz-yKooBq-F2HsjGzttGHqlR5ZHE_r1RekRBfUYr7gUl6CwrrT6GPvWxBqsUQyHxlyZwDAQ68OaRV-7kAYuYVKyJFACYBSrzephiKq8YcV4WXxp5-ndio46FzIL6-iAGmTDlM36WrtHieHfJmlWXIY522zJlD691cDALfaRyMSRcVid_2HWB2FjZVWJQIS485xao1AO_ZqEXQHHksEgQh_PKQOBtzrpggfoX4KpiuyLSTqJmPJgL4qiGGzWKBrZLEfcmwnOTyM91IBi4NOECS-NHJW3a0nb0qnFf6f4R13dkeFzVNnMGOSxEeEKYw-4pu1TvdKkIrHziEVLXwAPIYHrRH86EfOw_LSHgwUweOjpD8ORB8Zgue4NtOenZS0-dtaA5keKnrWa_fDLCEdvGB-G9xcMDuKWgbORPRdkMlfHP2vqXo3J9myel-43iu-4F46MJ4oA-FDsgEl0OKhlQ-wFjNkLp5jDT7Qvl-8swCOUV5-l08W3qBzxLAPfza0ybfXCyHC8BDUOn49fM3QarzKAkLgo18uJUXVjy9bzA5K6ZE9A2lYmCJXYuKrPeofNg_9aeX2Uzbp-2VM6VIw4awM23TQACPNOdQJKKhnDlpA0e9CKdQAzjJcGfR4_H_XEHsJQU1F_Cl

Диаграмма контейнеров
https://editor.plantuml.com/uml/ZLLHJzDG67tVhxZkQKiSYubFFY43emHqikbhqsqLbdHjqtO8CIPi4p510wW9FXW9YSRNCPYKmSfVkFSVURwltJAsQKW8lRszztpddE_SkrdFrrs_NZCJTwfMsQnN3B7c-uxt89jrzTSpgrL_hLwgUuPRjYtViFoPibtBEgPkqPwCvrVCQYcRkv_9qzIBvQLiJVTymyMKbhDhZctH7eVm4uLDVAbf2nj-IYzvTqLIxii3UPoaqJVLK4qPgXtPbu7i2NacsnZsrQxQ5Z8K_BajEx8dssexcHu5A-kcgPLHnt0rZwS9yLW6lAahhsHRO5yeBpFgFTxxggcsC9S2N5-r-AtBnVRKNfhf7ABMDIrI7q2dWxUkQewI26vISE2XXVAted8Ds2syzjK1dWscTWgDKpWocIEQ1i-T0Ort65p8I_0PyGdOH6h0QiwkMnNTtKoLxqsX46BF9QFqCt2zANjWiejdeFO8imkIeJp7AveYEoAr_3AVJgR5cuGG-CiX2teLWbEkxXkUXdYiLyj6LAWBuXqg9-Hnx5SeUwHaKL_Nxug2urQjLJ5dstuaZ-q_0us1lPTgZuK-p3yHCX3g4-WrY17PDfGFTo92n2TEMaftgXebrRLDqt01JnYvuGGLN5ae50cQY_-G9-IpF45FcZ1nq6fQb841KGo8sguWewOsAJr6mjXmRDVNQdQbRh8ftx7dJBKWxEEOcgZ5XVAQGMihOj4kCQyld4YoCi2oris-mnFP0TbJ_lGdfemTdA8-6bnuLCmphRU9qNRDb-A6LKfKv41-dUXHtlRyLTSeF5zY7h_OdJu5GM3GW-8MdX32cUkEdmbKMp7CgKToeZMtEMMKciApfzd7nMA-m8e0hyr75yX4-8v0xWJ9m0qIUmPP9w0VKghOKWhui4AiMUwZ8G44RLElwJZ9S51hFE6Z_ltcyy6iisXe01aOCkVvkHmGuFxGUxudl5U-mrXi07KfWzBHYS5_9lCpZdV8FRuG4miE8EGSd-aUQN0RBYATLwHmv7p4LmAf68laJHxoyqIO1Y39c6O4eotzzwORGptaSnLmWlw1EMjO5Vms_0K0

1. Данное решение полностью построено на уже спроектированных компонентах ("Сервис Ставок"), что минимизирует затраты на разработку
2. Данное решение удовлетворяет требованиям обоих кол-центров, используя разные, но подходящие для каждого случая механизмы интеграции (API для внутреннего, файлы для внешнего)
3. Использование SFTP-сервера является отраслевым стандартом для безопасной передачи файлов между организациями и решает требование безопасности

### <a name="_bjrr7veeh80c"></a>**Альтернативы**
1. Была рассмотрена отправка файла по электронной почте: "Модуль экспорта" мог бы отправлять файл на e-mail партнёра, но это влечет за собой низкую безопасность (e-mail легко перехватить), отсутствие гарантий доставки, процесс не полностью автоматизирован на стороне партнёра (требуется ручное скачивание и загрузка)
2. Предоставление партнёру доступа к веб-интерфейсу: Была рассмотрена возможность создать специальную веб-страницу, где сотрудники партнёра могли бы смотреть ставки, однако это неудобно для операторов партнёра (нужно переключаться между окнами), не решает задачу интеграции с их системой, создает дополнительные риски безопасности

**Недостатки, ограничения, риски**

1. Рассинхронизация данных: Сотрудники партнёрского кол-центра всегда будут работать с немного устаревшими данными (например, вчерашними). Это является риском и должно быть чётко прописано в их скриптах (Например: "ставки актуальны на утро сегодняшнего дня")
2. Надёжность файлового обмена: Процесс зависит от работоспособности трёх систем: нашего "Сервиса Ставок", SFTP-сервера и системы партнёра. Сбой в любом звене приведёт к тому, что партнёр не получит обновления. Требуется внедрение мониторинга и алертов на процесс выгрузки
3. Хрупкость формата файла: Любое изменение в структуре файла (порядок колонок, разделитель) сломает интеграцию. Требуется строгое версионирование и согласование формата с партнёром
