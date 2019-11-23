---
title: NFP 消息订阅
description: NFP 消息订阅
ms.assetid: ECE9C495-978F-4BD7-95BC-B68432F9B81E
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51ff1d58af1cfa651808dc451b36fcc59de4bacd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832120"
---
# <a name="nfp-message-subscriptions"></a>NFP 消息订阅


订阅在驱动程序中表示为唯一打开的句柄。 通过打开 "Sub\\" 设备命名空间中的句柄使订阅处于活动状态。 订阅的类型定义为 "Sub\\" 前缀后面的所有内容。

消息接收的回调是通过已完成的[**IOCTL\_NFP 提供的，\_获取\_下一\_订阅\_消息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfpdev/ni-nfpdev-ioctl_nfp_get_next_subscribed_message)。

可以通过[**IOCTL\_NFP\_DISABLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfpdev/ni-nfpdev-ioctl_nfp_disable)来暂时禁用订阅。

可以通过[**IOCTL\_NFP\_启用**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfpdev/ni-nfpdev-ioctl_nfp_enable)来重新启用订阅。

## <a name="handles"></a>手柄


要订阅消息类型的客户端将首先打开驱动程序的新句柄。 不能重复使用以前的发布、订阅等的句柄。 如果不再需要它们，它们将被良好的客户端关闭。

在打开句柄时，客户端设置消息订阅的类型。 这是与发布一起使用的相同机制，只不过该类型以 "Sub\\" 而不是 "Pubs\\" 作为前缀。

没有任何工具可以读回类型。

### <a name="required-actions"></a>必需的措施

-   驱动程序必须分析协议组件（在第一个 "." 之前）。 任何无法识别的协议必须完成，状态\_对象\_路径\_找不到\_
-   如果字符串在缓冲区长度内不以 NULL 值结束，则驱动程序必须完成具有状态\_无效\_参数的 IOCTL。
-   如果协议需要子类型，并且字符串缓冲区的子类型组件小于一（1）个字符或超过250个字符，则驱动程序必须完成具有状态\_无效\_参数的 IOCTL。
-   如果字符串缓冲区的协议组件的长度超过250个字符，则驱动程序必须完成具有状态\_无效\_参数的 IOCTL。
-   驱动程序必须将第一个 NULL 解释为字符串的末尾。
-   驱动程序可以识别订阅的 "配对：蓝牙" 类型。
-   驱动程序必须识别 "WindowsUri" 类型。
-   驱动程序必须识别订阅的 "DeviceArrived" 类型。
-   驱动程序必须识别订阅的 "DeviceDeparted" 类型。
-   驱动程序必须识别订阅的 "WindowsMime" 类型。
-   驱动程序必须识别 "WindowsMime"。 类别.
-   如果只应为订阅识别协议，并且 IOCTL 指定了 "Pubs\\"，则驱动程序必须完成状态为\_对象\_路径的 IOCTL，\_\_找不到。
-   如果只应为发布识别此协议，并且 IOCTL 指定了 "Sub\\"，则驱动程序必须完成状态为\_对象\_路径的 IOCTL，\_\_找不到该路径。
-   某些协议（命名空间）是保留的。 除非在本文档中显式指定，否则驱动程序不能识别以以下开头的任何协议：
    -   Windows
    -   装置
    -   组合
    -   "NDEF"
-   同一类型的两个打开的句柄必须表示两个不同的实体。
-   如果*CreateFile*成功，句柄现在为 "订阅句柄"，不能将其更改为任何其他类型的句柄。
-   此 IOCTL 成功后和句柄关闭之前，每次通过与此订阅的类型匹配的邻近技术收到消息时，该消息的数据必须附加到文件句柄，以便传递到客户端。

## <a name="unsubscribe"></a>订阅


客户端将关闭订阅句柄以停止接收消息。 如果客户端进程终止，系统会代表客户端关闭所有打开的文件句柄。

### <a name="required-actions"></a>必需的措施

当关闭句柄时，驱动程序必须回收订阅使用的所有内存：

-   驱动程序必须回收类型字符串数据。
-   必须清除并回收收到的队列。
-   必须完成任何挂起的 IOCTL，状态\_"已取消"。

## <a name="malicious-peers"></a>恶意对等


如果恶意对等设备尝试通过邻近技术的拒绝服务（DOS）攻击，则客户端可能无法以足够快的速度释放 "接收的" 队列，以防止驱动程序使用过多的内存。

### <a name="required-actions"></a>必需的措施

如果在50消息当前在 "接收" 队列中时收到消息，则驱动程序不得将给定的消息排队或传递给客户端（最新的消息被丢弃）。

## <a name="unresponsive-or-misbehaving-clients"></a>客户端无响应或异常


如果客户端由于无法将所需的 IOCTL 发送\_NFP 来停止排出 "接收的" 队列， [ **\_获取\_下一\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfpdev/ni-nfpdev-ioctl_nfp_get_next_subscribed_message)在10到20秒的时间段内\_的消息请求 \[，则驱动程序应假定客户端已断开。\] 在正常情况下，客户端应在1秒 \[1\]中正常刷新请求。 如果出现这种情况，驱动程序必须将 "CompleteEventImmediately" 计数器设置为零，且在客户端唤醒并发送所需的 IRP 之前，不能递增计数器。

### <a name="required-actions"></a>必需的措施

如果客户端尚未发送替换 IOCTL\_NFP，则驱动程序必须将 "CompleteEventImmediately" 计数器设置为零，且不能递增计数器[ **\_获取\_下一个\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfpdev/ni-nfpdev-ioctl_nfp_get_next_subscribed_message)在之前的 IOCTL 完成 10-20 秒内已订阅\_消息。

## <a name="malformed-messages"></a>消息格式不正确


客户端可能会删除或忽略从 IOCTL\_NFP 返回的所有错误（除了状态\_缓冲区\_溢出）， [ **\_获取\_下一\_订阅\_消息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfpdev/ni-nfpdev-ioctl_nfp_get_next_subscribed_message)。 因此，由于收到格式不正确的消息，驱动程序不应只使用错误条件来完成这些操作。

### <a name="required-actions"></a>必需的措施

-   驱动程序不得将超过允许的最大消息大小的消息传递给客户端。
-   驱动程序不应将长度为零的消息传递给客户端。
-   驱动程序不得将部分消息传递给订阅服务器。
-   驱动程序不能将消息传送到未通过强 CRC 的客户端。

    **注意**  Nfc 论坛认证可保证此功能适用于启用了 NFC 的 NFP 提供商。

     

-   驱动程序必须使用高度可靠的传输和/或尝试重新传输无法执行强 CRC 的消息。

    **注意**  Nfc 论坛认证可保证此功能适用于启用了 NFC 的 NFP 提供商。

     

## <a name="duplicate-subscriptions"></a>重复订阅


驱动程序应该假定，如果客户端订阅消息类型两次，则是因为客户端想要在收到消息后收到消息两次。

### <a name="required-actions"></a>必需的措施

驱动程序必须接受和报告重复的订阅，即使是由同一客户端订阅。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口（DDI）概述](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[近字段邻近 DDI 引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  

