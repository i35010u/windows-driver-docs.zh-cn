---
Description: Access Control
title: 访问控制
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5e203546649289d3b265c27be34b69994c87a19
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522259"
---
# <a name="access-control"></a>访问控制


Windows 驱动程序模型 (WDM) 支持 Plug and Play (PnP) 设备节点上通过访问控制列表 (Acl) 的设备访问的限制。 这意味着供应商和网络管理员可以为任何设备类型限制访问。 当应用程序打开的句柄驱动程序通过调用**IPortableDevice::Open**方法，驱动程序的 I/O 管理器验证给定的用户是否具有所需的权限，并且同样 does 来访问检查时 Ioctl 发送到从该句柄的驱动程序。

例如，网络管理员无法来宾用户限制到便携式设备的只读访问权限时它们可以授予身份验证的用户读/写访问。 在这种情况下，如果颁发的访客 WPD 命令该需要的读/写访问权限 （例如删除对象）;它会因访问被拒绝，而如果已经过身份验证用户发出同一命令，它会成功。

用于控制对可移动存储和可移植的设备访问的组策略条目实际上只不过是，管理员可以 （例如，应用"拒绝写入访问一次应用到整个类别的设备的即插即用设备节点 Acl 的简单方法便携设备"组策略将调整所有 WPD 设备的 Acl 以拒绝写入权限)。

## <a name="span-idiocontrolcodesinwpdspanspan-idiocontrolcodesinwpdspanspan-idiocontrolcodesinwpdspanio-control-codes-in-wpd"></a><span id="I_O_Control_Codes_in_WPD"></span><span id="i_o_control_codes_in_wpd"></span><span id="I_O_CONTROL_CODES_IN_WPD"></span>WPD 中的 I/O 控制代码


WPD 应用程序通过打开设备句柄并发送 I/O 控制代码 (Ioctl) 与驱动程序进行通信。 这些 Ioctl 由四个部分组成：

1.  设备类型
2.  函数代码
3.  缓冲区方法
4.  权限类型

第四个部分中，访问类型，指定给定的命令的特定访问要求。 驱动程序的 I/O 管理器使用此数据执行的访问控制列表 (ACL) 检查。

因此，如果 IOCTL 已定义为：

```ManagedCPlusPlus
    #define MY_READ_IOCTL CTL_CODE(FILE_DEVICE_X, CONTROL_FUNCTION_Y, METHOD_BUFFERED, FILE_READ_ACCESS)
```

驱动程序的 I/O 管理器会检查设备句柄的所有者具有读取访问权限的设备，当发送此消息。

而且，如果 IOCTL 已定义为：

```ManagedCPlusPlus
    #define MY_READWRITE_IOCTL CTL_CODE(FILE_DEVICE_X, CONTROL_FUNCTION_Z, METHOD_BUFFERED, (FILE_READ_ACCESS | FILE_WRITE_ACCESS))
```

驱动程序的 I/O 管理器将检查设备句柄的所有者具有读取和写入设备的访问权限时发送此消息。

## <a name="span-idpayloadverificationspanspan-idpayloadverificationspanspan-idpayloadverificationspanpayload-verification"></a><span id="Payload_Verification"></span><span id="payload_verification"></span><span id="PAYLOAD_VERIFICATION"></span>有效负载验证


WPD 是与许多其他驱动程序堆栈略有不同，因为它是包含 WPD 命令，不 IOCTL WPD 消息的负载 （在大多数驱动程序堆栈，IOCTL 是该命令）。 这不是唯一的但它意味着 WPD Ioctl 2:

-   只读 IOCTL (IOCTL\_WPD\_消息\_读取\_访问) 要求只读访问权限的所有 WPD 命令
-   读写 IOCTL (IOCTL\_WPD\_消息\_READWRITE\_访问) 的所有要求读写访问权限的 WPD 命令

在 WPD，就可以绕过 WPD API，并直接打开的句柄驱动程序的应用程序。 此操作，请结合这一事实 IOCTL 负载包含实际的命令中，意味着它是可能的恶意应用程序可能会尝试通过发送需要读写访问，只读 IOCTL (例如，IOCTL WPD 命令欺骗驱动程序使用将 IOCTL\_WPD\_消息\_读取\_访问权限，但负载可能包含 WPD\_命令\_对象\_管理\_删除\_对象)。

因此，WPD 驱动程序必须验证 WPD 命令有效负载发送与正确 IOCTL 以确保 I/O 管理器执行适当的 ACL 检查 （例如，在上一示例中，I/O 管理器将具有检查调用方必须只读的访问，因为 IOCTL 是 IOCTL\_WPD\_消息\_读取\_访问。 即使调用方具有只读访问权限，该驱动程序应拒绝此类调用，因为 IOCTL\_WPD\_消息\_READWRITE\_访问应使用下面的命令 WPD 使用\_命令\_对象\_管理\_删除\_对象)。

由于每个驱动程序必须执行负载验证，WPD 提供简单易用的宏，以进行此检查自动驱动程序。 请参阅[处理的访问控制](handling-access-control.md)WPD 驱动程序编程指南的详细信息和示例代码的部分。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[**WPD 驱动程序概述**](wpd-drivers-overview.md)

 

 





