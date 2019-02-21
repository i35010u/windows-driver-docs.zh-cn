---
title: 处理事务操作
description: 处理事务操作
ms.assetid: 9b82e9d6-3db2-4806-a087-1c9622dc04e2
keywords:
- WDK KTM，处理操作的事务
- 处理事务操作 WDK KTM
- WDK KTM，提交事务的事务
- 提交事务 WDK KTM
- WDK KTM，回滚事务的事务
- 回滚 WDK KTM 的事务
- WDK KTM，恢复事务的事务
- 恢复 WDK KTM 的事务
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd579db79ef67370c75770e86d3277b68bb69477
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554926"
---
# <a name="handling-transaction-operations"></a>处理事务操作


资源管理器必须处理三个事务操作：*提交*，*回滚*，并*恢复*。

向*提交的事务*，资源管理器对所有更改的事务数据永久和对其他事务可见。

向*回滚事务*，资源管理器中删除对事务的数据的所有更改。 资源管理器必须将数据还原到之前创建该事务的状态。

向*恢复事务*，资源管理器的事务将数据还原到已知的良好状态后在系统发生崩溃或其他意外的事件。

本部分包含以下主题：

[处理提交操作](handling-commit-operations.md)

[处理回滚操作](handling-rollback-operations.md)

[处理恢复操作](handling-recovery-operations.md)

 

 




