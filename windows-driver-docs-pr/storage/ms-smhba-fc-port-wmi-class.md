---
title: MS\_SMHBA\_FC\_端口 WMI 类
description: MS\_SMHBA\_FC\_端口 WMI 类
ms.assetid: 671f14e4-c591-4df2-85a1-2db3f802ef5e
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1149f715e6818d3f05e983d128a85c7438fe733c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544809"
---
# <a name="mssmhbafcport-wmi-class"></a>MS\_SMHBA\_FC\_端口 WMI 类


支持存储管理 API 的 HBA 微型端口驱动程序使用 MS\_SMHBA\_FC\_Port 类公开相关联的光纤通道适配器的端口属性。 应为每个端口的此类的一个实例。

MS\_SMHBA\_FC\_端口类定义，如下所示在*Hbaapi.mof*:

```cpp
class MS_SMHBA_FC_Port 
{
    [HBAType("HBA_WWN"), WmiDataId(1)]
    uint8   NodeWWN[8];

    [HBAType("HBA_WWN"), WmiDataId(2)]
    uint8   PortWWN[8];

    [WmiDataId(3)]
    uint32  FcId;

    [HBAType("HBA_COS"), WmiDataId(4)]
    uint32  PortSupportedClassofService;

    [HBAType("HBA_FC4TYPES"), WmiDataId(5)]
    uint8   PortSupportedFc4Types[32];

    [HBAType("HBA_FC4TYPES"), WmiDataId(6)]
    uint8   PortActiveFc4Types[32];

    [HBAType("HBA_WWN"), WmiDataId(7)]
    uint8   FabricName[8];

    [WmiDataId(8)]
    uint32  NumberofDiscoveredPorts;

    [WmiDataId(9)] 
    uint8   NumberofPhys;

    [MaxLen(256), WmiDataId(10)]
    string  PortSymbolicName;
};
```

此类定义编译时通过 WMI 工具套件，它会生成以下数据结构：

[**MS\_SMHBA\_FC\_端口**](https://msdn.microsoft.com/library/windows/hardware/ff563162)

没有与此 WMI 类相关联的方法。

 

 





