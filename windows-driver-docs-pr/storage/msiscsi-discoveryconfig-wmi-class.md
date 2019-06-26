---
title: MSiSCSI\_DiscoveryConfig WMI 类
description: MSiSCSI\_DiscoveryConfig WMI 类
ms.assetid: dbf170ba-92ab-47bd-a076-5f54129305a5
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 99d1578588bc237f011ec94abb949db76a0e7000
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379699"
---
# <a name="msiscsidiscoveryconfig-wmi-class"></a>MSiSCSI\_DiscoveryConfig WMI 类


## <span id="ddk_msiscsi_discoveryconfig_wmi_class_kr"></span><span id="DDK_MSISCSI_DISCOVERYCONFIG_WMI_CLASS_KR"></span>


MSiSCSI\_DiscoveryConfig WMI 类报告哪些方法发起程序使用来执行发现操作。

此类定义中，如下所示*Config.mof*。

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

当 WMI 工具套件编译前面的类定义时，它会生成[ **MSiSCSI\_DiscoveryConfig** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iscsicfg/ns-iscsicfg-_msiscsi_discoveryconfig)数据结构。

 

 





