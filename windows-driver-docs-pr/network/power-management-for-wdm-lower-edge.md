---
title: WDM 下边缘的电源管理
description: WDM 下边缘的电源管理
ms.assetid: e4504206-b303-4623-bb10-a19acbcede03
keywords:
- NDIS-WDM 微型端口驱动程序 WDK 网络，电源管理
- NDIS 微型端口驱动程序的下边缘 WDK 网络，电源管理
- WDM 低边缘 WDK 网络，电源管理
- 电源管理 WDK 网络，NDIS-WDM 微型端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4dacbdaea2c5158f96731fe4b9a9dbf1ace8dff
ms.sourcegitcommit: db9d058a9e592d4c47c67fc14f04f0ddc3aa92af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/13/2020
ms.locfileid: "91989851"
---
# <a name="power-management-for-wdm-lower-edge"></a>WDM 下边缘的电源管理





NDIS 处理所有即插即用 (PnP) 和电源管理 Irp，用于 NDIS-WDM 微型端口驱动程序。 因此，NDIS-WDM 微型端口驱动程序应根据设备功能响应 PnP 和电源管理 Oid，如 [Ndis 微型端口驱动程序的电源管理](required-and-optional-oids-for-power-management.md)中所述。

 

 





