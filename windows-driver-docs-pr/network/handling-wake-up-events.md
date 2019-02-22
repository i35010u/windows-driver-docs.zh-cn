---
title: 处理唤醒事件
description: 处理唤醒事件
ms.assetid: 4989d5a4-158c-41db-ab2d-fc995b67a822
keywords:
- 唤醒功能 WDK 网络，处理唤醒事件
- 总线特定唤醒行 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ba0a88f668f1de6d2a43f1cf94d0f135bbf9927
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556193"
---
# <a name="handling-wake-up-events"></a>处理唤醒事件





微型端口驱动程序不会处理检测到的 NIC 的唤醒事件 当 NIC 检测到已启用的唤醒事件时，因此要声明特定于总线的唤醒行。 电源管理器然后将 power IRP 发送到 NDIS，后者在响应中，将发送微型端口驱动程序[OID\_PNP\_设置\_POWER](https://msdn.microsoft.com/library/windows/hardware/ff569780)请求微型端口驱动程序放入 NIC 的 OIDhighest-powered (D0) 状态。

 

 





