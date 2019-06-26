---
title: MSiSCSI\_SecurityCapabilities WMI 类
description: MSiSCSI\_SecurityCapabilities WMI 类
ms.assetid: 50f7aa98-0743-4775-808b-c5a90dc1d0fe
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2e6f7a3932ada476e569ca7736cffeef408462f1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384668"
---
# <a name="msiscsisecuritycapabilities-wmi-class"></a>MSiSCSI\_SecurityCapabilities WMI 类


## <span id="ddk_msiscsi_securitycapabilities_wmi_class_kr"></span><span id="DDK_MSISCSI_SECURITYCAPABILITIES_WMI_CLASS_KR"></span>


MSiSCSI\_SecurityCapabilities WMI 类描述了发起方的安全功能。

微型端口驱动程序必须实现 MSiSCSI\_SecurityCapabilities 类如果它所管理的 HBA 支持 IPsec。

因为 MSiSCSI\_SecurityCapabilities 类与存储微型端口驱动程序的特定实例相关联，则微型端口驱动程序必须注册使用特定的物理设备对象 (PDO) 的名称的类的微型端口驱动程序管理。

MSiSCSI\_SecurityCapabilities 类中定义*Config.mof*。

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

当 WMI 工具套件编译前面的类定义时，它会生成[ **MSiSCSI\_SecurityCapabilities** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iscsicfg/ns-iscsicfg-_msiscsi_securitycapabilities)数据结构。

 

 





