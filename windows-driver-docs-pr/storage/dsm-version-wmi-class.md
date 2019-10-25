---
title: DSM\_WMI 类的版本
description: DSM\_WMI 类的版本
ms.assetid: 79239921-169d-496d-a52b-f4b6b0cb0c80
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 974bfede7fe9b9476c7b94dc0fed6dc3e99e69fe
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844562"
---
# <a name="dsm_version-wmi-class"></a>DSM\_WMI 类的版本


MPIO 驱动程序使用 DSM\_版本 WMI 类来标识已配置的 DSM 的版本。

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

当 WMI 工具套件编译此类定义时，它将生成[**DSM\_版本**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mpiowmi/ns-mpiowmi-_dsm_version)数据结构。 没有与此 WMI 类相关联的方法。

 

 





