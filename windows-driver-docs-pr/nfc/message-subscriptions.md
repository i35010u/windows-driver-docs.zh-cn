---
title: NFP 消息订阅
description: NFP 消息订阅
ms.assetid: ECE9C495-978F-4BD7-95BC-B68432F9B81E
keywords:
- NFC
- 附近通信
- 近程
- 邻近附近
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9ae0834d88925b73d13a7da1a910c9573c071e4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555897"
---
# <a name="nfp-message-subscriptions"></a>NFP 消息订阅


订阅表示为驱动程序中的唯一打开句柄。 订阅使处于活动状态的打开的句柄到"Sub\\"设备命名空间。 订阅的类型定义之后的内容为"Sub\\"前缀。

在接收到消息的回调提供通过已完成[ **IOCTL\_NFP\_获取\_下一步\_已订阅\_消息**](https://msdn.microsoft.com/library/windows/hardware/jj853319)。

可以通过暂时禁用订阅[ **IOCTL\_NFP\_禁用**](https://msdn.microsoft.com/library/windows/hardware/jj853315)。

订阅可以通过重新启动[ **IOCTL\_NFP\_启用**](https://msdn.microsoft.com/library/windows/hardware/jj853316)。

## <a name="handles"></a>句柄


想要订阅的消息类型的客户端将首先打开该驱动程序的新句柄。 不能重复使用以前的发布、 订阅和等等中的句柄。 如果不再需要它们，良好的客户端将关闭它们。

在打开句柄，客户端设置的消息订阅的类型。 这是相同的机制用于发布，的不同之处在于类型前缀为"Sub\\"而不是"Pubs\\"。

没有任何工具可以读回该类型。

### <a name="required-actions"></a>所需的操作

-   该驱动程序必须分析协议组件 (之前第一个。)。 无法识别的任何协议必须完成，状态\_对象\_路径\_不\_找到
-   如果缓冲区长度内以 NULL 结尾的字符串不是，该驱动程序必须完成状态 IOCTL\_无效\_参数。
-   如果协议要求子类型和字符串缓冲区的子类型组件是小于一 (1) 字符或超过 250 个字符，该驱动程序必须完成状态 IOCTL\_无效\_参数。
-   如果字符串缓冲区的协议组件的长度超过 250 个字符，该驱动程序必须完成状态 IOCTL\_无效\_参数。
-   该驱动程序必须将解释为字符串的末尾的第一个 NULL。
-   驱动程序可能会识别订阅的"配对： 蓝牙"类型。
-   驱动程序必须识别"WindowsUri"类型。
-   驱动程序必须识别仅限于订阅的"DeviceArrived"类型。
-   驱动程序必须识别仅限于订阅的"DeviceDeparted"类型。
-   驱动程序必须识别仅限于订阅的"WindowsMime"类型。
-   驱动程序必须识别"WindowsMime"。 类型。
-   如果协议应仅识别对于订阅，并指定 IOCTL"Pubs\\"，该驱动程序必须完成状态 IOCTL\_对象\_路径\_不\_找到。
-   如果协议应仅识别对于发布，并指定 IOCTL"子例程\\"，该驱动程序必须完成状态 IOCTL\_对象\_路径\_不\_找到。
-   仅某些协议 （命名空间）。 在本文档中显式指定，除非驱动程序都不能识别开头的任何协议：
    -   "Windows”
    -   "设备"
    -   "配对"
    -   "NDEF"
-   为同一类型的两个打开句柄必须代表两个不同的实体。
-   如果*CreateFile*成功，该句柄是现在的"订阅句柄"，和不能更改为任何其他类型的句柄。
-   此 IOCTL 成功后，和之前关闭此句柄，每次通过与此订阅的类型匹配的邻近技术收到一条消息时该消息的数据必须附加到传递到客户端的文件句柄。

## <a name="unsubscribe"></a>取消订阅


若要停止接收消息，客户端将关闭订阅句柄。 如果客户端进程将终止，系统将关闭所有打开的文件句柄代表客户端。

### <a name="required-actions"></a>所需的操作

当关闭句柄时，该驱动程序必须回收使用的订阅的所有内存：

-   该驱动程序必须回收的类型字符串数据。
-   接收的队列必须清除，并且可以回收。
-   IOCTL 必须完成，状态任何挂起\_已取消。

## <a name="malicious-peers"></a>恶意的对等方


如果恶意的对等设备尝试拒绝通过邻近技术服务 (DOS) 攻击，就可以在客户端可能不能以足够快的速度清空"Received"的队列，以防止过多的内存使用的驱动程序。

### <a name="required-actions"></a>所需的操作

该驱动程序不能进行排队或如果 50 条消息时当前 （最新消息将被删除） 的"Received"队列中收到该消息向客户端传递给定的消息。

## <a name="unresponsive-or-misbehaving-clients"></a>无响应或行为不正确的客户端


如果客户端将停止未能发送所需通过清空"Received"队列[ **IOCTL\_NFP\_获取\_下一步\_已订阅\_消息**](https://msdn.microsoft.com/library/windows/hardware/jj853319)十台到二十秒钟的请求\[10-20 秒\]，则驱动程序应假定客户端将消失。 正常情况下，客户端应刷新其请求一秒内还\[1s\]。 如果发生这种情况，驱动程序必须将"CompleteEventImmediately"计数器设置为零，必须递增计数器，直到客户端唤醒，并将所需的 IRP 发送。

### <a name="required-actions"></a>所需的操作

该驱动程序必须设置"CompleteEventImmediately"计数器为零，必须递增计数器，如果客户端未发送更换[ **IOCTL\_NFP\_获取\_下一步\_订阅\_消息**](https://msdn.microsoft.com/library/windows/hardware/jj853319)以前 IOCTL 完成后 10 到 20 秒内。

## <a name="malformed-messages"></a>格式不正确的消息


客户端很可能删除或忽略所有错误 (除状态\_缓冲区\_OVERFLOW) 从返回[ **IOCTL\_NFP\_获取\_下一步\_订阅\_消息**](https://msdn.microsoft.com/library/windows/hardware/jj853319)。 因此，驱动程序不应完成，这些错误条件只是因为收到格式不正确的消息。

### <a name="required-actions"></a>所需的操作

-   驱动程序都不能将大于到客户端的最大允许的消息大小的消息传递。
-   向客户端驱动程序不应提供长度为零的消息。
-   驱动程序都不能将部分消息传递到订阅服务器。
-   驱动程序都不能将消息传递到客户端未通过强的 CRC。

    **请注意**  NFC 论坛认证保证这 nfc 的 NFP 提供程序。

     

-   该驱动程序必须使用强可靠传输和/或尝试重新传输失败强 CRC 的消息。

    **请注意**  NFC 论坛认证保证这 nfc 的 NFP 提供程序。

     

## <a name="duplicate-subscriptions"></a>重复订阅


该驱动程序应假定，如果两次，客户端订阅的消息类型，这是因为客户端想要接收消息时两次收到消息。

### <a name="required-actions"></a>所需的操作

该驱动程序必须接受并报告重复订阅，即使由同一客户端订阅。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
[邻近 DDI 引用附近](https://msdn.microsoft.com/library/windows/hardware/jj866056)  

