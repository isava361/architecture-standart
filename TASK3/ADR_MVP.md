### <a name="_b7urdng99y53"></a>**Название задачи:**
Концептуальная архитектура MVP для процесса открытия депозитов онлайн
### <a name="_hjk0fkfyohdk"></a>**Автор:**
Савельев Иван
### <a name="_uanumrh8zrui"></a>**Дата:**
01.08.2025
### <a name="_3bfxc9a45514"></a>**Функциональные требования**
Опишите здесь верхнеуровневые Use Cases. Их нужно оформить в виде таблицы с пошаговым описанием:

|**№**|**Действующие лица или системы**|**Use Case**|**Описание**|
| :-: | :- | :- | :- |
|1|Новый клиент, Сайт, Кол-центр, Бэк-офис, АБС|Подача заявки на депозит новым клиентом через сайт|1. Клиент видит на сайте список депозитов с актуальными ставками 2. Клиент заполняет форму заявки (ФИО, телефон) 3. Заявка поступает в систему кол-центра 4. Менеджер кол-центра связывается с клиентом, консультирует и приглашает в отделение для идентификации и завершения процесса 5. Обращение фиксируется в АБС для дальнейшей обработки бэк-офисом|
|2|Существующий клиент, Интернет-банк, Бэк-офис, АБС, СМС-шлюз|Подача заявки на депозит существующим клиентом через интернет-банк|1. Клиент в интернет-банке видит список депозитов с общими и персональными ставками 2. Клиент выбирает депозит, указывает счет списания и сумму 3. Клиент подтверждает операцию кодом из СМС 4. Заявка поступает в АБС на обработку бэк-офисом 5. После обработки и открытия депозита бэк-офисом клиент получает СМС-уведомление|
|3|Сотрудник бэк-офиса (депозиты, кредиты), АБС|Управление ставками по депозитам|1. Сотрудники кредитного и депозитного отделов получают доступ к новому модулю в АБС 2. Они управляют (рассчитывают, обновляют) ставками по депозитам в этом модуле, заменяя ручную работу в Excel|


### <a name="_u8xz25hbrgql"></a>**Нефункциональные требования**
Опишите здесь нефункциональные требования и архитектурно значимые требования.

|**№**|**Требование**|
| :-: | :- |
|1|Надежность: Система должна быть доступна 24/7 (99,9%) с возможностью переключения на резервный ЦОД|
|2|Производительность: Отклик интерфейсов должен быть быстрым (не более 100 мс), система должна быть готова к масштабированию|
|3|Безопасность: Исключить прямую работу с БД АБС из интернет-банка. Весь трафик с чувствительными данными должен шифроваться. Разграничить доступ к данным для сотрудников|
|4|Поддерживаемость: Предусмотреть возможность перехода на микросервисную архитектуру. Разработать документацию|
|5|Ограничения: Использовать существующий технологический стек. Учесть, что АБС масштабируется только вертикально, а текущая версия интернет-банка несовместима с Kafka


### <a name="_qmphm5d6rvi3"></a>**Решение**
Диаграмма контекста:
https://editor.plantuml.com/uml/lLPDJnfH5DtpArvPGI8GcwwwihKcfgaj4UggoMGOdZXr60Wp54tJ1CL-XLPiLqtJQap_02KIHX3y2-_zevxx68h0M5ZLZJDlxZtttFFElRhYk7h9BUUjq1tJDgnobhCTroqwznE9abw9vqntfvmfExna56oNssxSAEGJHKktAIVck5dBp2HMxyMITFHyuqaYhpikB-58MwMCFJTU9FHGafUSWXsnUKKpB1D8IomiVeg1QCcwk6IYAth24stHbuTX-dGc1l9GlR_3ULFqv2SyJuSoyHlV-ZXgXgEZ6dpFT5pJpjqeT2vhygDeomDWjl1yZ3SlgEptG6mc3vYu02Faovgu1kqh9beCeNrYAQk8Qyl3s2XbJ2QZ6xjQONlRDBWYGct9Aa0k4EU9Bgh8pw8Rm_cHyEG16g6uKnnNWGKynDT52yzjujJ1GGElNU4jCUAYmbhGfw42L8jD5T0KLy8RCp5qoz8C2C9BcfxpXJb5CqGVLS2WIe8CH2y6qPK6z6LXFgGIDI0kYG8AXrBxC4C-Kk4PntJz_jLd5W7Fm2k9KhdaUZAnoNN3ZRzqWEF3c4JTvgwMqUrT0ljsY_fpq1-aal6dQscsiRMwnA3H03a3kdTuO5HCMzjp9nHprF6m1K_1jf7Q31BiblBGIPKNNnNT3mXlo0R31VIKg4Tq0OGvxbZFE9Hm8hw8ypceZxXLt34JpqgwOV79Dfoye-LqbrVq_I7_7-8yXlezUImwauo6Gp6ODCNu9hM7XRATrKlx4MCvG0eIiaSNBFenDRvTEBsEtnxrUO4mcfmE2Ks3po8RMybeECfUXnX-_9wpl5Y0MoO49p8jLQiUW1EUMYLzvLFbvYiQCIHZSiSWgZP5iSVwAntTlGc5DhariPjkM1QR23MdxIvhIAIicMqpOzCv01CRmh_n-UCcQse1AMi40StA-6kHNK4u0OiYU18MOKdc8T2_WiuGMuupSGeYq-mcUdrXixk88obxSFvxlzAD3ZoomUPQAfrOJwUJAR-NgSlulyMdgmMhUAQSsGwqoDHANQJ8rBG7DgTMm49elX__oL6D4hGPcM4u-JKrbYTWJtyatz8G8X2Rba708Lg78PuWhuTh71nMk9t5_mj_0000


Диаграмма контейнеров:
https://editor.plantuml.com/uml/nLPTQnj757tNhvZwIG99IqgV-XH_GHBiTckvUGeiezLWRxfQYTrH75CAYLIt2IvsNGeDfSIO4l8gYonUMxNy5sR-KS-TrRVMSKiVwWTfDJltt7FFFNF7zoF9Gzcg-xbFlC3rMpN1TgLiHfzRLiZtoZkUt6rLMv48tKOWHI3BRgDkDNqUK4mfaZNVgrghdvLiMlfwSyEgyqYA44lEAYAu5uYmt2Jyd2t2g17anNClabwmuxY-1y0YMr9dkgDVgrY_r6tLm_CHVYNgagahrST3hAvrUuas_ZxvpTIvwgfhREak5NALVMIjvprm30CXdIeFlg60DxGLo2-mCzRjqYY8q9OhTlcBzMss-NYro3OhhFBLHfdTpkKlDK3aW1Y0JI4toich4MNwMPseCu9T4tvprxE-3BdhYri0k_gOwPS0eiKOq9CQdFNdCX_L8sU7Ix77zuq-wWzrLjAlL5yVgGkZn2-ce5Vu97BBziE922xtVSSL98KJcQKKOoeRAOjAIlg7L4peqvs5rSUWg6vGRHUllrS3R45WaJtYp_WarvweHfuKQOAkkapxP3-mhIt1NLb-6lqR1KQQEYkDLb3ZuNxUlPV1dVhGfspgkWHYRNMbN-X3V2V4-GEstM3F1VK9tpsMttni5vOAxDiSmz_OblaG2aSElFtCSuSba5Dwb8rOjv6Z1mJZ5ggxo2hD4DPbAus6D7hzgMv8EsphwsDo63D4QG761Ds4H1pCiyAR8ZEXCTuCnZ4Z4FIJGlfKJw8F30P-TVIFr2-g4shD5BDM7PPJgnAl4_NhGWLs8v8xeO3D3VLtXZY1uImbwFYuoN15ee-Wyqmn-e0wDAiWRpPzp-NIQmItwlWRzVek7K-nFp5cHduZ0Ib7VAvIuz1xTBcJlXkeSyF-VDZ-3eEmupIWJTuoTYI_0EcDEibGR9h-b6vpZ3-csoZh5IL9qcQbee5o1q-76Q9L8uVNU1FdCnqS7u1tauuf74ms6INPMhr5sT04deZXXmJPXufrwK2XaGTWI6U4fbLiQ240L0S8eJt3zHwnDueFZ3qlqmDA0vOK7D98LJCVMyAVFpFJddi_j3QuMCYKO8p4wJnujBQoEWGYZ4pNBFRYl-4j7ExJyH7gpX_KX42trYlRreFjRRjo9zNP1hu5plmKc1Y3lDcRwkboj1-uB4_P2jE9fZ67Lqgs0Cpu1TtLXoes_jomu4rCvbILxt8v0bouPXVlHkCX4kKdTP6UB88RIK0WSp7Pn_qUHlp7n6LF0lOfzjobqq8JYC7uWlaVScUcdBkQCu7DVVtF8RClx5CpH6FJxGLBpKouXKov-oAeuN-klm40

Также опишите, какой логикой вы руководствовались в ходе принятия решений и выбора технологий. Не забывайте, что необходимо учесть все функциональные и нефункциональные требования
1. Микросервисная архитектура (Сервис Заявок, Сервис Ставок, Адаптер к АБС): Выбрана для изоляции новой логики от легаси. Это позволяет независимо разрабатывать, масштабировать (горизонтально) и развертывать новые компоненты, что соответствует требованиям к производительности (P2, P3) и надежности (R1). Использование Java-стека опирается на существующую экспертизу в банке (S3)
2. Выделенный "Сервис Ставок": Решает проблему с расчетом ставок в Excel. Он становится единым источником правды, а собственный UI и разделение прав доступа решают требование безопасности (+R5)
3. "Адаптер к АБС": Ключевой компонент для решения проблемы производительности и перегрузки АБС (R4, +R4). Он принимает запросы от "Сервиса Заявок" и асинхронно помещает их в очередь на обработку в АБС (например, через временную таблицу в БД). Это защищает АБС от пиковых нагрузок
4. Технологии: Выбран стек Java/Spring Boot и PostgreSQL. Он соответствует имеющейся в банке экспертизе, хорошо подходит для микросервисов и не создает дополнительной зависимости от подрядчиков
5. Интеграции: Все новые интеграции происходят по REST/HTTPS, что является современным стандартом и обеспечивает необходимую безопасность (R3). Отказ от прямой интеграции с ядром интернет-банка для отправки СМС снижает зависимость от подрядчика (S4)

### <a name="_bjrr7veeh80c"></a>**Альтернативы**
1. Доработка монолита интернет-банка: Рассмотрели реализовать всю логику внутри существующего интернет-банка, но это влечет усиление зависимости от подрядчика, невозможность горизонтального масштабирования, риск дестабилизации существующего функционала, технологические ограничения (.NET 4.5).
2. Реализация логики на стороне АБС: Рассмотрели вариант разработки новых модули и API на PL/SQL внутри АБС, но это влечет критическое увеличение нагрузки на уже перегруженную АБС, сложность разработки современных веб-сервисов на PL/SQL, сохранение проблемы вертикального масштабирования


**Недостатки, ограничения, риски**

1. Сложность интеграции с АБС: Механизм обратного уведомления от АБС к адаптеру (о том, что заявка обработана) может потребовать доработок в самой АБС, что бывает сложно и долго. На этапе MVP это может быть ручной процесс с помощью бэк-оффиса
2. Операционная сложность: Внедрение микросервисов требует выстраивания процессов CI/CD, мониторинга и логирования, что увеличивает операционную нагрузку на IT-отдел
3. Риск распределенной транзакции: Хотя в MVP процесс линеен, в будущем при усложнении логики может возникнуть потребность в обеспечении консистентности данных между несколькими сервисами, что потребует реализации сложных паттернов (например, Saga)
4. Требования к команде: Несмотря на наличие Java-экспертизы, команде может потребоваться дополнительное обучение по специфике микросервисной архитектуры
