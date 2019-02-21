---
title: 清除上虚拟端口的接收筛选器
description: 清除上虚拟端口的接收筛选器
ms.assetid: 8431322B-2BF0-4F82-AAAE-0E0396BBC857
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93e743a243aade14c147a8a7c8678c6e5cf1ea61
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543330"
---
# <a name="clearing-a-receive-filter-on-a-virtual-port"></a>清除上虚拟端口的接收筛选器


若要清除的 NIC 交换机上的虚拟端口 (VPort) 从接收筛选器，基础驱动程序发出的对象标识符 (OID) 组请求[OID\_接收\_筛选器\_清除\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569785). **InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向[ **NDIS\_接收\_筛选器\_清除\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567166)结构。

过量的驱动程序问题之前[OID\_接收\_筛选器\_清除\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569785)请求，它必须初始化[ **NDIS\_接收\_筛选器\_清除\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567166)结构，并按以下方式设置成员：

-   **QueueId**成员必须设置为 NDIS\_默认\_接收\_队列\_id。

-   **FilterId**成员必须设置为从早期获取驱动程序的筛选器标识符值[OID\_接收\_筛选器\_设置\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569795)方法 OID 请求。 详细了解如何设置接收筛选器，请参阅[上虚拟端口设置接收的筛选器](setting-a-receive-filter-on-a-virtual-port.md)。

基础驱动程序必须清除所有之前释放 VPort 设置 VPort 的筛选器。 基础驱动程序还必须清除所有筛选器，然后关闭其绑定到设置默认 VPort 或从网络适配器分离。

 

 





