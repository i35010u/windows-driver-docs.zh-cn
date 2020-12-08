---
title: DSM \_ 版本 WMI 类
description: DSM \_ 版本 WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 980636c95885a7df1d8f3d5307349c7ccbf69de1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804645"
---
# <a name="dsm_version-wmi-class"></a>DSM \_ 版本 WMI 类


MPIO 驱动程序使用 DSM \_ 版本 WMI 类标识已配置的 DSM 的版本。

```cpp
class DSM_VERSION
{
    //
    // Version: Major, Minor, Product, Qfe
    //
    [WmiDataId(1)] uint32 MajorVersion;
    [WmiDataId(2)] uint32 MinorVersion;
    [WmiDataId(3)] uint32 ProductBuild;
    [WmiDataId(4)] uint32 QfeNumber;

};
```

当 WMI 工具套件编译此类定义时，它将生成 [**DSM \_ 版本**](/windows-hardware/drivers/ddi/mpiowmi/ns-mpiowmi-_dsm_version) 数据结构。 没有与此 WMI 类相关联的方法。

 

