---
title: MSiSCSI \_ DISCOVERYCONFIG WMI 类
description: MSiSCSI \_ DISCOVERYCONFIG WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a2729c6a57ba7a38222d6afe6b4c34bd69c4cdd9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785523"
---
# <a name="msiscsi_discoveryconfig-wmi-class"></a>MSiSCSI \_ DISCOVERYCONFIG WMI 类


## <span id="ddk_msiscsi_discoveryconfig_wmi_class_kr"></span><span id="DDK_MSISCSI_DISCOVERYCONFIG_WMI_CLASS_KR"></span>


MSiSCSI \_ DISCOVERYCONFIG WMI 类报告发起程序使用哪些方法来执行发现。

此类在 *配置* 中定义为，如下所示。

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

 

