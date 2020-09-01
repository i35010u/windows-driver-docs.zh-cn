---
title: MSiSCSI \_ DISCOVERYCONFIG WMI 类
description: MSiSCSI \_ DISCOVERYCONFIG WMI 类
ms.assetid: dbf170ba-92ab-47bd-a076-5f54129305a5
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c7480341925fba2570d6cb2c04cbfaa4e3affc53
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89193191"
---
# <a name="msiscsi_discoveryconfig-wmi-class"></a>MSiSCSI \_ DISCOVERYCONFIG WMI 类


## <span id="ddk_msiscsi_discoveryconfig_wmi_class_kr"></span><span id="DDK_MSISCSI_DISCOVERYCONFIG_WMI_CLASS_KR"></span>


MSiSCSI \_ DISCOVERYCONFIG WMI 类报告发起程序使用哪些方法来执行发现。

此类在 *配置*中定义为，如下所示。

```cpp
class MSiSCSI_DiscoveryConfig {
  [key] string  InstanceName;
  boolean  Active;
  [WmiDataId(1), read, write, description("HBA should
    perform target discovery via iSNS") : amended] 
    boolean  PerformiSNSDiscovery;
  [WmiDataId(2), read, write, description("HBA should 
    perform target discovery via SLP") : amended] 
    boolean  PerformSLPDiscovery;
  [WmiDataId(3), read, write, description("Automatic 
    discovery of iSNS server") : amended] 
    boolean  AutomaticiSNSDiscovery;
  [WmiDataId(4), read, write, MaxLen(256), 
    description("Default initiator name for registering with 
    iSNS") : amended] 
    string  InitiatorName;
  [WmiDataId(5), read, write, description("Fixed Addresses 
    of iSNS servers") : amended] 
    ISCSI_IP_Address  iSNSServer;
};
```

当 WMI 工具套件编译上述类定义时，它会生成 [**MSiSCSI \_ DiscoveryConfig**](/windows-hardware/drivers/ddi/iscsicfg/ns-iscsicfg-_msiscsi_discoveryconfig) 数据结构。

 

