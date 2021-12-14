# homework 1

## CAP Теорема

[Теорема CAP](https://ru.wikipedia.org/wiki/%D0%A2%D0%B5%D0%BE%D1%80%D0%B5%D0%BC%D0%B0_CAP) - эвристическое утверждение о том, что в любой реализации распределённых вычислений возможно обеспечить не более двух из трёх следующих свойств:

* **согласованность данных** (англ. consistency) — во всех вычислительных узлах в один момент времени данные не противоречат друг другу;
* _доступность_ (англ. availability) — любой запрос к распределённой системе завершается корректным откликом, однако без гарантии, что ответы всех узлов системы совпадают;
* _**устойчивость к разделению**_ (англ. partition tolerance) — расщепление распределённой системы на несколько изолированных секций не приводит к некорректности отклика от каждой из секций.

![схема](https://upload.wikimedia.org/wikipedia/commons/e/e7/Cap-theorem.png)

##MongoDB
из источника [IBM](https://www.ibm.com/ru-ru/cloud/learn/cap-theorem#toc--cap-cp----oVh3rgM9)
> MongoDB — это популярная система управления базами данных NoSQL, в которой данные хранятся в виде документов BSON (бинарный JSON). Она часто используется для больших данных и динамических приложений, работающих в нескольких разных расположениях. В контексте теоремы CAP база данных

> MongoDB представляет собой хранилище данных CP — она отличается устойчивостью к разделению и обеспечивает согласованность, но не гарантирует доступность

> MongoDB — это система с одним главным узлом, в которой каждый набор реплик (внешняя ссылка) может иметь только один главный узел, принимающий все операции записи. Все остальные узлы в том же наборе реплик выполняют роль вспомогательных узлов — они получают от главного узла копию журнала операций и применяют ее к своим наборам данных. По умолчанию клиенты отправляют запросы на чтение главному узлу, однако они могут настроить параметры предпочтения чтения (внешняя ссылка), позволяющие обращаться для этой цели к вспомогательным узлам.

> В случае потери доступа к главному узлу вспомогательный узел с самой последней версией журнала операций выбирается в качестве нового главного узла. После того как все остальные вспомогательные узлы зарегистрируются на новом главном узле, доступ к кластеру восстанавливается. Поскольку в течение этого времени запросы на запись от клиентов не принимаются, данные остаются согласованными во всей сети.

Из [db-engines.com](https://db-engines.com/en/system/MongoDB)
> Transaction concepts - Multi-document ACID Transactions with snapshot isolation


Из [документации MongoDB о репликах](https://docs.mongodb.com/manual/replication/)

> Replication provides redundancy and increases data availability. With multiple copies of data on different database servers, replication provides a level of fault tolerance against the loss of a single database server.

> Asynchronous Replication - Secondaries replicate the primary's oplog and apply the operations to their data sets asynchronously. By having the secondaries' data sets reflect the primary's data set, the replica set can continue to function despite the failure of one or more members.


Из выше перечисленного пологаю что MongoDB это **CA** система, которая решает проблему доступности с помощью реплик.



