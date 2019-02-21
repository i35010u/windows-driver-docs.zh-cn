---
title: 处理回滚操作
description: 处理回滚操作
ms.assetid: d36bfac8-47dc-4fcd-a6e2-feb27d244630
keywords:
- WDK KTM，回滚事务的事务
- 回滚 WDK KTM 的事务
- 资源管理器 WDK KTM，滚动支持事务
- 事务客户端 WDK KTM，回滚事务
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 74e93ae910fc9008d1c623334d6b4b4a27b24655
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519678"
---
# <a name="handling-rollback-operations"></a>处理回滚操作


资源管理器、 事务客户端或 KTM 可以回滚事务，如果确定不能提交事务 (通常因为检测到错误)。

若要回滚事务，资源管理器可以调用[ **ZwRollbackEnlistment**](https://msdn.microsoft.com/library/windows/hardware/ff567083)。 资源管理器调用了具有[ **ZwCreateEnlistment** ](https://msdn.microsoft.com/library/windows/hardware/ff566422)若要在事务中登记，它可以回滚事务时调用之前[ **ZwPrepareComplete**](https://msdn.microsoft.com/library/windows/hardware/ff567037)。

事务的客户端可以回滚其事务通过调用[ **ZwRollbackTransaction**](https://msdn.microsoft.com/library/windows/hardware/ff567086)。 事务的客户端具有调用后[ **ZwCreateTransaction** ](https://msdn.microsoft.com/library/windows/hardware/ff566429)若要创建一个事务，它可以回滚事务时调用之前[ **ZwCommitTransaction**](https://msdn.microsoft.com/library/windows/hardware/ff566420)。

此外，事务的客户端可以设置事务的超时值，通过调用[ **ZwSetInformationTransaction**](https://msdn.microsoft.com/library/windows/hardware/ff567104)。 如果未提交的指定的时间内 KTM 回滚事务。

在调用**ZwRollbackEnlistment**或**ZwRollbackTransaction**进行，或 KTM 当超过超时值时，将事务发送\_通知\_回滚[通知](transaction-notifications.md)到所有资源管理器。

当每个资源管理器收到事务\_通知\_回滚通知时，它必须执行以下操作：

1.  事务的数据还原到在事务中登记的资源管理器之前的状态。

    通常情况下，资源管理器中日志流事务的已保存的初始数据复制到数据库的公共、 永久存储通过还原事务的数据。 有关如何使用日志流的详细信息，请参阅[使用日志流与 KTM 一起](using-log-streams-with-ktm.md)。

2.  调用[ **ZwRollbackComplete**](https://msdn.microsoft.com/library/windows/hardware/ff567081)。

在调用**ZwRollbackComplete**，应调用资源管理器[ **ZwClose** ](https://msdn.microsoft.com/library/windows/hardware/ff566417)关闭登记句柄。

如果资源管理器启动的回滚操作，它必须使用其客户端接口以通知客户端，则事务失败。

 

 




