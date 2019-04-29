---
title: 中断调解
description: 中断调解
ms.assetid: 291f9606-6379-4b78-b388-ba663f84b431
keywords:
- 中断裁决 WDK 网络
- 中断 WDK 连接网络、 减少的数量
- OID_GEN_INTERRUPT_MODERATION
- NDIS_INTERRUPT_MODERATION_PARAMETERS
- 中断 WDK 网络审查
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93c0de142b47b8e84e9d52483b8bb635a8bbbf45
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362917"
---
# <a name="interrupt-moderation"></a>中断调解





若要减少中断的数量，数目的 Nic，请使用*的中断裁决*。 中断裁决，与 NIC 硬件不会生成中断，它接收的数据包后，立即。 相反，硬件等待更多数据包到达，或等待超时过期之前生成中断。 硬件供应商指定数据包、 超时间隔或其他中断裁决算法的最大数目。

数据包的测量往返时间是一种最常用的技术来确定两个终结点之间的网络带宽。 但是，启用中断裁决，接收数据包不会生成立即中断，并且因此一个特定的数据包的感知往返时间变得大于的平均时间。 若要允许的数据包的往返时间准确度量，NDIS 提供的功能，可以禁用和启用按需中断裁决。

所有 NDIS 6.0 和更高版本的微型端口驱动程序必须都支持[OID\_代\_中断\_审查](https://msdn.microsoft.com/library/windows/hardware/ff569590)OID。 如果微型端口驱动程序不支持中断裁决，驱动程序必须指定**NdisInterruptModerationNotSupported**中**InterruptModeration**的成员[ **NDIS\_中断\_审查\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff565793)结构。

NDIS 6.0 和更高版本的微型端口驱动程序必须支持这两个[OID\_代\_中断\_审查](https://msdn.microsoft.com/library/windows/hardware/ff569590)OID 设置和查询请求。 设置请求将定向微型端口驱动程序，若要启用或禁用中断裁决，并查询请求报告的中断裁决的当前状态。

支持中断裁决的微型端口驱动程序应启用此功能默认情况下除非**InterruptModeration**标准关键字在注册表中的禁用它。 有关标准关键字的详细信息，请参阅[网络设备的标准化 INF 关键字](standardized-inf-keywords-for-network-devices.md)。

 

 





