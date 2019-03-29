---
title: 处理 OID_PNP_SET_POWER OID
description: 处理 OID_PNP_SET_POWER OID
ms.assetid: 6140c772-57ba-47d3-b294-a2e2b2e3ccc7
keywords:
- OID_PNP_SET_POWER_OID
- 网络接口卡 WDK 网络，转换的电源状态
- 网络适配器 WDK 网络，转换的电源状态
- 电源管理 WDK NDIS 微型端口转换的电源状态
- 设备电源状态 WDK 网络
- 电源状态 WDK 网络
- 转换电源状态 WDK 网络
- 唤醒功能 WDK 网络，转换的电源状态
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b2f607ba5ed502cc18ba821076dd7ca6624089a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563969"
---
# <a name="handling-an-oidpnpsetpower-oid"></a>处理 OID\_PNP\_设置\_POWER OID





NDIS 发送的 OID 请求[OID\_PNP\_设置\_POWER](https://msdn.microsoft.com/library/windows/hardware/ff569780)通知微型端口驱动程序，网络适配器将会进行转换从睡眠状态的工作状态或处于休眠状态状态设置为处于工作状态。 OID\_PNP\_设置\_电源请求可以在加[OID\_PNP\_查询\_POWER](https://msdn.microsoft.com/library/windows/hardware/ff569778)请求。

本部分包括：

[转入睡眠状态](transitioning-to-a-sleeping-state.md)

[转换到的工作状态](transitioning-to-the-working-state.md)

 

 





