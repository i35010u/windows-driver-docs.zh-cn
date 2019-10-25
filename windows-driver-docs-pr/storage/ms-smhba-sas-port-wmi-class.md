---
title: MS\_SMHBA\_SAS\_端口 WMI 类
description: MS\_SMHBA\_SAS\_端口 WMI 类
ms.assetid: d3528212-f884-4db8-aadc-eb4ca15814da
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a8ae3e75fbf04d6c323dd57624f7d8e530b30185
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844528"
---
# <a name="ms_smhba_sas_port-wmi-class"></a>MS\_SMHBA\_SAS\_端口 WMI 类


支持存储管理 API 的 HBA 微型端口驱动程序使用 MS\_SMHBA\_SAS\_Port 类公开与 SAS 端口关联的属性。 每个端口都应有此类的一个实例。

MS\_SMHBA\_SAS\_端口类在*Hbaapi*中定义如下：

```cpp
class MS_SMHBA_SAS_Port 
{
    [HBAType("HBA_SASPORTPROTOCOL"), WmiDataId(1)]
    uint32  PortProtocol;

    [HBAType("HBA_WWN"), WmiDataId(2)]
    uint8   LocalSASAddress[8];

    [HBAType("HBA_WWN"), WmiDataId(3)]
    uint8   AttachedSASAddress[8];

    [WmiDataId(4)]
    uint32  NumberofDiscoveredPorts;

    [WmiDataId(5)]
    uint32  NumberofPhys;
};
```

当 WMI 工具套件编译此类定义时，它将生成以下数据结构：

[**MS\_SMHBA\_SAS\_端口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_ms_smhba_sas_port)

没有与此 WMI 类相关联的方法。

 

 





