---
title: 创建事务客户端
description: 创建事务客户端
ms.assetid: 75d4758b-dfba-431b-9bfa-9dcb98c2a7cc
keywords:
- 事务性客户端 WDK KTM
- 事务性客户端 WDK KTM，创建事务性客户端
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 803e0fca9ab73b8c481c2a12f42c9ffaf95f0af3
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190075"
---
# <a name="creating-a-transactional-client"></a>创建事务客户端


[*事务性客户端*](transaction-processing-terms.md#ktm-term-transactional-client)是事务处理系统 (TPS) 组件，它使用资源管理器的导出接口访问资源管理器支持的资源，例如数据库。

通常，客户端会创建一个事务，执行一组数据库操作，然后提交该事务以使操作永久运行。 如果客户端遇到错误，则可以回滚事务，以删除事务的操作，而不是提交事务。

通常，使用内核模式 KTM 的事务性客户端必须为每个事务执行以下任务：

1.  创建事务对象。

    对 [**ZwCreateTransaction**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreatetransaction) 的调用将创建一个事务对象，提供一个对象句柄，并将对象标识符分配给一个 GUID) ，客户端可以将该对象 (标识符传递给 resource manager 以标识该事务。

2.  获取事务对象的标识符。

    客户端可以调用 [**ZwQueryInformationTransaction**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntqueryinformationtransaction) 来获取对象标识符。

3.  将事务对象的标识符传递给资源管理器。

    客户端通常会调用资源管理器的导出接口，以打开资源管理器的通信路径并将路径与事务相关联。 例如，资源管理器可能会提供类似于 "[理解 TPS 组件](understanding-tps-components.md)" 主题所描述的*CreateDataObject*例程。

4.  执行要包含在事务中的操作。

    通常，客户端调用资源管理器的接口来访问资源管理器的资源。 例如，数据库管理器的客户端可能会从数据库中读取和写入数据库。

5.  提交或回滚事务。

    如果所有资源操作都成功，则客户端必须调用 [**ZwCommitTransaction**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommittransaction) 来使操作永久运行。 如果操作失败，则客户端必须调用 [**ZwRollbackTransaction**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollbacktransaction) 而不是 **ZwCommitTransaction**。 例如，如果数据库管理器的客户端确定一系列写入操作中的一项失败，则客户端必须调用 **ZwRollbackTransaction** ，以使任何写入操作都不会成为永久性操作。

    客户端可以同步或异步方式调用 **ZwCommitTransaction** 和 **ZwRollbackTransaction** 。 如果客户端以同步方式调用这些例程，则在提交或回滚操作完成前，例程不会返回。

    有关如何提交和回滚事务的详细信息，请参阅 [处理事务操作](handling-transaction-operations.md)。

6.  关闭事务对象句柄。

    客户端处理完事务之后，必须调用 [**ZwClose**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose) 来关闭事务对象的句柄。

TPS 可能包含多个资源管理器。 如果客户端的事务包含对多个资源（例如两个资源管理器支持的两个数据库）的操作，则客户端通常会执行以下操作：

1.  为每个事务创建一个事务对象。

2.  将事务对象的标识符传递给每个资源管理器。

3.  通过调用每个资源管理器的接口，对每个数据库执行操作。

4.  如果所有操作都已完成且未发生错误，则提交事务，如果检测到错误，则会回滚事务。

如果 TPS 包含 *高级事务管理器*，则事务客户端通常不调用 KTM。 有关上级事务管理器及其客户端的详细信息，请参阅 [创建高级事务管理器](creating-a-superior-transaction-manager.md)。

事务性客户端可以调用 [**ZwSetInformationTransaction**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntsetinformationtransaction) 来设置特定于事务的信息。 例如，客户端可以设置事务的超时值或提供描述性字符串。 客户端可以调用 [**ZwQueryInformationTransaction**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntqueryinformationtransaction) 来检索有关事务的信息。 例如，客户端可以调用此例程来确定事务是否已提交或回滚。

 

