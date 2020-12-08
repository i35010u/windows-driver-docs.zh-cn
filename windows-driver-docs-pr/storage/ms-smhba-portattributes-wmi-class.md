---
title: MS \_ SMHBA \_ PORTATTRIBUTES WMI 类
description: MS \_ SMHBA \_ PORTATTRIBUTES WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 6bad739823ce595812d17e38d69d61a13891650d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811505"
---
# <a name="ms_smhba_portattributes-wmi-class"></a>MS \_ SMHBA \_ PORTATTRIBUTES WMI 类


支持存储管理 API 的 HBA 微型端口驱动程序使用 MS \_ SMHBA \_ PORTATTRIBUTES 类公开端口属性。 每个端口都应有此类的一个实例。

MS \_ SMHBA \_ PORTATTRIBUTES 类在 *Hbaapi* 中定义如下：

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

 

