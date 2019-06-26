---
title: MSiSCSI\_ManagementOperations WMI 类
description: MSiSCSI\_ManagementOperations WMI 类
ms.assetid: 1037be46-6cae-458d-8549-927c7a053195
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 20291f4cdd88cddc0caa62fd1c1b3746caafa1ab
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379090"
---
# <a name="msiscsimanagementoperations-wmi-class"></a>MSiSCSI\_ManagementOperations WMI 类


MSiSCSI\_MangementOperations WMI 类包含 ping 方法来执行 ICMP ping 请求到的目标地址。 此类 Mgmt.mof 中定义，如下所示。

```cpp
class MSiSCSI_ManagementOperations
{
    //
    // This class must be registered using PDO instance names
    //
    [key]
    string InstanceName;
 
    boolean Active;

    [WmiMethodId(10),
     Implemented,
     Description("Perform an ICMP ping") : amended,
     cpp_quote(
"//\n"
"// This method is recommended.\n"
"//\n"             
"// Ping will perform ICMP ping requests to the destination address \n"
"// and return the number of ping responses received. This is only supported\n"
"// by some HBA, use the ping command for the software initiator.\n"
"//\n"
              )            
    ]
    void PingIPAddress(
                     [in,
                      Description("Number of requests to send") : amended
                     ] uint32 RequestCount,

                     [in,
                      Description("Number of bytes in each request") : amended
                     ] uint32 RequestSize,

                     [in,
                      Description("Number of ms to wait for response") : amended
                     ] uint32 Timeout,

                     [in,
                      description("IP address to ping") : amended
                     ] ISCSI_IP_Address Address,
 
                     [out,
                      ISCSI_STATUS_QUALIFIERS
                     ] ISCSI_STATUS Status,
 
                     [out,
                      Description("Number of responses received") : amended
                     ] uint32 ResponsesReceived

                    );

 
};
```

当 WMI 工具套件编译前面的类定义时，它会生成之一[MSiSCSI\_ManagementOperations](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)数据结构。

 

 





