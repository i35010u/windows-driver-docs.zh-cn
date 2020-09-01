---
title: MS \_ SMHBA \_ SAS \_ 端口 WMI 类
description: MS \_ SMHBA \_ SAS \_ 端口 WMI 类
ms.assetid: d3528212-f884-4db8-aadc-eb4ca15814da
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 0894355eb375180d4551abf0de6e0fadaba3bd46
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186423"
---
# <a name="ms_smhba_sas_port-wmi-class"></a>MS \_ SMHBA \_ SAS \_ 端口 WMI 类


支持存储管理 API 的 HBA 微型端口驱动程序使用 MS \_ SMHBA \_ SAS \_ 端口类公开与 SAS 端口关联的属性。 每个端口都应有此类的一个实例。

\_ \_ 在 Hbaapi 中，MS SMHBA SAS \_ 端口类定义如下*Hbaapi.mof*：

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

[**MS \_ SMHBA \_ SAS \_ 端口**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_ms_smhba_sas_port)

没有与此 WMI 类相关联的方法。

 

