---
title: MS\_SMHBA\_SAS\_端口 WMI 类
description: MS\_SMHBA\_SAS\_端口 WMI 类
ms.assetid: d3528212-f884-4db8-aadc-eb4ca15814da
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d32fd65f39bf2bd23c3e6f0980f074ce3fef5cd8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386131"
---
# <a name="mssmhbasasport-wmi-class"></a>MS\_SMHBA\_SAS\_端口 WMI 类


支持存储管理 API 的 HBA 微型端口驱动程序使用 MS\_SMHBA\_SAS\_Port 类来公开与 SAS 端口相关联的属性。 应为每个端口的此类的一个实例。

MS\_SMHBA\_SAS\_端口类定义，如下所示在*Hbaapi.mof*:

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

此类定义编译时通过 WMI 工具套件，它会生成以下数据结构：

[**MS\_SMHBA\_SAS\_端口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_ms_smhba_sas_port)

没有与此 WMI 类相关联的方法。

 

 





