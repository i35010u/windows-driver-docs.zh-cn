---
title: ISCSI \_ IP \_ 地址 WMI 类
description: ISCSI \_ IP \_ 地址 WMI 类
ms.assetid: 3ceeb54f-ecc5-40c5-b0a8-8c6f86203f1c
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e3410358a5a4d0742683a38c23752a3ffdebb3af
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188813"
---
# <a name="iscsi_ip_address-wmi-class"></a>ISCSI \_ IP \_ 地址 WMI 类


## <span id="ddk_iscsi_ip_address_wmi_class_kr"></span><span id="DDK_ISCSI_IP_ADDRESS_WMI_CLASS_KR"></span>


ISCSI \_ ip \_ 地址类提供与所使用的 ip 协议版本无关的 ip 地址的定义。 此类是在 *常见的 mof*中定义的。

```cpp
class ISCSI_IP_Address {
  [WmiDataId(1), read, write, DisplayName("Address Format")
    : amended, description("Type of address specified. 
    It can be text: a DNS or dotted address or it can be
    a binary ipv4 or ipv6 address") : amended,
    Values{ "Text Address", "IpV4 Address",
            "IpV6 Address", "Empty Address"},
    ValueMap{"0", "1", "2", "3"}]
#define ISCSIIPADDRESSTYPE  uint32
  ISCSIIPADDRESSTYPE  Type;
  [WmiDataId(2), read, write, DisplayInHex,
    DisplayName("IPV4 Address"): amended,
    description("If IPV4 Address is specified as the 
    Address Format then this contains the binary IPv4 
    ip address") : amended]
    uint32  IpV4Address;
  [WmiDataId(3), DisplayName("IPV6 Address"): amended,
    read, write, description("If IPV6 Address is 
    specified as the Address Format then this contains 
    the binary IPv6 ip address") : amended]
    uint8  IpV6Address[16];
  [WmiDataId(4), read, write,
    DisplayName("IPV6 Flow Information") : amended,
    description("IPV6 flow information") : amended]
    uint32  IpV6FlowInfo;
  [WmiDataId(5), read, write,
    DisplayName("IPV6 Scope Id") : amended,
    description("IPV6 scope id") : amended]
    uint32  IpV6ScopeId;
  [WmiDataId(6), read, write,
    DisplayName("Text Address") : amended,
    description("Text address, either a DNS address or
    dotted address") : amended, 
    MaxLen(MAX_ISCSI_TEXT_ADDRESS_LEN)]
    string  TextAddress;
};
```

当 WMI 工具套件编译上述类定义时，它将生成 [**ISCSI \_ IP \_ 地址**](/windows-hardware/drivers/ddi/iscsidef/ns-iscsidef-_iscsi_ip_address) 数据结构。

 

