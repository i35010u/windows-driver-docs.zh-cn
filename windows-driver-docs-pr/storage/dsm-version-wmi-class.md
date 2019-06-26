---
title: DSM\_版本 WMI 类
description: DSM\_版本 WMI 类
ms.assetid: 79239921-169d-496d-a52b-f4b6b0cb0c80
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e4531e63b1cb50233987f6dc187acf7a988399ad
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384682"
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

此类定义编译时通过 WMI 工具套件，它会生成[ **DSM\_版本**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mpiowmi/ns-mpiowmi-_dsm_version)数据结构。 没有与此 WMI 类相关联的方法。

 

 





