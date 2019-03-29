---
title: DSM\_版本 WMI 类
description: DSM\_版本 WMI 类
ms.assetid: 79239921-169d-496d-a52b-f4b6b0cb0c80
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 51db53f70e3bd6d6e60a68c32b7c81ce0cc23ff1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569111"
---
# <a name="dsmversion-wmi-class"></a>DSM\_版本 WMI 类


MPIO 驱动程序使用 DSM\_版本 WMI 类来确定已配置的 DSM 的版本。

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

此类定义编译时通过 WMI 工具套件，它会生成[ **DSM\_版本**](https://msdn.microsoft.com/library/windows/hardware/ff552750)数据结构。 没有与此 WMI 类相关联的方法。

 

 





