---
title: 处理事务操作
description: 处理事务操作
keywords:
- 事务 WDK KTM，处理操作
- 处理事务操作 WDK KTM
- 事务 WDK KTM，提交事务
- 提交事务 WDK KTM
- 事务 WDK KTM，回滚事务
- 回滚事务 WDK KTM
- 事务 WDK KTM，恢复事务
- 恢复事务 WDK KTM
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4c98c4c2673b69d5b4e73ff556a34464e7f2d89
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836935"
---
# <a name="handling-transaction-operations"></a>处理事务操作


资源管理器必须处理三个事务操作： *commit*、 *rollback* 和 *recovery*。

若要 *提交事务*，资源管理器会对事务的数据进行永久更改，使其对其他事务可见。

若要 *回滚事务*，资源管理器将删除对事务数据所做的所有更改。 资源管理器必须将数据还原到创建事务之前所处的状态。

若要 *恢复事务*，资源管理器会在系统崩溃或发生其他意外事件后，将事务的数据还原到已知的良好状态。

本节包含下列主题：

[处理提交操作](handling-commit-operations.md)

[处理回滚操作](handling-rollback-operations.md)

[处理恢复操作](handling-recovery-operations.md)

 

 




