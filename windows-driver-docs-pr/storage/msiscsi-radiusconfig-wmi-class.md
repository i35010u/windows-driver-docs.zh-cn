---
title: MSiSCSI\_RADIUSConfig WMI 类
description: MSiSCSI\_RADIUSConfig WMI 类
ms.assetid: e0fd1fea-3d8c-4d25-a9fd-0e115ecb8163
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a13d03ea3fd135742721563b5f16bdd33df42cf2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575715"
---
# <a name="msiscsiradiusconfig-wmi-class"></a>MSiSCSI\_RADIUSConfig WMI 类


## <span id="ddk_msiscsi_radiusconfig_wmi_class_kr"></span><span id="DDK_MSISCSI_RADIUSCONFIG_WMI_CLASS_KR"></span>


MSiSCSI\_RADIUSConfig WMI 类表示发起程序是否使用远程身份验证拨入用户服务 (RADIUS) 和提供发起方需要使用此服务的信息。

发起程序使用 RADIUS 服务器来执行身份验证质询握手过程的质询握手身份验证协议 (CHAP)。

微型端口驱动程序必须实现 MSiSCSI\_RADIUSConfig 类，如果它所管理的 HBA 支持使用 RADIUS 的 CHAP 身份验证。

应该使用 RADIUS 只要有可能，因为它允许集中的管理的 CHAP 凭据。

因为 MSiSCSI\_RADIUSConfig WMI 类与存储微型端口驱动程序的特定实例相关联，则微型端口驱动程序必须注册使用特定的物理设备对象 (PDO) 的名称的类的微型端口驱动程序管理。

MSiSCSI\_RADIUSConfig 类中定义*Config.mof*。

```cpp
class MSiSCSI_RADIUSConfig {
  [key] string  InstanceName;
  boolean  Active;
  [WmiDataId(1), read, write, description("HBA should use 
    RADIUS for CHAP authentication") : amended] 
    boolean  UseRADIUSForCHAP;
  [WmiDataId(2), read, write, description("Size in bytes of 
    shared secret for RADIUS servers") : amended] 
    uint32  SharedSecretSizeInBytes;
  [WmiDataId(3), read, write, description("Fixed Addresses 
    of RADIUS server") : amended] 
    ISCSI_IP_Address  RADIUSServer;
  [WmiDataId(4), read, write, description("Fixed Addresses 
    of backup RADIUS server") : amended] 
    ISCSI_IP_Address  BackupRADIUSServer;
  [WmiDataId(5), read, write, 
    WmiSizeIs("SharedSecretSizeInBytes"), 
    description("Shared secret for RADIUS servers") :
    amended] 
    uint8 SharedSecret[];
};
```

当 WMI 工具套件编译前面的类定义时，它会生成[ **MSiSCSI\_RADIUSConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff563112)数据结构。

 

 





