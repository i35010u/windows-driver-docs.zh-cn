---
title: 访问 SDP 服务信息
description: 访问 SDP 服务信息
ms.assetid: 0b327fbd-1101-4566-ac2f-3d039eed6835
keywords:
- 蓝牙 WDK、SDP 服务器通信
- SDP WDK 蓝牙
- 服务发现协议 WDK 蓝牙
- 浏览服务 WDK 蓝牙
- 搜索服务 WDK 蓝牙
- 服务浏览 WDK 蓝牙
- IOCTL_BTH_SDP_CONNECT
- 搜索 SDP 记录 WDK 蓝牙
- IOCTL_BTH_SDP_SERVICE_SEARCH
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ca62609fff56107cda23cde78948b0286378674
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90010591"
---
# <a name="accessing-sdp-service-information"></a>访问 SDP 服务信息


配置文件驱动程序提交服务发现协议后 (SDP) 记录使用 SDP 播发其服务，其他设备可以通过专门搜索该记录或通过浏览找到该记录来发现这些服务。

若要搜索 SDP 记录，客户端配置文件驱动程序必须首先使用 [**IOCTL \_ BTH \_ SDP \_ connect**](/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_sdp_connect) 连接到远程设备的 SDP 服务。

然后，配置文件驱动程序可以使用以下 IOCTLs 之一来执行实际的 SDP 记录搜索：

-   [**IOCTL \_BTH \_ SDP \_ 特性 \_ 搜索**](/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_sdp_attribute_search) 获取属于指定 SDP 属性范围的远程 SDP 记录的所有组件。

-   [**IOCTL \_BTH \_ sdp \_ 服务 \_ 搜索**](/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_sdp_service_search) 向远程设备发出 sdp 请求，请求处理特定服务类的 sdp 记录。

-   [**IOCTL \_BTH \_ SDP \_ 服务 \_ 特性 \_ 搜索**](/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_sdp_service_attribute_search) 将 IOCTL \_ BTH \_ sdp \_ 特性 \_ 搜索和 ioctl \_ BTH \_ SDP \_ 服务 \_ 属性 \_ 搜索结合起来，并在单个操作中返回可用的 SDP 记录流。

配置文件驱动程序可以使用 IOCTL \_ BTH \_ sdp \_ 服务 \_ 搜索和 ioctl \_ BTH \_ Sdp \_ 特性 \_ 搜索来减少通过蓝牙链接传输的 SDP 流量，并通过使用少量的最大传输单位 (mtu) 来提取必要的信息。 如果这两个问题都不太重要，则配置文件驱动程序可以更方便地调用 IOCTL \_ BTH \_ SDP \_ 服务 \_ 属性 \_ 搜索。

在配置文件驱动程序获取 *动态* 协议/服务多路复用器 (PSM) 用于所需服务后，可以使用 **BRB \_ L2CA \_ 开放 \_ 通道** BRB 连接到远程服务。

**注意**   如果服务具有固定的 PSM，其中很多都是，则 L2CAP 客户端配置文件驱动程序无需使用 SDP 来获取 PSM。 但是，L2CAP 客户端配置文件驱动程序仍可以使用 SDP 来获取 SDP 服务器特性。

 

当配置文件驱动程序完成搜索时，它应使用 [**IOCTL \_ BTH \_ SDP \_ 断开连接**](/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_sdp_disconnect) 从远程 SDP 服务器断开连接。

 

