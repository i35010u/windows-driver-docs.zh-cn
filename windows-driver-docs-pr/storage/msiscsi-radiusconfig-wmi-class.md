---
title: MSiSCSI \_ RADIUSCONFIG WMI 类
description: MSiSCSI \_ RADIUSCONFIG WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 79fdd8efa84815263696fa6cc3429355d0e46065
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796461"
---
# <a name="msiscsi_radiusconfig-wmi-class"></a>MSiSCSI \_ RADIUSCONFIG WMI 类


## <span id="ddk_msiscsi_radiusconfig_wmi_class_kr"></span><span id="DDK_MSISCSI_RADIUSCONFIG_WMI_CLASS_KR"></span>


MSiSCSI \_ RADIUSCONFIG WMI 类指示发起方是使用远程身份验证拨入用户服务 (RADIUS) ，并提供发起方在使用服务时所需的信息。

发起程序在质询握手身份验证协议 (CHAP) 的质询握手期间，使用 RADIUS 服务器执行身份验证。

如果小型端口驱动程序 \_ 管理的 HBA 支持使用 RADIUS 进行 CHAP 身份验证，则该驱动程序必须实现 MSiSCSI RADIUSConfig 类。

应尽可能使用 RADIUS，因为它允许对 CHAP 凭据进行集中管理。

由于 MSiSCSI \_ RADIUSCONFIG WMI 类与存储微型端口驱动程序的特定实例相关联，因此微型端口驱动程序必须使用微型端口驱动程序管理的特定物理设备对象 (PDO) 的名称注册该类。

MSiSCSI \_ RADIUSConfig 类是在 *配置* 中定义的。

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

当 WMI 工具套件编译上述类定义时，它会生成 [**MSiSCSI \_ RADIUSConfig**](/windows-hardware/drivers/ddi/iscsicfg/ns-iscsicfg-_msiscsi_radiusconfig) 数据结构。

 

