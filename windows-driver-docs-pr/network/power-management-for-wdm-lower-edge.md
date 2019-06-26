---
title: WDM 下边缘的电源管理
description: WDM 下边缘的电源管理
ms.assetid: e4504206-b303-4623-bb10-a19acbcede03
keywords:
- NDIS WDM 微型端口驱动程序 WDK 网络、 电源管理
- NDIS 微型端口驱动程序 WDK 联网、 电源管理的下边缘
- WDM 低边缘 WDK 网络、 电源管理
- 电源管理 WDK 网络 NDIS WDM 微型端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a938c6dc419ca9d6591015b73fe86c0b3d0a601b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386854"
---
# <a name="power-management-for-wdm-lower-edge"></a>WDM 下边缘的电源管理





NDIS 处理所有插即用 (PnP) 和电源管理 Irp NDIS WDM 微型端口驱动程序。 因此，NDIS WDM 微型端口驱动程序应响应 PnP 和电源管理 Oid，根据设备功能，如中所述[NDIS 微型端口驱动程序的电源管理](https://docs.microsoft.com/windows-hardware/drivers/network/power-management--ndis-6-0-and-ndis-6-1-)。 有关这些 Oid 的详细信息，请参阅[（NDIS 6.0 和更高版本） 的电源管理](https://docs.microsoft.com/windows-hardware/drivers/network/power-management--ndis-6-0-and-ndis-6-1-)。

 

 





