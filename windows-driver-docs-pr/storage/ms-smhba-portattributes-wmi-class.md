---
title: MS \_ SMHBA \_ PORTATTRIBUTES WMI 类
description: MS \_ SMHBA \_ PORTATTRIBUTES WMI 类
ms.assetid: 26f17443-cb89-4c93-9b67-35acb75b6d03
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 601b9a3d808ec789e2924875ecfe8e49b333b5c1
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188811"
---
# <a name="ms_smhba_portattributes-wmi-class"></a>MS \_ SMHBA \_ PORTATTRIBUTES WMI 类


支持存储管理 API 的 HBA 微型端口驱动程序使用 MS \_ SMHBA \_ PORTATTRIBUTES 类公开端口属性。 每个端口都应有此类的一个实例。

MS \_ SMHBA \_ PORTATTRIBUTES 类在 *Hbaapi*中定义如下：

```cpp
class MS_SMHBA_PORTATTRIBUTES 
{
    [HBA_PORTTYPE_QUALIFIERS, WmiDataId(1)]
    uint32 PortType;

    [HBA_PORTSTATE_QUALIFIERS, WmiDataId(2)]
    uint32 PortState;

    [WmiDataId(3),
     Description("Size of MS_SMHBA_SAS_Port or MS_SMHBA_FC_Port")
    ]
    uint32 PortSpecificAttributesSize;

    [MaxLen(256), WmiDataId(4)]
    string OSDeviceName;

    [WmiDataId(5)]
    uint64 Reserved;

    [WmiDataId(6),
     Description(" MS_SMHBA_SAS_Port or MS_SMHBA_FC_Port Buffer"),
     WmiSizeIs("PortSpecificAttributesSize")
    ]
    uint8 PortSpecificAttributes[];
};
```

当 WMI 工具套件编译此类定义时，它将生成以下数据结构：

[**MS \_ SMHBA \_ PORTATTRIBUTES**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_ms_smhba_portattributes)

没有与此 WMI 类相关联的方法。

 

