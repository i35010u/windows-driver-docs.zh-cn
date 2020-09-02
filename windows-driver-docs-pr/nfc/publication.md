---
title: 发布 NFP 消息
description: 发布 NFP 消息
ms.assetid: 45BE3620-ADF4-413D-90B3-586FCEB5F606
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 175a09f8f9de4cdc67bc575f59f9dee614bd06dd
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89381683"
---
# <a name="publishing-nfp-messages"></a>发布 NFP 消息


发布表示为驱动程序中的唯一打开句柄。 活动发布必须同时具有类型和数据缓冲区。 该类型是通过在 "Pubs" 命名空间中打开文件名设置的。 数据缓冲区通过发送 [**IOCTL \_ NFP \_ 集 \_ 负载**](/windows-hardware/drivers/ddi/nfpdev/ni-nfpdev-ioctl_nfp_set_payload)进行设置。

尝试传输时，将通过已完成的 [**IOCTL \_ NFP \_ 获取 \_ 下一次传输的 \_ \_ 消息**](/windows-hardware/drivers/ddi/nfpdev/ni-nfpdev-ioctl_nfp_get_next_transmitted_message)。

可以通过 [**IOCTL \_ NFP \_ DISABLE**](/windows-hardware/drivers/ddi/nfpdev/ni-nfpdev-ioctl_nfp_disable)暂时禁用发布。

可以通过 [**IOCTL \_ NFP \_ ENABLE**](/windows-hardware/drivers/ddi/nfpdev/ni-nfpdev-ioctl_nfp_enable)重新启用发布。

##  <a name="handles"></a>句柄数


要发布消息的客户端将首先打开驱动程序的新句柄。 不能重复使用以前的发布、订阅等的句柄。 如果不再需要它们，它们将被良好的客户端关闭。

客户端将打开 "Pubs/协议" 中的文件句柄 &lt; &gt; 。 &lt;子类型 &gt; "设备相对命名空间。 下面是一个完整示例。

``` syntax
\\?\root#ContosoProx#0000#{FB3842CD-9E2A-4F83-8FCC-4B0761139AE9}\Pubs\Windows.windows.com/SD
<---------------Device Interface Symbolic Link-----------------> <------File Name---------->
    <--------------------><------------------------------------> <--> <-----> <------------>
          DeviceID          NearFieldProximity Interface Class     *  Protocol   SubType
```

打开句柄之后，客户端应设置要与 [**IOCTL \_ NFP \_ 集 \_ 负载**](/windows-hardware/drivers/ddi/nfpdev/ni-nfpdev-ioctl_nfp_set_payload)一起发布的消息的负载。

没有任何工具可以读回指定的文件名 () 的发布类型。

### <a name="file-name"></a>文件名

在驱动程序的 *CreateFile* 处理程序中，将去除设备接口 *SymbolicLink* ，而只保留设备相对文件名。 此文件名将为以 null 结尾的区分大小写的 UTF-16LE 字符串缓冲区，该缓冲区指示发布 (或订阅) 的类型。 此缓冲区的最大大小为502个字符，包括 NULL 结束符。 驱动程序必须将此路径解析为三个构成组件： "Pubs \\ "、"协议" 和 "子类型"。

### <a name="required-actions"></a>必需的措施

-   驱动程序必须在第一个 "." 之前解析协议组件 () 。 任何无法识别的协议必须完成，但 \_ \_ \_ \_ 找不到状态对象路径
-   如果字符串在缓冲区长度内不以 NULL 值结束，则驱动程序必须完成具有 \_ 无效参数的 IOCTL \_ 。
-   如果协议需要子类型，并且字符串缓冲区的子类型组件小于一 (1) 字符或超过250个字符，则驱动程序必须完成状态为 "无效" 的 \_ IOCTL \_ 。
-   如果字符串缓冲区的协议组件的长度超过250个字符，则驱动程序必须完成具有 \_ 无效参数的 IOCTL \_ 。
-   驱动程序必须将第一个 NULL 解释为字符串的末尾。
-   驱动程序可以识别发布的 "配对：蓝牙" 类型。 驱动程序可能会识别此类型，以便保持兼容性。  (记下冒号，而不是使用句点。 ) 
-   驱动程序必须识别 "WindowsUri" 类型。
-   驱动程序必须识别订阅的 "DeviceArrived" 类型。
-   驱动程序必须识别订阅的 "DeviceDeparted" 类型。
-   驱动程序必须识别订阅的 "WindowsMime" 类型。
-   驱动程序必须识别 "WindowsMime"。 的参数。
-   如果只应为订阅识别协议，并且 IOCTL 指定了 "Pubs \\ "，则驱动程序必须完成 \_ 未找到状态对象路径的 \_ IOCTL \_ \_ 。
-   如果只应为发布识别此协议，并且 IOCTL 指定了 "Sub \\ "，则驱动程序必须完成 \_ \_ \_ 找不到状态对象路径的 IOCTL \_ 。
-   同一类型的两个打开的句柄必须表示两个不同的实体。
-   保留了一些 (命名空间) 的协议。 除非在本文档中显式指定，否则驱动程序不能识别以以下开头的任何协议：
    -   Windows
    -   装置
    -   组合
    -   "NDEF"
    -   NFC
    -   "Iso14443Dep"
    -   "Iso14443TypeA"
    -   "Iso14443TypeB"
    -   "Iso15693Vicinity"
    -   "MifareClassic"
    -   "MifareUltralight"
    -   "FeliCa"

## <a name="unpublish"></a>取消发布


当客户端不再需要发布消息时，它将关闭发布句柄。 这表示不应再传输消息。 如果客户端进程终止，系统会代表客户端关闭所有打开的文件句柄。

### <a name="required-actions"></a>必需的措施

-   关闭句柄 (IRP \_ MJ \_ 关闭) ，驱动程序：
    -   必须回收发布使用的所有内存 (类型和消息数据) 除用于当前发布传输的缓冲区外。
    -   如果设备将来变为近程，则不能传输消息。
    -   不得中断发布的任何正在进行的传输。
-   驱动程序可能会忽略 IRP \_ MJ \_ 清除。

驱动程序应该假定，如果客户端发布一条消息两次，则是因为客户端希望在设备接近时传输两次消息。

### <a name="required-actions"></a>必需的措施

驱动程序必须接受并传输重复发布的消息，即使是由同一客户端发布的。

### <a name="required-actions"></a>必需的措施


如果客户端尚未发送替换 IOCTL 10-20 NFP，则驱动程序必须删除所有消息 (并从 "接收" 队列中收回这些资源) 。 [** \_ \_ \_ \_ \_ **](/windows-hardware/drivers/ddi/nfpdev/ni-nfpdev-ioctl_nfp_get_next_subscribed_message)

## <a name="unresponsive-or-misbehaving-clients"></a>客户端无响应或异常


如果客户端无法发送所需的 [**IOCTL \_ NFP \_ 获取 \_ 下一次 \_ 传输 \_ 消息**](/windows-hardware/drivers/ddi/nfpdev/ni-nfpdev-ioctl_nfp_get_next_transmitted_message) 请求的时间为10到20秒 \[ 10-20sec \] ，则驱动程序应假定客户端已消失。 正常情况下，客户端应在1秒内刷新请求 \[ \] 。 如果出现这种情况，驱动程序必须将 "CompleteEventImmediately" 计数器设置为零，且在客户端唤醒并发送所需的 IRP 之前，不能递增计数器。

### <a name="required-actions"></a>必需的措施

如果客户端尚未发送替换 IOCTL 10-20 NFP，则驱动程序必须将 "CompleteEventImmediately" 计数器设置为零，且不能递增计数器。 [** \_ \_ \_ \_ \_ **](/windows-hardware/drivers/ddi/nfpdev/ni-nfpdev-ioctl_nfp_get_next_transmitted_message)

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](/windows-hardware/drivers/ddi/index)  
[近字段邻近 DDI 引用](/windows-hardware/drivers/ddi/index)