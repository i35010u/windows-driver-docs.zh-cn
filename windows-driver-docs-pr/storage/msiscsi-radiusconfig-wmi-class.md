---
title: MSiSCSI\_RADIUSConfig WMI 类
description: MSiSCSI\_RADIUSConfig WMI 类
ms.assetid: e0fd1fea-3d8c-4d25-a9fd-0e115ecb8163
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5e1e2175576e2a0af894b77716e391d96cb328bc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845332"
---
# <a name="msiscsi_radiusconfig-wmi-class"></a>MSiSCSI\_RADIUSConfig WMI 类


## <span id="ddk_msiscsi_radiusconfig_wmi_class_kr"></span><span id="DDK_MSISCSI_RADIUSCONFIG_WMI_CLASS_KR"></span>


MSiSCSI\_RADIUSConfig WMI 类指示发起程序是否使用远程身份验证拨入用户服务（RADIUS）并提供发起方在使用服务时所需的信息。

发起程序在质询握手身份验证协议（CHAP）的质询握手期间，使用 RADIUS 服务器来执行身份验证。

如果小型端口驱动程序管理的 HBA 支持使用 RADIUS 进行 CHAP 身份验证，则该驱动程序必须实现 MSiSCSI\_RADIUSConfig 类。

应尽可能使用 RADIUS，因为它允许对 CHAP 凭据进行集中管理。

由于 MSiSCSI\_RADIUSConfig WMI 类与存储微型端口驱动程序的特定实例相关联，因此微型端口驱动程序必须使用微型端口驱动程序管理的特定物理设备对象（PDO）的名称来注册该类。

MSiSCSI\_RADIUSConfig 类是在*配置*中定义的。

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

当 WMI 工具套件编译上述类定义时，它会生成[**MSiSCSI\_RADIUSConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsicfg/ns-iscsicfg-_msiscsi_radiusconfig)数据结构。

 

 





