---
title: Windows 内核模式内核事务管理器
description: Windows 内核模式内核事务管理器
ms.assetid: 43bf96ed-8be8-4670-a310-99cd7c7f9073
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 125795e0b823a5e6623d0f293c163e588b1b8c7d
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89403494"
---
# <a name="windows-kernel-mode-kernel-transaction-manager"></a>Windows 内核模式内核事务管理器


处理一个或多个数据存储区上的多个读写操作，并且这些操作必须以原子方式全部成功或无法保留数据的完整性时，您可能希望将操作组合成单个事务。 如果事务中的所有操作都成功，则可以提交事务，以使所有更改都保留为原子单元。 如果发生失败，则可以回滚事务，以便将数据存储还原到其原始状态。

内核事务管理器 (KTM) 是在内核模式下实现事务处理的 Windows 内核模式组件。 KTM 允许内核模式组件（如驱动程序）执行事务。 此外，KTM 是用户模式 [事务性 NTFS (TxF) ](https://go.microsoft.com/fwlink/p/?linkid=131245) 所基于的平台。

有关如何在内核模式组件中使用 KTM 的信息，请参阅 [内核事务管理器](introduction-to-ktm.md)。

 

 




