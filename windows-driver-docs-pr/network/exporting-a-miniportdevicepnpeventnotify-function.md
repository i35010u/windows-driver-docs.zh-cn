---
title: 导出 MiniportDevicePnPEventNotify 函数
description: 导出 MiniportDevicePnPEventNotify 函数
ms.assetid: 1c6dce4e-c452-48ce-b3c9-a3fb7842f060
keywords:
- 即插即用和播放 WDK NDIS 微型端口，事件通知
- MiniportDevicePnPEventNotify
- 通知
- 通知即插即用，WDK NDIS 微型端口驱动程序
- 事件通知 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca306701c973e56aba974cb88613a32a96eaf667
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373349"
---
# <a name="exporting-a-miniportdevicepnpeventnotify-function"></a>导出 MiniportDevicePnPEventNotify 函数





NDIS 调用微型端口驱动程序[ *MiniportDevicePnPEventNotify* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_device_pnp_event_notify)函数，以通知以下插即用 (PnP) 事件的微型端口驱动程序：

-   微型端口驱动程序控制的 NIC 被意外删除。

-   系统的电源中的更改。

如果微型端口驱动程序不会导出*MiniportDevicePnPEventNotify*函数，NDIS 无法通知这些即插即用事件驱动程序。

所有 NDIS 6.0 和更高版本的微型端口驱动程序*必须*导出*MiniportDevicePnPEventNotify*函数。 此外，所有微型端口驱动程序具有 WDM 降低边缘*应*导出*MiniportDevicePnPEventNotify*函数。

 

 





