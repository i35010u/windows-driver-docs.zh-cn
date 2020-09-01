---
title: MSiSCSI \_ SECURITYCAPABILITIES WMI 类
description: MSiSCSI \_ SECURITYCAPABILITIES WMI 类
ms.assetid: 50f7aa98-0743-4775-808b-c5a90dc1d0fe
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 411549740c3082a16400e061491fe7bc8d1df644
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184939"
---
# <a name="msiscsi_securitycapabilities-wmi-class"></a>MSiSCSI \_ SECURITYCAPABILITIES WMI 类


## <span id="ddk_msiscsi_securitycapabilities_wmi_class_kr"></span><span id="DDK_MSISCSI_SECURITYCAPABILITIES_WMI_CLASS_KR"></span>


MSiSCSI \_ SECURITYCAPABILITIES WMI 类描述了发起方的安全功能。

如果小型端口驱动程序 \_ 管理的 HBA 支持 IPsec，则它必须实现 MSiSCSI SecurityCapabilities 类。

由于 MSiSCSI \_ SecurityCapabilities 类与存储微型端口驱动程序的特定实例相关联，因此微型端口驱动程序必须使用微型端口驱动程序管理的特定物理设备对象 (PDO) 的名称注册该类。

MSiSCSI \_ SecurityCapabilities 类是在 *配置*中定义的。

```cpp
class MSiSCSI_SecurityCapabilities {
  [key] string  InstanceName;
  boolean  Active;
  [read, DisplayName("Protect iSCSI") : amended, 
    WmiDataId(1), description("TRUE if the HBA can use IPsec 
    to protect iSCSI traffic") : amended]
    boolean  ProtectiScsiTraffic;
  [read, WmiDataId(2), DisplayName("Protect iSNS") : 
    amended, description("TRUE if the HBA can use IPsec to 
    protect iSNS traffic") : amended] 
    boolean  ProtectiSNSTraffic;
  [read, WmiDataId(3), DisplayName("Certificates Supported") 
    : amended, description("TRUE if HBA supports 
    certificates") : amended] 
    boolean  CertificatesSupported;
  [read, WmiDataId(4), DisplayName("Encryption Types 
    Available") : amended, description("Count of encryption 
    types available")] 
    uint32  EncryptionAvailableCount;
  [read, WmiDataId(5), 
    WmiSizeIs("EncryptionAvailableCount"), 
    ENCRYPTION_TYPES_QUALIFIERS, DisplayName("Encryption 
    Types") : amended] 
    uint32  EncryptionAvailable[];
};
```

当 WMI 工具套件编译上述类定义时，它会生成 [**MSiSCSI \_ SecurityCapabilities**](/windows-hardware/drivers/ddi/iscsicfg/ns-iscsicfg-_msiscsi_securitycapabilities) 数据结构。

 

