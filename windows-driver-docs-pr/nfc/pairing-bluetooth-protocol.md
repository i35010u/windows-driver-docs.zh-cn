---
title: 配对的蓝牙协议
description: 配对的蓝牙协议
ms.assetid: 6C95CA57-A226-4252-91E2-FAD8F1A0432B
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f185a04d31ab54d2931a97a774e23c41643b0852
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348566"
---
# <a name="pairingbluetooth-protocol"></a>配对：蓝牙协议


"配对： 蓝牙"协议是一种抽象出来也一点蓝牙 OOB 配对结构的订阅。 Windows 订阅以向 Windows 感兴趣接收配对结构才能完成邻近触发蓝牙简单 OOB 配对的蓝牙 OOB 的提供程序注册此类型。

**请注意**  蓝牙配对： 发布的行为是未定义

 

**请注意**  同时定义格式的 NFC 启用 NFP 提供程序必须支持 （静态连接移交单一蓝牙承运人和简化的标记格式）。 协商的连接移交必须不受支持。

 

### <a name="required-actions"></a>所需的操作

-   如果邻近技术公布为 NFC，驱动程序必须匹配与 NDEF 消息具有 0x02 TNF 字段值和类型字段，它等于"application/vnd.bluetooth.ep.oob"的"配对： 蓝牙"协议的订阅。

    该驱动程序必须返回到此类型的订阅服务器仅 NDEF 记录的有效负载。

-   邻近技术被公布为 NFC，则该驱动程序也必须匹配与其中第一条记录具有 TNF 字段值 0x01 NDEF 消息的"配对： 蓝牙"协议的订阅，如果某一类型字段，它等于"Hs"和一个单个的替代方法运营商指向蓝牙运营商配置记录 （mime 类型"application/vnd.bluetooth.ep.oob"） 的记录。
    -   该驱动程序必须返回到此类型的订阅服务器仅"application/vnd.bluetooth.ep.oob"NDEF 记录的有效负载。
    -   该驱动程序必须仅支持静态连接移交。 驱动程序都不能支持如协商连接移交连接移交中的其他机制。
    -   请参阅\[NFC BTSSP\]有关详细信息。
-   该驱动程序可能支持的"配对： 蓝牙"类型的发布。 此发布格式未定义的 NFC。
-   该驱动程序可能支持其他兼容的方案。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
[邻近 DDI 引用附近](https://msdn.microsoft.com/library/windows/hardware/jj866056)  

