---
title: MS\_SMHBA\_PROTOCOLSTATISTICS WMI 类
description: MS\_SMHBA\_PROTOCOLSTATISTICS WMI 类
ms.assetid: 718ae583-254d-4807-b8e2-5eb39017c097
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e95e12b788a175fc0441e3c1b462527e0e746dd9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844532"
---
# <a name="ms_smhba_protocolstatistics-wmi-class"></a>MS\_SMHBA\_PROTOCOLSTATISTICS WMI 类


支持存储管理 API 的 HBA 微型端口驱动程序使用 MS\_SMHBA\_PROTOCOLSTATISTICS 类来公开流量统计信息。

MS\_SMHBA\_PROTOCOLSTATISTICS 类在*Hbaapi*中定义如下：

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

[**MS\_SMHBA\_PROTOCOLSTATISTICS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_ms_smhba_protocolstatistics)

没有与此 WMI 类相关联的方法。

 

 





