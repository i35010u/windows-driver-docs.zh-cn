---
title: WDI_EXTENDED_TID
description: 本主题介绍 WDI 微型端口驱动程序的 WDI_EXTENDED_TID 数据类型。
keywords:
- WDI_EXTENDED_TID，WDK WDI_EXTENDED_TID 网络驱动程序
ms.date: 11/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: a5d70d5d19d2513250978e2c62ee3bdeee138112
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822765"
---
# <a name="wdi_extended_tid"></a>WDI_EXTENDED_TID

WDI_EXTENDED_TID 的数据类型是一个 UINT8 值，该值定义了 (TID) 的流量标识符。

```c++
typedef UINT8 WDI_EXTENDED_TID;
```

## <a name="remarks"></a>备注

可能的值如下：

| “值” | 描述 |
| --- | --- |
| 0-15 | 802.11 TIDs |
| 16 (WDI_EXT_TID_NON_QOS)  | 非 QoS 数据 |
| 17-24 | 保留以与 IHV 注入的帧一起使用。 在时间间隔17-24 中具有扩展 TID 的帧被视为比在相同间隔17-24 中具有较小扩展 TID 的帧的优先级高。 |
| 25-30 | 未使用的值 |
| 31 (WDI_EXT_TID_UNKNOWN)  | 未知/未指定 |

## <a name="requirements"></a>要求

**支持的最低客户端**： Windows 10

**支持的最低服务器**： Windows server 2016

**标头**： Dot11wdi


