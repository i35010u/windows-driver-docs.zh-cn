---
description: 访问控制
title: 访问控制
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54c3999a5e9d2b51ec1f73683499cac5e3f68907
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88968706"
---
# <a name="access-control"></a>访问控制


Windows 驱动模型 (WDM) 支持通过访问控制列表 (Acl) 上即插即用 (PnP) 设备节点上的访问控制列表限制设备访问。 这意味着供应商和网络管理员可以限制对任何设备类型的访问。 当应用程序通过调用 **IPortableDevice：： Open** 方法打开驱动程序的句柄时，驱动程序的 I/o 管理器将验证给定用户是否具有所需的访问权限，并且在将 IOCTLs 发送到该句柄的驱动程序时，与访问检查类似。

例如，网络管理员可能会将来宾用户限制为对便携设备进行只读访问，同时可以向经过身份验证的用户授予读/写访问权限。 在这种情况下，如果来宾发出 WPD 命令，该命令需要读取/写入访问权限 (如删除对象) ;如果访问被拒绝，它会失败，而如果经过身份验证的用户发出了相同的命令，则会成功。

用于控制对可移动存储和便携式设备的访问的组策略项实际上并不是一种简单的方式，管理员可以一次将 PnP 设备节点 Acl 应用于整个设备类 (例如，应用 "拒绝对便携设备的写入访问权限" 组策略会调整所有 WPD 设备的 Acl 以拒绝写入访问) 。

## <a name="span-idi_o_control_codes_in_wpdspanspan-idi_o_control_codes_in_wpdspanspan-idi_o_control_codes_in_wpdspanio-control-codes-in-wpd"></a><span id="I_O_Control_Codes_in_WPD"></span><span id="i_o_control_codes_in_wpd"></span><span id="I_O_CONTROL_CODES_IN_WPD"></span>WPD 中的 i/o 控制代码


WPD 应用程序通过打开设备句柄并发送 i/o 控制代码 (IOCTLs) 来与驱动程序通信。 这些 IOCTLs 由四个部分组成：

1.  设备类型
2.  函数代码
3.  Buffer 方法
4.  访问类型

访问类型是第四部分指定给定命令的特定访问要求。 驱动程序的 i/o 管理器使用此数据来执行访问控制列表 (ACL) 检查。

如果 IOCTL 定义为：

```ManagedCPlusPlus
    #define MY_READ_IOCTL CTL_CODE(FILE_DEVICE_X, CONTROL_FUNCTION_Y, METHOD_BUFFERED, FILE_READ_ACCESS)
```

驱动程序的 i/o 管理器将检查发送此消息时设备句柄的所有者是否具有对设备的读取访问权限。

如果 IOCTL 定义为：

```ManagedCPlusPlus
    #define MY_READWRITE_IOCTL CTL_CODE(FILE_DEVICE_X, CONTROL_FUNCTION_Z, METHOD_BUFFERED, (FILE_READ_ACCESS | FILE_WRITE_ACCESS))
```

驱动程序的 i/o 管理器将在发送此消息时检查设备句柄的所有者是否对设备具有读写访问权限。

## <a name="span-idpayload_verificationspanspan-idpayload_verificationspanspan-idpayload_verificationspanpayload-verification"></a><span id="Payload_Verification"></span><span id="payload_verification"></span><span id="PAYLOAD_VERIFICATION"></span>负载验证


WPD 与其他许多驱动程序堆栈略有不同，因为它是包含 WPD 命令的 WPD 消息的负载，而不是大多数驱动程序堆栈中的 IOCTL (，IOCTL 是命令) 。 这并不是唯一的，但这意味着 WPD 具有 2 IOCTLs：

-   \_ \_ \_ \_ 为需要只读访问权限的所有 WPD 命令 (ioctl WPD 消息读取访问) 权限的只读 ioctl
-   \_ \_ \_ \_ 对于需要读写访问权限的所有 WPD 命令，可读写 ioctl (ioctl WPD MESSAGE READWRITE 访问) 

在 WPD 中，应用程序可以通过传递 WPD API 并直接打开驱动程序的句柄。 这与 IOCTL 有效负载包含实际命令的事实相结合，这意味着恶意应用程序可能会尝试通过发送 WPD 命令（该命令需要具有只读 IOCTL 的读写访问权限）来欺骗驱动程序 (例如，使用的 IOCTL 应为 IOCTL \_ WPD \_ 消息 \_ 读取 \_ 访问，但负载可能包含 WPD \_ command \_ 对象 \_ 管理 \_ 删除 \_ 对象) 。

因此，WPD 驱动程序必须验证是否已使用正确的 IOCTL 发送 WPD 命令有效负载，以确保 i/o 管理器执行了相应的 ACL 检查 (例如，在前面的示例中，i/o 管理器会检查调用方是否具有只读访问权限，因为 IOCTL 是 IOCTL \_ WPD \_ 消息 \_ 读取 \_ 访问权限。 即使调用方具有只读访问权限，驱动程序也应拒绝此类调用，因为 IOCTL \_ WPD \_ MESSAGE \_ READWRITE \_ 访问应已与命令一起使用，如 WPD \_ 命令 \_ 对象 \_ 管理 \_ 删除 \_ 对象) 。

由于每个驱动程序都必须执行有效负载验证，因此 WPD 提供了易于使用的宏，以使该驱动程序自动进行此检查。 有关详细信息和示例代码，请参阅 WPD 驱动程序编程指南的 [处理访问控制](handling-access-control.md) 部分。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[**WPD 驱动程序概述**](wpd-drivers-overview.md)

 

 





