---
title: 配对蓝牙协议
description: 配对蓝牙协议
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9f7b26310251aa82bad4dcbf5b1917eda5b9d9a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812777"
---
# <a name="pairingbluetooth-protocol"></a>配对：蓝牙协议


"配对：蓝牙" 协议是一种抽象方式，用于为蓝牙 OOB 配对结构抽象订阅。 Windows 订阅此类型是为了向提供商注册 Windows 对接收蓝牙 OOB 配对结构感兴趣的访问接口，以便完成邻近触发的蓝牙简单 OOB 配对。

**注意**  配对发布的行为：蓝牙未定义

 

**注意**  对于启用了 NFC 的 NFP 提供程序，静态连接 (静态连接切换单一蓝牙运营商和简化标记格式) 必须受支持。 不得支持协商连接切换。

 

### <a name="required-actions"></a>必需的措施

-   如果邻近技术被播发为 NFC，则驱动程序必须将 "配对：蓝牙" 协议的订阅与 NDEF 消息（其 TNF 字段值为0x02）和类型字段（等于 "application/vnd.apple.mpegurl"）匹配。

    驱动程序必须仅将 NDEF 记录的有效负载返回到此类型的订阅服务器。

-   如果近程技术被播发为 NFC，然后，该驱动程序还必须与 "配对： Bluetooth" 协议的订阅和 NDEF 消息匹配，其中第一个记录的 TNF 字段值为0x01，类型字段等于 "Hs"，另一条备用运营商记录指向 Bluetooth 运营商配置记录 (mime 类型 "application/vnd.apple.mpegurl" ) 。
    -   驱动程序必须仅将 "application/vnd.apple.mpegurl" NDEF 记录的负载返回到此类型的订阅服务器。
    -   驱动程序必须仅支持静态连接切换。 驱动程序不得支持连接切换中的其他机制，如协商连接切换。
    -   \[ \] 有关详细信息，请参阅 NFC BTSSP。
-   驱动程序可以支持发布 "配对：蓝牙" 类型。 对于 NFC，此发布格式是不确定的。
-   驱动程序还支持其他兼容方案。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](/windows-hardware/drivers/ddi/index)  
[近字段邻近 DDI 引用](/windows-hardware/drivers/ddi/index)
