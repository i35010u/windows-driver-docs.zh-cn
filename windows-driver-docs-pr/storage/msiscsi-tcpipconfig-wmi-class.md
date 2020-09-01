---
title: MSiSCSI \_ TCPIPCONFIG WMI 类
description: MSiSCSI \_ TCPIPCONFIG WMI 类
ms.assetid: 57451576-a900-4eaa-b229-bda79a81d014
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3a99bc03af79e9c9c247b1aa9d313596b27184d0
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184941"
---
# <a name="msiscsi_tcpipconfig-wmi-class"></a>MSiSCSI \_ TCPIPCONFIG WMI 类


## <span id="ddk_msiscsi_tcpipconfig_wmi_class_kr"></span><span id="DDK_MSISCSI_TCPIPCONFIG_WMI_CLASS_KR"></span>


MSiSCSI \_ TCPIPCONFIG WMI 类报告有关某个 HBA IP 地址的 tcp/ip 配置信息。

适配器的微型端口驱动程序应为适配器支持的每个 IP 地址创建此类的一个实例。

由于 MSiSCSI \_ TCPIPConfig 类与存储微型端口驱动程序的特定实例相关联，因此微型端口驱动程序必须使用微型端口驱动程序管理的特定物理设备对象 (PDO) 的名称注册该类。

MSiSCSI \_ TCPIPConfig 类是在 *配置*中定义的。

```cpp
class MSiSCSI_TCPIPConfig {
  [key] string  InstanceName;
  boolean  Active;
  [read, write, WmiDataId(1), DisplayName("Use Link Local 
    Address") : amended, description("TRUE if the HBA should 
    use a link local address as its ip address") : amended] 
    boolean  UseLinkLocalAddress;
  [read, write, WmiDataId(2), displayName("DHCP Enabled") : 
    amended, description("TRUE if the HBA should use DHCP") 
    : amended] 
    boolean  EnableDHCP;
  [read, WmiDataId(3), description("IP Versions supported") 
    : amended, 
    BitValues{ "IPV4", "IPV6"},
    BitMap{"0x00000001", "0x00000002"}] 
    uint32  IPVersions;
  [read, write, WmiDataId(4), DisplayName("Static IP 
    Address") : amended, description("Static IP address for 
    the HBA") : amended]
    ISCSI_IP_Address  StaticIpAddress;
  [read, write, WmiDataId(5), DisplayName("Default Gateway") 
    : amended, Description("Static Default Gateway IP 
    address") : amended]
    ISCSI_IP_Address  DefaultGateway;
  [read, write, WmiDataId(6), DisplayName("Subnet Mask") : 
    amended, Description("Static Subnet Mask") : amended] 
    ISCSI_IP_Address  SubnetMask;
  [read, write, WmiDataId(7), DisplayName("Preferred DNS 
    Server") : amended, Description("Preferred DNS Server") 
    : amended] 
    ISCSI_IP_Address  PreferredDNSServer;
  [read, write, WmiDataId(8), DisplayName("Alternate DNS 
    Server") : amended, Description("Alternate DNS Server") 
    : amended] 
    ISCSI_IP_Address  AlternateDNSServer;
};
```

当 WMI 工具套件编译上述类定义时，它会生成 [**MSiSCSI \_ TCPIPConfig**](/windows-hardware/drivers/ddi/iscsicfg/ns-iscsicfg-_msiscsi_tcpipconfig) 数据结构。

 

