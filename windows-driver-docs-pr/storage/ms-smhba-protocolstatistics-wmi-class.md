---
title: MS \_ SMHBA \_ PROTOCOLSTATISTICS WMI 类
description: MS \_ SMHBA \_ PROTOCOLSTATISTICS WMI 类
ms.assetid: 718ae583-254d-4807-b8e2-5eb39017c097
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2714667aa9d0419e80f5a130f1c6200ad97bce11
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189041"
---
# <a name="ms_smhba_protocolstatistics-wmi-class"></a>MS \_ SMHBA \_ PROTOCOLSTATISTICS WMI 类


支持存储管理 API 的 HBA 微型端口驱动程序使用 MS \_ SMHBA \_ PROTOCOLSTATISTICS 类来公开流量统计信息。

MS \_ SMHBA \_ PROTOCOLSTATISTICS 类在 *Hbaapi*中定义如下：

```cpp
class MS_SMHBA_PROTOCOLSTATISTICS
{
    [WmiDataId(1)]
    sint64 SecondsSinceLastReset;

    [WmiDataId(2)]
    sint64 InputRequests;

    [WmiDataId(3)]
    sint64 OutputRequests;

    [WmiDataId(4)]
    sint64 ControlRequests;

    [WmiDataId(5)]
    sint64 InputMegabytes;

    [WmiDataId(6)]
    sint64 OutputMegabytes;
};
```

当 WMI 工具套件编译此类定义时，它将生成以下数据结构：

[**MS \_ SMHBA \_ PROTOCOLSTATISTICS**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_ms_smhba_protocolstatistics)

没有与此 WMI 类相关联的方法。

 

