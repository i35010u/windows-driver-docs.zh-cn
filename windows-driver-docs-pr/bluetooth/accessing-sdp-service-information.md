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
ms.openlocfilehash: ba84a61be48ad4af19f514fd20cb4ca722805f03
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833878"
---
# <a name="accessing-sdp-service-information"></a>访问 SDP 服务信息


在配置文件驱动程序提交服务发现协议（SDP）记录以便使用 SDP 播发其服务后，其他设备可以通过专门搜索该记录或通过浏览找到该记录来发现这些服务。

若要搜索 SDP 记录，客户端配置文件驱动程序必须先使用[**IOCTL\_BTH\_SDP\_连接**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_sdp_connect)才能连接到远程设备的 SDP 服务。

然后，配置文件驱动程序可以使用以下 IOCTLs 之一来执行实际的 SDP 记录搜索：

-   [**IOCTL\_BTH\_SDP\_属性\_搜索**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_sdp_attribute_search)获取属于指定 SDP 属性范围的远程 SDP 记录的所有组件。

-   [**IOCTL\_BTH\_SDP\_服务\_搜索**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_sdp_service_search)向远程设备发出 sdp 请求，请求处理特定服务类或类的 sdp 记录。

-   [**Ioctl\_BTH\_SDP\_服务\_特性\_搜索**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_sdp_service_attribute_search)将 IOCTL\_BTH\_SDP\_特性\_搜索和 IOCTL\_BTH\_\_14_ 特性\_搜索，并在单个操作中返回可用的 SDP 记录流。

配置文件驱动程序可以使用 IOCTL\_BTH\_SDP\_服务\_搜索和 IOCTL\_BTH\_SDP\_属性\_搜索以减少通过蓝牙链接传输的 SDP 流量，并可提取使用少量最大传输单位（Mtu）所需的信息。 如果这两个问题都不太重要，则配置文件驱动程序可以更方便地调用 IOCTL\_BTH\_SDP\_服务\_属性\_搜索。

在配置文件驱动程序已获取所需服务的*动态*协议/服务多路复用器（PSM）后，它可以使用**BRB\_L2CA\_打开\_通道**BRB 连接到远程服务。

**请注意**  如果服务具有固定的 PSM，其中很多都是，L2CAP 客户端配置文件驱动程序无需使用 SDP 来获取 PSM。 但是，L2CAP 客户端配置文件驱动程序仍可以使用 SDP 来获取 SDP 服务器特性。

 

当配置文件驱动程序完成搜索时，它应使用[**IOCTL\_BTH\_SDP\_断开**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_sdp_disconnect)连接以断开与远程 SDP 服务器的连接。

 

 





