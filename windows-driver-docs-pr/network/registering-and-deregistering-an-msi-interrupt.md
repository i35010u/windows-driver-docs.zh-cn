---
title: 注册和取消注册 MSI 中断
description: 注册和取消注册 MSI 中断
ms.assetid: 61bdcf8c-b56e-4ef9-b9db-407591ff2f95
keywords:
- MSI X WDK 连接网络、 注册中断
- 消息信号中断 WDK 网络注册中断
- Msi WDK 网络注册中断
- 中断 WDK 连接网络、 注册
- MSI X WDK 连接网络、 取消的中断
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 648b059770ad572720b9f95a40e573d0eb4d1a06
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566593"
---
# <a name="registering-and-deregistering-an-msi-interrupt"></a>注册和取消注册 MSI 中断





若要注册 MSI 的支持，微型端口驱动程序调用[ **NdisMRegisterInterruptEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563649)函数以注册 MSI 中断。 该驱动程序分配并初始化[ **NDIS\_微型端口\_中断\_特征**](https://msdn.microsoft.com/library/windows/hardware/ff566465)结构，以指定中断特征和函数入口点。 该驱动程序必须设置**MsiSupported**成员的 NDIS\_微型端口\_中断\_特征结构**TRUE**。 该驱动程序然后将传递的结构**NdisMRegisterInterruptEx**。

必须定义以下函数以支持 MSI 中断：

-   [*MiniportMessageInterrupt*](https://msdn.microsoft.com/library/windows/hardware/ff559407)

-   [*MiniportMessageInterruptDpc*](https://msdn.microsoft.com/library/windows/hardware/ff559411)

-   [*MiniportDisableMessageInterrupt*](https://msdn.microsoft.com/library/windows/hardware/ff559376)

-   [*MiniportEnableMessageInterrupt*](https://msdn.microsoft.com/library/windows/hardware/ff559383)

微型端口驱动程序应为基于行的中断函数 （它们以下列表中所示），提供入口点，即使该驱动程序支持 MSI 入口点。 如果 NDIS 不会授予 MSI 中断，它可以作为回退条件授予正常中断。

行中断函数包括：

-   [*MiniportInterrupt*](https://msdn.microsoft.com/library/windows/hardware/ff559395)

-   [*MiniportInterruptDPC*](https://msdn.microsoft.com/library/windows/hardware/ff559398)

-   [*MiniportDisableInterruptEx*](https://msdn.microsoft.com/library/windows/hardware/ff559375)

-   [*MiniportEnableInterruptEx*](https://msdn.microsoft.com/library/windows/hardware/ff559380)

驱动程序应调用[ **NdisMDeregisterInterruptEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563575)函数，以释放以前分配的资源**NdisMRegisterInterruptEx**。

 

 





