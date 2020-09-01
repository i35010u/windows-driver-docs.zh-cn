---
title: 导出 MiniportDevicePnPEventNotify 函数
description: 导出 MiniportDevicePnPEventNotify 函数
ms.assetid: 1c6dce4e-c452-48ce-b3c9-a3fb7842f060
keywords:
- 即插即用 WDK NDIS 微型端口，事件通知
- MiniportDevicePnPEventNotify
- 通知
- 通知 WDK PnP，NDIS 微型端口驱动程序
- 事件通知 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0fe2e6a49a4064fa675d221cc1d4cb393caee0f
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218422"
---
# <a name="exporting-a-miniportdevicepnpeventnotify-function"></a>导出 MiniportDevicePnPEventNotify 函数





NDIS 调用微型端口驱动程序的 [*MiniportDevicePnPEventNotify*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_device_pnp_event_notify) 函数，以通知以下即插即用 (PnP) 事件的微型端口驱动程序：

-   删除微型端口驱动程序控制的 NIC 的意外删除。

-   系统电源的更改。

如果微型端口驱动程序未导出 *MiniportDevicePnPEventNotify* 函数，NDIS 无法通知驱动程序这些 PnP 事件。

所有 NDIS 6.0 和更高版本的微型端口驱动程序都 *必须* 导出 *MiniportDevicePnPEventNotify* 函数。 此外，具有 WDM 下边缘的所有微型端口驱动程序都 *应* 导出 *MiniportDevicePnPEventNotify* 函数。

 

