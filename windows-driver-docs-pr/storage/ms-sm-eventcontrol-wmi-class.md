---
title: MS \_ SM \_ EventControl WMI 类
description: MS \_ SM \_ EventControl WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 996b03c575ced8dc0a80964b0b7e542123452bd7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811537"
---
# <a name="ms_sm_eventcontrol-wmi-class"></a>MS \_ SM \_ EventControl WMI 类


MS \_ SM \_ EventControl wmi 类定义 wmi 方法，这些方法允许 wmi 客户端控制链接、端口和目标事件的传送。 此 WMI 类没有数据块。 因此，WMI 工具套件将为包含属于类的方法的参数数据的结构生成声明，但不会生成对应于类本身的结构声明。

此类的每个方法的 MOF 语法在方法的参考页中进行了介绍。 以下主题介绍了这些方法及其随附的结构：

[**SM \_ AddTarget**](sm-addtarget.md)

[**SM \_ RemoveTarget**](sm-removetarget.md)

[**SM \_ AddPort**](sm-addport.md)

[**SM \_ RemovePort**](sm-removeport.md)

[**SM \_ AddLink**](sm-addlink.md)

[**SM \_ RemoveLink**](sm-removelink.md)

MS \_ SM \_ EventControl 类在 *Hbaapi* 中定义如下：

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

 

 





