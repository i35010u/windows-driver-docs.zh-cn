---
title: MSiSCSI\_BootConfiguration WMI 类
description: MSiSCSI\_BootConfiguration WMI 类
ms.assetid: 5ca350ba-8689-46c2-8313-8f523354db98
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: cb45546a4f2cdd22a8f319f2c404c0ca8fc28ab0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376693"
---
# <a name="msiscsibootconfiguration-wmi-class"></a>MSiSCSI\_BootConfiguration WMI 类


## <span id="ddk_msiscsi_bootconfiguration_wmi_class_kr"></span><span id="DDK_MSISCSI_BOOTCONFIGURATION_WMI_CLASS_KR"></span>


MSiSCSI\_BootConfiguration WMI 类描述了如何配置启动设备。

此类定义中，如下所示*Config.mof*。

```cpp
class MSiSCSI_BootConfiguration {
  [key] string  InstanceName;
  boolean  Active;
  [read, write, WmiDataId(1), Description("LUN on target of 
    boot device") : amended, DisplayName("Target LUN") : 
    amended] 
    uint64  LUN;
  [read, write, WmiDataId(2), SECURITY_FLAG_QUALIFIERS] 
    ISCSI_SECURITY_FLAGS  SecurityFlags;
  [read, write, WmiDataId(3), description("Size in bytes of 
    Target Username") : amended] 
    uint32  UsernameSize;
  [read, write, WmiDataId(4), description("Size in bytes of 
    Target Password") : amended] 
    uint32  PasswordSize;
  [read, write, WmiDataId(5), description("If TRUE 
    dynamically discover boot device") : amended] 
    boolean  DiscoverBootDevice;
  [read, write, WmiDataId(6), MaxLen(MAX_ISCSI_NAME_LEN), 
    description("The InitiatorNode specifies the iScsi name 
    of the initiator node to use for the connection. If 
    empty, then the HBA can choose any initiator node") : 
    amended] 
    string  InitiatorNode;
  [read, write, WmiDataId(7), MaxLen(MAX_ISCSI_NAME_LEN), 
    description("TargetName specifies the iScsi target name 
    to which a session should be established.") : amended] 
    string TargetName;
  [read, write, WmiDataId(8), description("Portal to use for 
    initial connection") : amended] 
    ISCSI_TargetPortal  TargetPortal;
  [read, write, WmiDataId(9), description("Login options") : 
    amended] 
    ISCSI_LoginOptions  LoginOptions;
  [read, write, WmiDataId(10), WmiSizeIs("UsernameSize"),
    description("Authentication Username, for CHAP this 
    is the CHAP Name (CHAP_N) when authenticating the 
    target") : amended] 
    uint8  Username[];
  [read, write, WmiDataId(11), WmiSizeIs("PasswordSize"), 
    description("Authentication Password, for CHAP this is 
    the shared secret to use when generating the response to 
    the target challenge") : amended] 
    uint8  Password[];
};
```

当 WMI 工具套件编译前面的类定义时，它会生成[ **MSiSCSI\_BootConfiguration** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iscsicfg/ns-iscsicfg-_msiscsi_bootconfiguration)数据结构。

 

 





