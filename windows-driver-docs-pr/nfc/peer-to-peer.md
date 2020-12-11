---
title: 对等
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
description: 有关 NFC 论坛定义的对等标准和协议的信息，可确保设备能够使用 NFC 进行交互。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64bd025d1886e72364304d520ae7d842ad6c0375
ms.sourcegitcommit: e47bd7eef2c2b89e3417d7f2dceb7c03d894f3c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2020
ms.locfileid: "97091020"
---
# <a name="peer-to-peer"></a>对等


为了确保两个设备能够使用 NFC 进行交互，驱动程序必须通过以下 NFC 论坛定义的对等标准和协议来传输和接收数据：

-   LLCP 1.1 版
-   SNEP v1。0

## <a name="driver-requirements"></a>驱动程序要求


驱动程序必须支持在 LLCP 上运行的默认 SNEP 服务器以交换 NDEF 消息：

-   在远程 P2P 设备到达时，驱动程序必须与远程设备的默认 SNEP 服务器建立客户端 SNEP 连接 (然后) 触发 "DeviceArrived" 订阅。
-   驱动程序还必须能够从远程设备的 SNEP 客户端连接接受其默认 SNEP 服务器上的连接。
-   在 SNEP 服务器上收到的所有 NDEF 消息必须按照本文档中的定义转换为消息类型。
-   要发布的所有消息类型必须转换为 NDEF 消息，并按上述定义发送到远程设备。 传输消息后，将按照本文档中的定义完成 [**IOCTL \_ NFP \_ 获取 \_ 下一次 \_ 传输的 \_ 消息**](/windows-hardware/drivers/ddi/nfpdev/ni-nfpdev-ioctl_nfp_get_next_transmitted_message) 。

 

 
## <a name="related-topics"></a>相关主题
[近现场通信 (NFC) API 参考](/windows-hardware/drivers/ddi/_nfpdrivers/)
