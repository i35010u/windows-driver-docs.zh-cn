---
title: Windows 内核模式内核事务管理器
description: Windows 内核模式内核事务管理器
ms.assetid: 43bf96ed-8be8-4670-a310-99cd7c7f9073
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 016fc60ae26f7b561db03037b6d554dacd8d7b57
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546187"
---
# <a name="windows-kernel-mode-kernel-transaction-manager"></a>Windows 内核模式内核事务管理器


当您处理多个读取和写入一个或多个数据存储和操作必须全部以原子方式成功还是失败，保持数据的完整性时，可能想要作为单个事务的操作组合在一起。 如果在事务中操作的所有成功，以便所有更改将都保留原子单位的形式可以提交事务。 如果发生故障，可以回滚事务，以便数据存储还原到其原始状态。

内核事务管理器 (KTM) 是在内核模式下实现事务处理的 Windows 内核模式组件。 KTM 允许内核模式组件，如驱动程序，以执行事务。 此外，KTM 是上的用户模式的平台[事务性 NTFS (TxF)](https://go.microsoft.com/fwlink/p/?linkid=131245)为基础。

有关如何使用 KTM 内核模式组件中的信息，请参阅[内核事务管理器](using-kernel-transaction-manager.md)。

 

 




