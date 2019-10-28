---
title: MSiSCSI\_TCPIPConfig WMI 类
description: MSiSCSI\_TCPIPConfig WMI 类
ms.assetid: 57451576-a900-4eaa-b229-bda79a81d014
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1b3015ced1d92ab7ea3094412965b62c17260093
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840629"
---
# <a name="msiscsi_tcpipconfig-wmi-class"></a>MSiSCSI\_TCPIPConfig WMI 类


## <span id="ddk_msiscsi_tcpipconfig_wmi_class_kr"></span><span id="DDK_MSISCSI_TCPIPCONFIG_WMI_CLASS_KR"></span>


MSiSCSI\_TCPIPConfig WMI 类报告有关某个 HBA IP 地址的 TCP/IP 配置信息。

适配器的微型端口驱动程序应为适配器支持的每个 IP 地址创建此类的一个实例。

由于 MSiSCSI\_TCPIPConfig 类与存储微型端口驱动程序的特定实例相关联，因此微型端口驱动程序必须使用微型端口驱动程序管理的特定物理设备对象（PDO）的名称来注册该类。

MSiSCSI\_TCPIPConfig 类是在*配置*中定义的。

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

当 WMI 工具套件编译上述类定义时，它会生成[**MSiSCSI\_TCPIPConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsicfg/ns-iscsicfg-_msiscsi_tcpipconfig)数据结构。

 

 





