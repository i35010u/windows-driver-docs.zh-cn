---
title: MS\_SMHBA\_PROTOCOLSTATISTICS WMI 类
description: MS\_SMHBA\_PROTOCOLSTATISTICS WMI 类
ms.assetid: 718ae583-254d-4807-b8e2-5eb39017c097
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2b09709ef965b8d88bcc3ce40dd4925230e45c67
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386137"
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

[**MS\_SMHBA\_PROTOCOLSTATISTICS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_ms_smhba_protocolstatistics)

没有与此 WMI 类相关联的方法。

 

 





