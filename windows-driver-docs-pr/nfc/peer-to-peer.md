---
title: 对等
ms.assetid: 0234BA57-477E-408C-94C8-8DD8922FD386
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
description: 定义对等标准 NFC 论坛有关的信息，确保设备的协议可以使用 NFC 进行交互。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c0272feb0fd890058c34c911742fb0155b9c466
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348409"
---
# <a name="peer-to-peer"></a>对等


若要确保两个设备均可使用 NFC 进行交互，该驱动程序必须传输和接收数据通过以下 NFC 论坛定义对等标准和协议：

-   LLCP v1.1
-   SNEP v1.0

## <a name="driver-requirements"></a>驱动程序要求


驱动程序必须支持运行通过 LLCP 交换 NDEF 消息的默认 SNEP 服务器：

-   远程 P2P 设备到达时，驱动程序必须建立与远程设备的默认 SNEP 服务器 （后跟"DeviceArrived"订阅触发） 的客户端 SNEP 连接。
-   该驱动程序还必须能够接受其默认 SNEP 服务器从远程设备的 SNEP 客户端连接上的连接。
-   接收 SNEP 服务器上的所有 NDEF 消息必须都转换为消息类型，如本文档中定义。
-   要发布的所有消息类型必须转换为 NDEF 消息并发送到远程设备，如上文所定义。 传输消息时，一旦[ **IOCTL\_NFP\_获取\_下一步\_传输\_消息**](https://msdn.microsoft.com/library/windows/hardware/jj853320)中定义完成本文档中。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
[邻近 DDI 引用附近](https://msdn.microsoft.com/library/windows/hardware/jj866056)  
