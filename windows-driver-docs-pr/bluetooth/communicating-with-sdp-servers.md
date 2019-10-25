---
title: “与 SDP 服务器进行通信”概述
description: “与 SDP 服务器进行通信”概述
ms.assetid: 833f2eea-d7e6-4f19-979e-3bb4db47fa43
keywords:
- 蓝牙 WDK、SDP 服务器通信
- SDP WDK 蓝牙
- 服务发现协议 WDK 蓝牙
- 配置文件驱动程序 WDK 蓝牙
- 浏览服务 WDK 蓝牙
- 搜索服务 WDK 蓝牙
- 服务浏览 WDK 蓝牙
- 广告服务 WDK 蓝牙
- 服务广告 WDK 蓝牙
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73e2acf2f525ea25bd849ca2500ff6a1988280f0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832122"
---
# <a name="communicating-with-sdp-servers-overview"></a>“与 SDP 服务器进行通信”概述


蓝牙驱动程序堆栈支持服务发现协议（SDP）。 此协议允许配置文件驱动程序搜索或浏览本地收音机范围内的蓝牙设备提供的服务。 SDP 使用逻辑链接控制和适配协议（L2CAP）作为其传输协议，并遵循客户端-服务器模型。

服务是指可以提供信息、执行操作或代表其他实体控制资源的任何实体。 服务可以作为软件、硬件或硬件和软件的组合实现。 服务记录完全由服务属性列表组成。

在 L2CAP 服务器配置文件驱动程序将自身注册为接受传入 L2CAP 连接请求后，它可以通过使用[**IOCTL\_BTH\_sdp\_提交\_记录**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_sdp_submit_record)或 IOCTL 来使用 sdp 协议播发其服务[ **\_BTH\_SDP\_提交\_记录\_\_的信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_sdp_submit_record_with_info)。 每个 SDP 记录都作为流提交。 如果配置文件驱动程序使用 IOCTL\_BTH\_SDP\_使用\_信息提交\_记录\_，则配置文件驱动程序会在原始流前面加上一个[**BTH\_SDP\_记录**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ns-bthioctl-_bth_sdp_record)结构，它包含不属于 SDP 记录本身的额外特性。 其中包括请求客户端的安全要求、SDP 记录的发布选项、设备的设备（货条）信息、记录的长度和记录本身。

配置文件驱动程序播发其服务后，其他蓝牙设备可以搜索或浏览这些服务。 有关 SDP 服务的详细信息，请参阅[访问 Sdp 服务信息](accessing-sdp-service-information.md)。

若要使用 SDP 停止播发服务，配置文件驱动程序使用[**IOCTL\_BTH\_SDP\_删除\_记录**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_sdp_remove_record)。

 

 





