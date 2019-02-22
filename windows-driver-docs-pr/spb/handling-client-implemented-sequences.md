---
title: 处理客户端实现序列
description: 可选 EvtSpbControllerLock 和 EvtSpbControllerUnlock 事件回调函数执行互为补充的操作。
ms.assetid: C1DED853-059D-481F-A524-E50772072018
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d391105da7f94c485b96594b946d16560ce12987
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542417"
---
# <a name="handling-client-implemented-sequences"></a>处理客户端实现序列


可选[ *EvtSpbControllerLock* ](https://msdn.microsoft.com/library/windows/hardware/hh450814)并[ *EvtSpbControllerUnlock* ](https://msdn.microsoft.com/library/windows/hardware/hh450816)事件回调函数执行的补充操作。 *EvtSpbControllerLock*函数是一个处理程序[ **IOCTL\_存储\_锁\_控制器**](https://msdn.microsoft.com/library/windows/hardware/hh450858)请求。 *EvtSpbControllerUnlock*函数是一个处理程序[ **IOCTL\_存储\_解锁\_控制器**](https://msdn.microsoft.com/library/windows/hardware/hh450859)请求。 客户端 （即，总线上外围设备的驱动程序） 将发送这些请求开始和结束[I/O 传输序列](https://msdn.microsoft.com/library/windows/hardware/hh450890)。 大多数存储控制器驱动程序不支持**IOCTL\_存储\_锁\_控制器**并**IOCTL\_存储\_解锁\_控制器**请求，因此，也不实现*EvtSpbControllerLock*并*EvtSpbControllerUnlock*函数。

客户端可以执行 I/O 传输序列作为一系列简单传输请求 (即[ **IRP\_MJ\_读取**](https://msdn.microsoft.com/library/windows/hardware/ff550794)并[ **IRP\_MJ\_编写**](https://msdn.microsoft.com/library/windows/hardware/ff550819)请求)。 序列中的第一个传输前必须加**IOCTL\_存储\_锁\_控制器**请求 — 此请求指示存储控制器驱动程序的 I/O 操作的持续时间内锁定总线传输序列。 最后一个传输必须后跟**IOCTL\_存储\_解锁\_控制器**请求，指示解锁总线驱动程序。 此类型的 I/O 传输序列称为[客户端实现序列](https://msdn.microsoft.com/library/windows/hardware/hh450890#buses-client-implemented-sequences)以便将其从[单请求序列](https://msdn.microsoft.com/library/windows/hardware/hh450890#buses-single-request-sequences)，使用[ **IOCTL\_存储\_EXECUTE\_序列**](https://msdn.microsoft.com/library/windows/hardware/hh450857)请求而不是**IOCTL\_存储\_锁\_控制器**和**IOCTL\_存储\_解锁\_控制器**请求。

虽然外围设备的驱动程序总线上持有的锁，总线控制器将允许总线上没有其他外围设备的访问权限。 总线锁定操作的详细信息取决于总线类型。 I²C 控制器，传输方向 （后跟执行写入操作，或者反之亦然读取） 的更改要求 I²C 重启操作。 对于 SPI 控制器到目标设备的芯片选择必须保持断言时控制器锁定保持有效。 有关详细信息，请参阅[总线的原子操作](https://msdn.microsoft.com/library/windows/hardware/jj850339)。

对客户端实现传输序列的支持是可选的。 存储控制器驱动程序应声明对其进行支持仅当控制器可以执行以下操作：

-   锁定持续时间内客户端实现序列总线。
-   在任何时候解锁总线。 例如，如果解除锁定请求字节传输之间发生，控制器应该是总线解锁而无需等待下一个字节传输通过总线。

锁定在总线时客户端可以发送任意简单传输请求序列。 也就是说，序列可以是任意长度，并可以是任意组合的读取和写入。

若要指示客户端实现序列的支持，存储控制器驱动程序实现*EvtSpbControllerUnlock*函数。 如果您的驱动程序实现此函数，存储框架扩展 (SpbCx) 接受**IOCTL\_存储\_锁\_控制器**并**IOCTL\_存储\_解锁\_控制器**来自客户端请求。 否则，SpbCx 失败这些请求通过完成并返回状态\_不\_支持状态代码。

实现的存储控制器驱动程序*EvtSpbControllerUnlock*函数不需要实现*EvtSpbControllerLock*函数。 但是，该实现的存储控制器驱动程序*EvtSpbControllerLock*函数还必须实现*EvtSpbControllerUnlock*函数。

如果您的驱动程序实现*EvtSpbControllerUnlock*函数但未*EvtSpbControllerLock*函数，SpbCx 调用*EvtSpbControllerUnlock*函数处理**IOCTL\_存储\_解锁\_控制器**请求，但只需完成**IOCTL\_存储\_锁\_控制器**请求的状态\_成功状态代码。

您的驱动程序提供两种方法来检测客户端实现的序列的开头。 首先，如果您的驱动程序实现*EvtSpbControllerLock*函数，SpbCx 调用此函数来处理**IOCTL\_存储\_锁\_控制器**请求从客户端。 该驱动程序可以依赖于此调用序列中的第一个传输请求之前发生。 其次，如果您的驱动程序不实现*EvtSpbControllerLock*函数，该驱动程序可以调用[ **SpbRequestGetParameters** ](https://msdn.microsoft.com/library/windows/hardware/hh450922)方法时，驱动程序处理从客户端的简单传输请求。 若要指示请求的传输是序列中的第一个传输，此方法设置**位置**方法中的成员的输出结构**SpbRequestSequencePositionFirst**。

*EvtSpbControllerUnlock*回调是驱动程序可以确定当序列结束时的唯一方法。 未实现的驱动程序*EvtSpbControllerUnlock*函数不能支持客户端实现的序列。

 

 




