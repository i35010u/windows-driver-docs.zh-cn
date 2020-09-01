---
title: DSM \_ 版本 WMI 类
description: DSM \_ 版本 WMI 类
ms.assetid: 79239921-169d-496d-a52b-f4b6b0cb0c80
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1a109c300bf43597fb3b0576d953f9c1e00eff6a
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186893"
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

 

