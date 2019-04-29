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
ms.openlocfilehash: 8398ab93e6ab9208cc25954ba94a9575cccd5e73
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385487"
---
# <a name="exporting-a-miniportdevicepnpeventnotify-function"></a>导出 MiniportDevicePnPEventNotify 函数





NDIS 调用微型端口驱动程序[ *MiniportDevicePnPEventNotify* ](https://msdn.microsoft.com/library/windows/hardware/ff559369)函数，以通知以下插即用 (PnP) 事件的微型端口驱动程序：

-   微型端口驱动程序控制的 NIC 被意外删除。

-   系统的电源中的更改。

如果微型端口驱动程序不会导出*MiniportDevicePnPEventNotify*函数，NDIS 无法通知这些即插即用事件驱动程序。

所有 NDIS 6.0 和更高版本的微型端口驱动程序*必须*导出*MiniportDevicePnPEventNotify*函数。 此外，所有微型端口驱动程序具有 WDM 降低边缘*应*导出*MiniportDevicePnPEventNotify*函数。

 

 





