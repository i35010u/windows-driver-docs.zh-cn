---
title: 发布 NFP 消息
description: 发布 NFP 消息
ms.assetid: 45BE3620-ADF4-413D-90B3-586FCEB5F606
keywords:
- NFC
- 附近通信
- 近程
- 邻近附近
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ad5b29f3064cb5cc84f6e9844c514fc2bb1d9f3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546402"
---
# <a name="publishing-nfp-messages"></a>发布 NFP 消息


发布表示为驱动程序中的唯一打开句柄。 一个类型和数据缓冲区，必须具有活动发布。 通过在"Pubs"命名空间中打开的文件名称集的类型。 通过发送设置的数据缓冲区[ **IOCTL\_NFP\_设置\_负载**](https://msdn.microsoft.com/library/windows/hardware/jj853321)。

在尝试传输回调提供通过已完成[ **IOCTL\_NFP\_获取\_下一步\_传输\_消息**](https://msdn.microsoft.com/library/windows/hardware/jj853320).

可以通过暂时禁用发布[ **IOCTL\_NFP\_禁用**](https://msdn.microsoft.com/library/windows/hardware/jj853315)。

发布可以通过重新启动[ **IOCTL\_NFP\_启用**](https://msdn.microsoft.com/library/windows/hardware/jj853316)。

##  <a name="handles"></a>句柄


想要将消息发布的客户端将首次打开该驱动程序的新句柄。 不能重复使用以前的发布、 订阅和等等中的句柄。 如果不再需要它们，良好的客户端将关闭它们。

客户端将打开的文件句柄"Pubs /&lt;协议&gt;。&lt;子类型&gt;"相对于设备的命名空间。 下面是一个完整的示例。

``` syntax
\\?\root#ContosoProx#0000#{FB3842CD-9E2A-4F83-8FCC-4B0761139AE9}\Pubs\Windows.windows.com/SD
<---------------Device Interface Symbolic Link-----------------> <------File Name---------->
    <--------------------><------------------------------------> <--> <-----> <------------>
          DeviceID          NearFieldProximity Interface Class     *  Protocol   SubType
```

打开句柄之后, 客户端应然后设置要在中发布的消息有效负载[ **IOCTL\_NFP\_设置\_负载**](https://msdn.microsoft.com/library/windows/hardware/jj853321)。

没有任何工具可以读回指定的文件名 （发布类型）。

### <a name="file-name"></a>文件名

中的驱动程序*CreateFile*处理程序中，设备接口*SymbolicLink*将得到解决，并且只能相对于设备的文件名称将保留。 此文件的名称将以 null 结尾区分大小写 UTF 16LE 字符串缓冲区中指示类型的发布 （或订阅）。 此缓冲区的最大大小为 502 包括 NULL 终止符的字符。 该驱动程序必须解析为三个构成组件的此路径："Pubs\\"、 协议、 和子类型。

### <a name="required-actions"></a>所需的操作

-   该驱动程序必须分析协议组件 (之前第一个。)。 无法识别的任何协议必须完成，状态\_对象\_路径\_不\_找到
-   如果缓冲区长度内以 NULL 结尾的字符串不是，该驱动程序必须完成状态 IOCTL\_无效\_参数。
-   如果协议要求子类型和字符串缓冲区的子类型组件是小于一 (1) 字符或超过 250 个字符，该驱动程序必须完成状态 IOCTL\_无效\_参数。
-   如果字符串缓冲区的协议组件的长度超过 250 个字符，该驱动程序必须完成状态 IOCTL\_无效\_参数。
-   该驱动程序必须将解释为字符串的末尾的第一个 NULL。
-   驱动程序可能会识别发布的"配对： 蓝牙"类型。 驱动程序可能会识别这种类型，以保持兼容性。 （请注意使用冒号，而不是使用句点）。
-   驱动程序必须识别"WindowsUri"类型。
-   驱动程序必须识别仅限于订阅的"DeviceArrived"类型。
-   驱动程序必须识别仅限于订阅的"DeviceDeparted"类型。
-   驱动程序必须识别仅限于订阅的"WindowsMime"类型。
-   驱动程序必须识别"WindowsMime"。 类型。
-   如果协议应仅识别对于订阅，并指定 IOCTL"Pubs\\"，该驱动程序必须完成状态 IOCTL\_对象\_路径\_不\_找到。
-   如果协议应仅识别对于发布，并指定 IOCTL"子例程\\"，该驱动程序必须完成状态 IOCTL\_对象\_路径\_不\_找到。
-   为同一类型的两个打开句柄必须代表两个不同的实体。
-   仅某些协议 （命名空间）。 在本文档中显式指定，除非驱动程序都不能识别开头的任何协议：
    -   "Windows”
    -   "设备"
    -   "配对"
    -   "NDEF"
    -   "NFC"
    -   "Iso14443Dep"
    -   "Iso14443TypeA”
    -   "Iso14443TypeB”
    -   "Iso15693Vicinity"
    -   "MifareClassic"
    -   "MifareUltralight"
    -   "FeliCa"

## <a name="unpublish"></a>取消发布


当客户端不再想发布一条消息时，它会关闭发布句柄。 这表示应不再传输消息。 如果客户端进程将终止，系统将关闭所有打开的文件句柄代表客户端。

### <a name="required-actions"></a>所需的操作

-   当关闭句柄 (IRP\_MJ\_关闭)，该驱动程序：
    -   必须回收所有内存缓冲区除外的发布 （类型和消息数据） 用于该发布的正在进行传输。
    -   如果在将来成为近程设备，必须不传输该消息。
    -   必须不会中断任何正在进行中传输的发布。
-   该驱动程序可能会忽略 IRP\_MJ\_清理。

该驱动程序应假定，如果客户端将消息发布两次，这是因为客户端希望消息两次传输设备处于接近。

### <a name="required-actions"></a>所需的操作

该驱动程序必须接受并传输重复的已发布的消息，即使由同一客户端发布。

### <a name="required-actions"></a>所需的操作


该驱动程序必须删除所有消息 （和回收这些资源） 从"Received"队列，如果客户端未发送更换[ **IOCTL\_NFP\_获取\_下一步\_已订阅\_消息**](https://msdn.microsoft.com/library/windows/hardware/jj853319)以前 IOCTL 完成后 10 到 20 秒内。

## <a name="unresponsive-or-misbehaving-clients"></a>无响应或行为不正确的客户端


如果客户端无法发送所需[ **IOCTL\_NFP\_获取\_下一步\_传输\_消息**](https://msdn.microsoft.com/library/windows/hardware/jj853320) 10 个段的请求到二十秒钟的时间\[10-20 秒\]，则驱动程序应假定客户端将消失。 正常情况下，客户端应刷新其请求一秒内还\[1s\]。 如果发生这种情况，驱动程序必须将"CompleteEventImmediately"计数器设置为零，必须递增计数器，直到客户端唤醒，并将所需的 IRP 发送。

### <a name="required-actions"></a>所需的操作

该驱动程序必须设置"CompleteEventImmediately"计数器为零，必须递增计数器，如果客户端未发送更换[ **IOCTL\_NFP\_获取\_下一步\_传输\_消息**](https://msdn.microsoft.com/library/windows/hardware/jj853320)以前 IOCTL 完成后 10 到 20 秒内。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
[邻近 DDI 引用附近](https://msdn.microsoft.com/library/windows/hardware/jj866056)  

