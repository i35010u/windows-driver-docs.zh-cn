---
title: 创建事务客户端
description: 创建事务客户端
ms.assetid: 75d4758b-dfba-431b-9bfa-9dcb98c2a7cc
keywords:
- 事务客户端 WDK KTM
- 事务客户端 WDK KTM，创建事务的客户端
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b36e896890e0dfa4158a5bcbe5444fe977f418a2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377173"
---
# <a name="creating-a-transactional-client"></a>创建事务客户端


一个[*事务客户端*](transaction-processing-terms.md#ktm-term-transactional-client)是事务处理系统 (TPS) 组件，它使用资源管理器的导出的接口来访问资源，例如数据库、 的资源管理器支持。

通常情况下，客户端创建一个事务、 执行数据库操作的一组，然后提交事务以使操作为永久。 如果客户端时遇到错误，它可以回滚事务以删除而不是提交事务的事务的操作。

通常情况下，使用内核模式 KTM 的事务客户端必须为每个事务中执行以下任务：

1.  创建事务对象。

    调用[ **ZwCreateTransaction** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcreatetransaction)创建事务对象，提供了对象句柄，并将分配客户端可以将传递到资源管理器来标识的对象标识符 (GUID)事务。

2.  获取事务对象的标识符。

    客户端可以调用[ **ZwQueryInformationTransaction** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntqueryinformationtransaction)若要获取的对象标识符。

3.  将事务对象的标识符传递到资源管理器。

    客户端通常会调用资源管理器的导出的接口可打开资源管理器的通信路径，从而将该路径与事务相关联。 例如，可能会提供资源管理器*CreateDataObject*类似于一个例程，[了解 TP 组件](understanding-tps-components.md)主题介绍。

4.  执行操作要包含在事务中。

    通常情况下，客户端调用资源管理器的接口来访问资源管理器的资源。 例如，数据库管理器的客户端可能会读取和写入到数据库。

5.  提交或回滚事务。

    如果资源的所有操作都成功，必须调用客户端[ **ZwCommitTransaction** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcommittransaction)若要永久操作。 如果操作失败，必须调用客户端[ **ZwRollbackTransaction** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrollbacktransaction)而不是**ZwCommitTransaction**。 例如，如果客户端的数据库管理器确定失败的写入操作的一系列之一，客户端必须调用**ZwRollbackTransaction** ，以便将成为永久性的任何写入操作。

    客户端可以调用**ZwCommitTransaction**并**ZwRollbackTransaction**同步或异步。 如果客户端以同步方式调用这些例程，例程提交或回滚操作完成之前不会返回。

    有关如何提交和回滚的事务的详细信息，请参阅[处理事务操作](handling-transaction-operations.md)。

6.  关闭事务对象句柄。

    客户端已完成处理该事务后，它必须调用[ **ZwClose** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntclose)关闭事务对象的句柄

TP 可能包括多个资源管理器。 如果客户端的事务包括对多个资源，例如两个数据库的两个资源管理器支持，操作客户端通常执行以下操作：

1.  创建每个事务的单个事务对象。

2.  将事务对象的标识符传递给每个资源管理器。

3.  通过调用每个资源管理器的界面中执行每个数据库上的操作。

4.  如果所有操作完成且没有错误，或如果检测到错误回滚该事务将提交事务。

如果包含在 TP*上级事务管理器*，事务的客户端通常不会调用 KTM。 有关高级事务管理器和客户端的详细信息，请参阅[上级事务管理器中创建](creating-a-superior-transaction-manager.md)。

事务的客户端可以调用[ **ZwSetInformationTransaction** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntsetinformationtransaction)设置特定于事务的信息。 例如，客户端可以设置该事务的超时值或提供描述性字符串。 客户端可以调用[ **ZwQueryInformationTransaction** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntqueryinformationtransaction)检索关于事务的信息。 例如，客户端可以调用此例程，以确定是否已提交或回滚事务。

 

 




