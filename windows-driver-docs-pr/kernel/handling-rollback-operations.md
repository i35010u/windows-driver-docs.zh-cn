---
title: 处理回滚操作
description: 处理回滚操作
keywords:
- 事务 WDK KTM，回滚事务
- 回滚事务 WDK KTM
- 资源管理器 WDK KTM，滚动后备事务
- 事务性客户端 WDK KTM，回滚事务
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4d1572149a599ca6c7660dd39f72746af9b65a6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830391"
---
# <a name="handling-rollback-operations"></a>处理回滚操作


如果资源管理器、事务客户端或 KTM 确定事务不能提交 (通常是因为) 检测到错误，则会回滚该事务。

若要回滚事务，资源管理器可以调用 [**ZwRollbackEnlistment**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollbackenlistment)。 在资源管理器调用 [**ZwCreateEnlistment**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreateenlistment) 以在事务中登记之前，它可以在调用 [**ZwPrepareComplete**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntpreparecomplete)之前随时回滚事务。

事务客户端可以通过调用 [**ZwRollbackTransaction**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollbacktransaction)回滚其事务。 在事务客户端调用 [**ZwCreateTransaction**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreatetransaction) 创建一个事务后，它可以在调用 [**ZwCommitTransaction**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommittransaction)之前随时回滚该事务。

此外，事务客户端可以通过调用 [**ZwSetInformationTransaction**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntsetinformationtransaction)来设置事务的超时值。 如果未在指定的时间内提交事务，则 KTM 将回滚该事务。

当对 **ZwRollbackEnlistment** 或 **ZwRollbackTransaction** 进行调用，或超出超时值时，KTM 会将事务 \_ 通知 \_ 回滚 [通知](transaction-notifications.md) 发送到所有资源管理器。

当每个资源管理器收到事务 \_ 通知 \_ 回滚通知时，它必须执行以下操作：

1.  将事务的数据还原到在事务中登记资源管理器之前所处的状态。

    通常情况下，资源管理器通过将事务保存的初始数据从日志流复制到数据库的公共永久存储来还原事务的数据。 有关如何使用日志流的详细信息，请参阅 [使用 KTM 的日志流](using-log-streams-with-ktm.md)。

2.  调用 [**ZwRollbackComplete**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollbackcomplete)。

调用 **ZwRollbackComplete** 后，资源管理器应调用 [**ZwClose**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose) 以关闭登记句柄。

如果资源管理器启动了回滚操作，它必须使用其客户端接口来通知客户端事务失败。

 

