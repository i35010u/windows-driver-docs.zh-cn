---
title: 协议驱动程序中的可分页和可放弃代码
description: 协议驱动程序中的可分页和可放弃代码
ms.assetid: acc27690-cdc3-433c-85c4-489501ea3d26
keywords:
- 协议驱动程序 WDK 网络、 可分页和可放弃代码
- NDIS 协议驱动程序 WDK，可分页和可放弃代码
- 可分页并可放弃代码 WDK NDIS 协议
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff6c661ccc3942785b1ae9c4c5a0336f7f654cb4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522345"
---
# <a name="pageable-and-discardable-code-in-a-protocol-driver"></a>协议驱动程序中的可分页和可放弃代码





驱动程序开发人员应将代码指定为可分页，只要有可能，释放系统空间必须驻留在内存中的代码。 您可以将标记为具有可分页的函数[ **NDIS\_PAGEABLE\_函数**](https://msdn.microsoft.com/library/windows/hardware/ff557121)宏。 IRQL、 资源管理功能和其他特征的一个函数可能会禁止在正在可分页的函数。

每个*ProtocolXxx*函数在范围内的 IRQL 运行从被动\_调度到级别\_级别。 以独占方式在 IRQL 运行的函数 = 被动\_级别应标记为可分页。

在 IRQL 运行的驱动程序函数 = 被动\_级别可为可分页，只要它既不调用也不函数调用的任何 IRQL 在运行&gt;= 调度\_级别-例如获取自旋锁的函数。 获取数值调节钮锁导致获取线程的调度到引发 IRQL\_级别。 驱动程序函数，例如[ *ProtocolBindAdapterEx*](https://msdn.microsoft.com/library/windows/hardware/ff570220)，运行在 IRQL = 被动\_级别不能调用任何**Ndis * Xxx*** 在 IRQL运行的函数&gt;= 调度\_级别如果该驱动程序函数标记为可分页的代码。 详细了解 IRQL 为每个**Ndis * Xxx*** 函数中，请参阅[NDIS 库函数](https://msdn.microsoft.com/library/windows/hardware/ff557039)。

[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113) NDIS 协议驱动程序，以及仅从调用的代码的函数**DriverEntry**，应通过使用指定为仅初始化代码[ **NDIS\_INIT\_函数**](https://msdn.microsoft.com/library/windows/hardware/ff557007)宏。 使用此宏标识的代码假定仅运行一次在系统初始化时，，并因此，仅在该时间段映射。 标记为仅初始化返回的函数后，它将被放弃。

 

 





