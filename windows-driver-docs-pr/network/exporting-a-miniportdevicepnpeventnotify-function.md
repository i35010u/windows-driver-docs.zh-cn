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
ms.openlocfilehash: 9e416d8b709f2228280d3f6bce1d009322c6e3ce
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838112"
---
# <a name="exporting-a-miniportdevicepnpeventnotify-function"></a>导出 MiniportDevicePnPEventNotify 函数





NDIS 调用微型端口驱动程序的[*MiniportDevicePnPEventNotify*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_device_pnp_event_notify)函数，以通知小型端口驱动程序以下即插即用（PnP）事件：

-   删除微型端口驱动程序控制的 NIC 的意外删除。

-   系统电源的更改。

如果微型端口驱动程序未导出*MiniportDevicePnPEventNotify*函数，NDIS 无法通知驱动程序这些 PnP 事件。

所有 NDIS 6.0 和更高版本的微型端口驱动程序都*必须*导出*MiniportDevicePnPEventNotify*函数。 此外，具有 WDM 下边缘的所有微型端口驱动程序都*应*导出*MiniportDevicePnPEventNotify*函数。

 

 





