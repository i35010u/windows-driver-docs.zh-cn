---
title: MSiSCSI\_NICConfig WMI 类
description: MSiSCSI\_NICConfig WMI 类
ms.assetid: 9b7a466d-a9bb-41c5-8f38-e5baf21e863a
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1893b7a4731cf1d84325acf3db56149b8dcf841d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845341"
---
# <a name="msiscsi_nicconfig-wmi-class"></a>MSiSCSI\_NICConfig WMI 类


## <span id="ddk_msiscsi_nicconfig_wmi_class_kr"></span><span id="DDK_MSISCSI_NICCONFIG_WMI_CLASS_KR"></span>


MSiSCSI\_NICConfig WMI 类描述网络接口卡（NIC）端口。

HBA 发起程序的微型端口驱动程序必须为 HBA 上的每个端口创建一个 MSiSCSI\_NICConfig 类的实例。

MSiSCSI\_NICConfig 类是在*配置*中定义的。

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

当 WMI 工具套件编译上述类定义时，它会生成[**MSiSCSI\_NICConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsicfg/ns-iscsicfg-_msiscsi_nicconfig)数据结构。

 

 





