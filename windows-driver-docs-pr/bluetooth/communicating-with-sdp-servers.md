---
title: SDP 服务器概述与通信
description: SDP 服务器概述与通信
ms.assetid: 833f2eea-d7e6-4f19-979e-3bb4db47fa43
keywords:
- 蓝牙 WDK，SDP 服务器通信
- SDP WDK 蓝牙
- 服务发现协议 WDK 蓝牙
- 配置文件驱动程序 WDK 蓝牙
- 浏览服务 WDK 蓝牙
- 搜索服务 WDK 蓝牙
- 浏览 WDK 蓝牙的服务
- 广告服务 WDK 蓝牙
- 播发 WDK 蓝牙的服务
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40c08eb94e5f354f13533b875a2f3f5bf9326d56
ms.sourcegitcommit: 6f74454e7ed5e703e4e4b363b6816652950e6a51
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2019
ms.locfileid: "67608469"
---
# <a name="communicating-with-sdp-servers-overview"></a>SDP 服务器概述与通信


蓝牙驱动程序堆栈支持服务发现协议 (SDP)。 此协议允许配置文件驱动程序搜索或浏览提供的范围内的本地无线电收发器的蓝牙设备的服务。 SDP 作为其传输协议使用的逻辑链接控件和自适应协议 (L2CAP)，并遵循客户端-服务器模型。

服务是可以提供的信息、 执行的操作或代表另一个实体控制资源的任何实体。 服务可能会作为软件、 硬件或硬件和软件的组合。 服务记录完全包含的服务属性列表。

L2CAP server 配置文件驱动程序注册自己以接受传入 L2CAP 连接请求后，它可以通过使用播发其服务与 SDP 协议[ **IOCTL\_同时为\_SDP\_提交\_记录**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthioctl/ni-bthioctl-ioctl_bth_sdp_submit_record)或[ **IOCTL\_同时为\_SDP\_提交\_记录\_WITH\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthioctl/ni-bthioctl-ioctl_bth_sdp_submit_record_with_info)。 每个 SDP 记录以流的形式提交。 如果配置文件驱动程序将使用 IOCTL\_同时为\_SDP\_提交\_记录\_WITH\_信息，配置文件驱动程序的前面添加围绕[**同时为\_SDP\_记录**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthioctl/ns-bthioctl-_bth_sdp_record)包含不属于 SDP 的额外属性的原始流的结构记录本身。 其中包括请求的客户端的安全要求、 SDP 记录、 类的设备 (CoD) 信息、 记录和记录本身的长度的发布选项。

配置文件驱动程序已播发其服务后，其他蓝牙设备可以搜索或浏览这些服务。 SDP 服务的详细信息，请参阅[访问 SDP 服务信息](accessing-sdp-service-information.md)。

若要停止播发与 SDP 服务，配置文件驱动程序将使用[ **IOCTL\_同时为\_SDP\_删除\_记录**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthioctl/ni-bthioctl-ioctl_bth_sdp_remove_record)。

 

 





