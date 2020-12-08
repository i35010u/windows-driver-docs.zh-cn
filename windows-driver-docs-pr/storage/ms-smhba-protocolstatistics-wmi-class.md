---
title: MS \_ SMHBA \_ PROTOCOLSTATISTICS WMI 类
description: MS \_ SMHBA \_ PROTOCOLSTATISTICS WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d5e70b0e1399f8ebca1e3e08a10ab0f8178032b5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811501"
---
# <a name="ms_smhba_protocolstatistics-wmi-class"></a>MS \_ SMHBA \_ PROTOCOLSTATISTICS WMI 类


支持存储管理 API 的 HBA 微型端口驱动程序使用 MS \_ SMHBA \_ PROTOCOLSTATISTICS 类来公开流量统计信息。

MS \_ SMHBA \_ PROTOCOLSTATISTICS 类在 *Hbaapi* 中定义如下：

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

 

