---
title: ISCSI\_LoginOptions WMI 类
description: ISCSI\_LoginOptions WMI 类
ms.assetid: dc05f8e9-599d-4963-98a8-64e1d23c37a1
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: dc45a124ad183b7f52a81e52442ee877a8dac8f7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378429"
---
# <a name="iscsiloginoptions-wmi-class"></a>ISCSI\_LoginOptions WMI 类


## <span id="ddk_iscsi_loginoptions_wmi_class_kr"></span><span id="DDK_ISCSI_LOGINOPTIONS_WMI_CLASS_KR"></span>


ISCSI\_LoginOptions 类描述目标登录会话的特征。 此类定义中，如下所示*Common.mof*。

```cpp
class ISCSI_LoginOptions {
  [WmiDataId(1),
     description("Bit flags that specify which login 
     option values are specified") : amended,
     ISCSI_LOGIN_OPTIONS_INFO_QUALIFIERS,
     cpp_quote(ISCSI_LOGIN_OPTIONS_INFO_CPPQUOTE)]
     ISCSI_LOGIN_OPTIONS_INFO_SPECIFIED  
       InformationSpecified;
  [WmiDataId(2), 
     ValueMap{ ISCSI_DIGEST_TYPE_NONE,
               ISCSI_DIGEST_TYPE_CRC32C }, 
     Values{ "None", "CRC32C" },
     description("cyclic integrity checksums that can 
     be negotiated for the header digests") : amended]
     uint32  HeaderDigest;
  [WmiDataId(3),
     ValueMap{ ISCSI_DIGEST_TYPE_NONE,
               ISCSI_DIGEST_TYPE_CRC32C },
     Values{ "None", "CRC32C" },
     description("cyclic integrity checksums that can 
     be negotiated for the header digests") : amended]
     uint32  DataDigest;
  [WmiDataId(4),
    Description("Maximum number of connections, 0 implies 
    no limit") : amended]
    uint32  MaximumConnections;
  [WmiDataId(5),
    Description("The initiator and target negotiate 
    the minimum time, in seconds, to wait before 
    attempting an explicit/implicit logout or active 
    task reassignment after an unexpected connection
    termination or a connection reset.") : amended]
    uint32  DefaultTime2Wait;
  [WmiDataId(6),
    Description(" The initiator and target negotiate the
    maximum time, in seconds after an initial wait
    (Time2Wait), before which an explicit/implicit
    connection Logout or active task reassignment is still
    possible after an unexpected connection termination or
    a connection reset.") : amended]
    uint32  DefaultTime2Retain;
  [WmiDataId(7),
    Description("Flags that affect how login occurs") :
    amended, cpp_quote(ISCSI_LOGIN_FLAGS_CPPQUOTE),
                       ISCSI_LOGIN_FLAGS_QUALIFIERS]
    ISCSI_LOGIN_FLAGS  LoginFlags;
  [WmiDataId(8),
    Description("Authentication method specified for login")
    : amended, ISCSI_AUTH_TYPES_QUALIFIERS]
    ISCSI_AUTH_TYPES  AuthType;
};
```

当 WMI 工具套件编译前面的类定义时，它会生成[ **ISCSI\_LoginOptions** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iscsidef/ns-iscsidef-_iscsi_loginoptions)数据结构。

 

 





