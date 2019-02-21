---
title: 转入睡眠状态
description: 转入睡眠状态
ms.assetid: cea326dd-7235-41a3-ad37-19549533a8dd
keywords:
- 网络接口卡 WDK 网络，转换的电源状态
- Nic WDK 网络，转换的电源状态
- 睡眠状态 WDK 网络
- 电源管理 WDK NDIS 微型端口转换的电源状态
- 设备电源状态 WDK 网络
- 电源状态 WDK 网络
- 转换电源状态 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d907d88524f9e1296ab817e7f8eae494e3175acd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542589"
---
# <a name="transitioning-to-a-sleeping-state"></a>转入睡眠状态





NDIS 如果微型端口驱动程序支持唤醒事件时，将驱动程序发送[OID\_PNP\_启用\_唤醒\_向上](https://msdn.microsoft.com/library/windows/hardware/ff569775)之前发送的请求[OID\_PNP\_设置\_电源](https://msdn.microsoft.com/library/windows/hardware/ff569780)请求。 有关详细信息，请参阅[启用唤醒事件](enabling-wake-up-events.md)。 微型端口驱动程序不得失败 OID\_PNP\_设置\_POWER 请求。

然后再返回 NDIS\_状态\_SUCCESS 作为响应为一个 OID\_PNP\_设置\_POWER 请求，微型端口驱动程序必须：

-   执行依赖于设备的操作所需的睡眠状态为准备的网络适配器。

-   保存任何数据包筛选器、 多播的地址、 当前的 MAC 地址，唤醒模式和网络适配器不能在睡眠状态中保留的任何其他硬件上下文。

-   禁用中断和网络适配器的 DMA 引擎。 微型端口驱动程序无法访问网络适配器硬件后网络适配器已设置为 D3 状态由总线驱动程序。

 

 





