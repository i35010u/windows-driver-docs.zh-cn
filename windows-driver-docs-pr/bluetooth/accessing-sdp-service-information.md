---
title: 访问 SDP 服务信息
description: 访问 SDP 服务信息
ms.assetid: 0b327fbd-1101-4566-ac2f-3d039eed6835
keywords:
- 蓝牙 WDK，SDP 服务器通信
- SDP WDK 蓝牙
- 服务发现协议 WDK 蓝牙
- 浏览服务 WDK 蓝牙
- 搜索服务 WDK 蓝牙
- 浏览 WDK 蓝牙的服务
- IOCTL_BTH_SDP_CONNECT
- 记录进行搜索 SDP WDK 蓝牙
- IOCTL_BTH_SDP_SERVICE_SEARCH
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eef2577892006b8b6f0ac561c2934ab879dcd26f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354042"
---
# <a name="accessing-sdp-service-information"></a>访问 SDP 服务信息


配置文件驱动程序提交服务发现协议 (SDP) 记录以播发其服务与 SDP 后，其他设备可以发现这些服务通过专用于该记录搜索或通过浏览找到它。

若要搜索的 SDP 记录，客户端配置文件驱动程序必须先使用[ **IOCTL\_同时为\_SDP\_CONNECT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthioctl/ni-bthioctl-ioctl_bth_sdp_connect)以连接到远程设备 SDP 服务。

配置文件驱动程序可以然后使用以下 Ioctl 之一进行实际 SDP 记录搜索：

-   [**IOCTL\_同时为\_SDP\_特性\_搜索**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthioctl/ni-bthioctl-ioctl_bth_sdp_attribute_search)获取在指定的 SDP 属性范围内的所有组件的远程 SDP 记录。

-   [**IOCTL\_同时为\_SDP\_服务\_搜索**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthioctl/ni-bthioctl-ioctl_bth_sdp_service_search)到远程设备，请求的句柄的特定服务类或类 SDP 记录发出一个 SDP 请求。

-   [**IOCTL\_同时为\_SDP\_服务\_特性\_搜索**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthioctl/ni-bthioctl-ioctl_bth_sdp_service_attribute_search)结合了 IOCTL\_同时为\_SDP\_属性\_搜索和 IOCTL\_同时为\_SDP\_服务\_特性\_搜索并返回可用 SDP 记录在单个操作中流式传输。

配置文件驱动程序可以使用 IOCTL\_同时为\_SDP\_服务\_搜索和 IOCTL\_同时为\_SDP\_特性\_搜索来减少的 SDP 流量通过蓝牙链接传输，并可以通过使用少量的最大传输单位 (Mtu) 提取必要的信息。 如果这些问题都不太重要，它可以更方便的配置文件驱动程序来调用 IOCTL\_同时为\_SDP\_服务\_特性\_搜索。

在配置文件后，驱动程序已获取*动态*协议/服务所需服务的多路复用器 (PSM)，它可以通过使用连接到远程服务**BRB\_L2CA\_打开\_通道**BRB。

**请注意**  如果服务有哪些多执行操作，固定的 PSM L2CAP 客户端配置文件驱动程序不需要使用 SDP 获取 PSM。 但是，L2CAP 客户端配置文件驱动程序仍可以使用 SDP 以获取 SDP 服务器属性。

 

完成配置文件驱动程序搜索后，它应使用[ **IOCTL\_同时为\_SDP\_断开连接**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthioctl/ni-bthioctl-ioctl_bth_sdp_disconnect)断开与远程 SDP 服务器的连接。

 

 





