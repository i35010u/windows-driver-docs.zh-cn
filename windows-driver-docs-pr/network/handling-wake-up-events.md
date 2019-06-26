---
title: 处理唤醒事件
description: 处理唤醒事件
ms.assetid: 4989d5a4-158c-41db-ab2d-fc995b67a822
keywords:
- 唤醒功能 WDK 网络，处理唤醒事件
- 总线特定唤醒行 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8823ff3c51a22d544424036b0165ca39701e91e9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381321"
---
# <a name="handling-wake-up-events"></a>处理唤醒事件





微型端口驱动程序不会处理检测到的 NIC 的唤醒事件 当 NIC 检测到已启用的唤醒事件时，因此要声明特定于总线的唤醒行。 电源管理器然后将 power IRP 发送到 NDIS，后者在响应中，将发送微型端口驱动程序[OID\_PNP\_设置\_POWER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)请求微型端口驱动程序放入 NIC 的 OIDhighest-powered (D0) 状态。

 

 





