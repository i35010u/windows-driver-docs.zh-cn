---
title: MSiSCSI \_ NICCONFIG WMI 类
description: MSiSCSI \_ NICCONFIG WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5ff1e7d3506f92e9090d244cb605db0ad205a4d2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788241"
---
# <a name="msiscsi_nicconfig-wmi-class"></a>MSiSCSI \_ NICCONFIG WMI 类


## <span id="ddk_msiscsi_nicconfig_wmi_class_kr"></span><span id="DDK_MSISCSI_NICCONFIG_WMI_CLASS_KR"></span>


MSiSCSI \_ NICCONFIG WMI 类描述网络接口卡 (NIC) 端口。

HBA 发起程序的微型端口驱动程序必须 \_ 为 hba 上的每个端口创建一个 MSiSCSI NICConfig 类的实例。

MSiSCSI \_ NICConfig 类是在 *配置* 中定义的。

```cpp
class MSiSCSI_NICConfig {
  [key] string  InstanceName;
  boolean  Active;
  [read, WmiDataId(1), DisplayName("Link Speed") : amended, 
    Description("Speed of network link in megabits per 
    second") : amended] 
    uint32  LinkSpeed;
  [read, WmiDataId(2), DisplayName("Max Link Speed") : 
    amended, Description("Maximum Speed of network link in 
    megabits per second") : amended] 
    uint32  MaxLinkSpeed;
  [read, WmiDataId(3), DisplayName("Link State") : amended, 
    description("Link State") : amended, 
    Values{"Media Disconnected", "Media Connected"} : 
    amended,
    ValueMap{"0", "1"}] 
    uint32  LinkState;
  [read, WmiDataId(4), DisplayName("Max Frame Size") : 
    amended, description("Maximum frame size") : amended] 
    uint32  MaxFrameSize;
  [read, WmiDataId(5), DisplayName("MAC Address") : amended, 
    description("Ethernet MAC Address") : amended] 
    uint8  MacAddress[6];
};
```

当 WMI 工具套件编译上述类定义时，它会生成 [**MSiSCSI \_ NICConfig**](/windows-hardware/drivers/ddi/iscsicfg/ns-iscsicfg-_msiscsi_nicconfig) 数据结构。

 

