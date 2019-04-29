---
title: MS\_SMHBA\_PORTATTRIBUTES WMI 类
description: MS\_SMHBA\_PORTATTRIBUTES WMI 类
ms.assetid: 26f17443-cb89-4c93-9b67-35acb75b6d03
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 60c045db6de116d45e23cc505e314d6ee547d126
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380352"
---
# <a name="mssmhbaportattributes-wmi-class"></a>MS\_SMHBA\_PORTATTRIBUTES WMI 类


支持存储管理 API 的 HBA 微型端口驱动程序使用 MS\_SMHBA\_PORTATTRIBUTES 类公开的端口属性。 应为每个端口的此类的一个实例。

MS\_SMHBA\_PORTATTRIBUTES 类定义，如下所示在*Hbaapi.mof*:

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

此类定义编译时通过 WMI 工具套件，它会生成以下数据结构：

[**MS\_SMHBA\_PORTATTRIBUTES**](https://msdn.microsoft.com/library/windows/hardware/ff563165)

没有与此 WMI 类相关联的方法。

 

 





