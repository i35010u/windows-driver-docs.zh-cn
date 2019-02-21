---
title: 注册和取消中断
description: 注册和取消中断
ms.assetid: 222782f3-092e-417d-ab1b-1988a593caa4
keywords:
- 中断 WDK 连接网络、 注册
- 中断 WDK 连接网络、 取消注册
- NdisMRegisterInterruptEx
- NdisMDeregisterInterruptEx
- 注册中断
- 取消中断
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93fd829d70a7e9bf1699319262f6f94141ee8412
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523828"
---
# <a name="registering-and-deregistering-interrupts"></a>注册和取消中断





微型端口驱动程序调用[ **NdisMRegisterInterruptEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563649)注册中断。 该驱动程序分配并初始化[ **NDIS\_微型端口\_中断\_特征**](https://msdn.microsoft.com/library/windows/hardware/ff566465)结构，以指定中断特征和函数入口点。 该驱动程序将向此结构传递**NdisMRegisterInterruptEx**。

驱动程序调用[ **NdisMDeRegisterInterruptEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563575)函数，以释放以前分配的资源**NdisMRegisterInterruptEx**。

 

 





