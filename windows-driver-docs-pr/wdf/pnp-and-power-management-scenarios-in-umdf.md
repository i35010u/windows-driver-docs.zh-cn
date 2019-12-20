---
title: UMDF 中的 PnP 和电源管理方案
description: UMDF 中的 PnP 和电源管理方案
ms.assetid: ca36eee5-482c-4cfe-a515-be9d3743e241
keywords:
- 即插即用在 UMDF 中的电源管理方案
- PnP WDK UMDF，UMDF 中的电源管理方案
- 电源管理方案 WDK UMDF
- 电源管理方案 WDK UMDF、PnP
- 电源管理方案 WDK UMDF，即插即用
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05550cf1b07b460426dbc45e44112a1f4b45dd6b
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210869"
---
# <a name="pnp-and-power-management-scenarios-in-umdf"></a>UMDF 中的 PnP 和电源管理方案


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

以下 PnP 和电源管理方案显示了框架调用 UMDF 驱动程序的事件回调函数的顺序：

-   [用户插入设备](a-user-plugs-in-a-device-umdf.md)
-   [断开设备的用户](a-user-unplugs-a-device-umdf.md)
-   [设备进入低功耗状态](a-device-enters-a-low-power-state-umdf.md)
-   [设备返回到其工作状态](a-device-returns-to-its-working-state-umdf.md)
-   [PnP 管理器重新分发系统资源](the-pnp-manager-redistributes-system-resources-umdf.md)

有关 KMDF 驱动程序的 PnP 和电源管理回调序列的信息，请参阅[pnp 和电源管理回拨顺序](pnp-and-power-management-callback-sequences.md)。

 

 





