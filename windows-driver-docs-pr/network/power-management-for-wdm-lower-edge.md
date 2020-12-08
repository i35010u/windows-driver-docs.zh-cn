---
title: WDM 下边缘的电源管理
description: WDM 下边缘的电源管理
keywords:
- NDIS-WDM 微型端口驱动程序 WDK 网络，电源管理
- NDIS 微型端口驱动程序的下边缘 WDK 网络，电源管理
- WDM 低边缘 WDK 网络，电源管理
- 电源管理 WDK 网络，NDIS-WDM 微型端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 355eef8058e16f5b219388cac475b37125147539
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836305"
---
# <a name="power-management-for-wdm-lower-edge"></a>WDM 下边缘的电源管理





NDIS 处理所有即插即用 (PnP) 和电源管理 Irp，用于 NDIS-WDM 微型端口驱动程序。 因此，NDIS-WDM 微型端口驱动程序应根据设备功能响应 PnP 和电源管理 Oid，如 [Ndis 微型端口驱动程序的电源管理](required-and-optional-oids-for-power-management.md)中所述。

 

 





