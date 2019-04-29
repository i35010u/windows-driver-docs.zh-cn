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
ms.openlocfilehash: 44259d0f3fa403ebf13adf5efac801013bf46734
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380081"
---
# <a name="power-management-for-wdm-lower-edge"></a>WDM 下边缘的电源管理





NDIS 处理所有插即用 (PnP) 和电源管理 Irp NDIS WDM 微型端口驱动程序。 因此，NDIS WDM 微型端口驱动程序应响应 PnP 和电源管理 Oid，根据设备功能，如中所述[NDIS 微型端口驱动程序的电源管理](https://msdn.microsoft.com/library/windows/hardware/hh205399)。 有关这些 Oid 的详细信息，请参阅[（NDIS 6.0 和更高版本） 的电源管理](https://msdn.microsoft.com/library/windows/hardware/hh205399)。

 

 





