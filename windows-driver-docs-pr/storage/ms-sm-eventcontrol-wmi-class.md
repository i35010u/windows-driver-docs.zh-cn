---
title: MS\_SM\_将 EventControl WMI 类
description: MS\_SM\_将 EventControl WMI 类
ms.assetid: d5c6a308-2782-4846-81f9-f4932d8caac6
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7fcaabce0bc75481e007dc1421f050356e72f7c6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566992"
---
# <a name="mssmeventcontrol-wmi-class"></a>MS\_SM\_将 EventControl WMI 类


MS\_SM\_将 EventControl WMI 类定义允许 WMI 客户端控件的链接、 端口和目标事件传递的 WMI 方法。 此 WMI 类都有无数据块。 因此，WMI 工具套件生成保存属于类的方法的参数数据结构的声明，但它不会生成对应于类本身在结构声明。

每个方法都属于此类的 MOF 语法所述的方法的参考页。 以下主题介绍了这些方法和其随附的结构：

[**SM\_AddTarget**](sm-addtarget.md)

[**SM\_RemoveTarget**](sm-removetarget.md)

[**SM\_AddPort**](sm-addport.md)

[**SM\_RemovePort**](sm-removeport.md)

[**SM\_AddLink**](sm-addlink.md)

[**SM\_RemoveLink**](sm-removelink.md)

MS\_SM\_将 EventControl 类定义，如下所示在*Hbaapi.mof*:

```cpp
class MS_SM_EventControl 
{ 
    [key] 
    string  InstanceName; 
    boolean Active; 

    //
    // These methods are used to control delivery of MS_SM_TargetEvents
//
    [ Implemented, WmiMethodId(1) ]
    void SM_AddTarget(
            [in, HBAType("HBA_WWN") ] uint8 HbaPortWWN[8],
            [in, HBAType("HBA_WWN") ] uint8 DiscoveredPortWWN[8],
            [in, HBAType("HBA_WWN") ] uint8 DomainPortWWN[8],
            [in ] uint32  AllTargets,
            [out, HBA_STATUS_QUALIFIERS ] HBA_STATUS HBAStatus
            );

    [ Implemented, WmiMethodId(2) ]
    void SM_RemoveTarget(
            [in, HBAType("HBA_WWN") ] uint8 HbaPortWWN[8],
            [in, HBAType("HBA_WWN") ] uint8 DiscoveredPortWWN[8],
            [in, HBAType("HBA_WWN") ] uint8 DomainPortWWN[8],
            [in ] uint32  AllTargets,
            [out, HBA_STATUS_QUALIFIERS ] HBA_STATUS HBAStatus
            );


//
// These methods are used to control delivery of MS_SM_PortEvents
//
    [ Implemented, WmiMethodId(3) ]
    void SM_AddPort(
            [in, HBAType("HBA_WWN") ] uint8 PortWWN[8],
            [in, EVENT_TYPES_QUALIFIERS ] uint32 EventType,
            [out, HBA_STATUS_QUALIFIERS ] HBA_STATUS HBAStatus
            );

    [ Implemented, WmiMethodId(4) ]
    void SM_RemovePort(
            [in, HBAType("HBA_WWN") ] uint8 PortWWN[8],
            [in, EVENT_TYPES_QUALIFIERS ] uint32 EventType,
            [out, HBA_STATUS_QUALIFIERS ] HBA_STATUS HBAStatus
            );

//
// These methods are used to control delivery of MSFC_LinkEvents
//
    [ Implemented, WmiMethodId(10) ]
    void SM_AddLink(
            [out, HBA_STATUS_QUALIFIERS ] HBA_STATUS HBAStatus
            );

    [ Implemented, WmiMethodId(11) ]
    void SM_RemoveLink(
            [out, HBA_STATUS_QUALIFIERS ] HBA_STATUS HBAStatus
            );
};
```

 

 





