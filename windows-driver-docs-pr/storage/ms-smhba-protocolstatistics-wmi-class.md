---
title: MS\_SMHBA\_PROTOCOLSTATISTICS WMI 类
description: MS\_SMHBA\_PROTOCOLSTATISTICS WMI 类
ms.assetid: 718ae583-254d-4807-b8e2-5eb39017c097
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d9a944f9b572fc5f1b585edeebf45b9c8015e270
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566451"
---
# <a name="mssmhbaprotocolstatistics-wmi-class"></a>MS\_SMHBA\_PROTOCOLSTATISTICS WMI 类


支持存储管理 API 的 HBA 微型端口驱动程序使用 MS\_SMHBA\_PROTOCOLSTATISTICS 类公开的流量统计信息。

MS\_SMHBA\_PROTOCOLSTATISTICS 类定义，如下所示在*Hbaapi.mof*:

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

此类定义编译时通过 WMI 工具套件，它会生成以下数据结构：

[**MS\_SMHBA\_PROTOCOLSTATISTICS**](https://msdn.microsoft.com/library/windows/hardware/ff563172)

没有与此 WMI 类相关联的方法。

 

 





