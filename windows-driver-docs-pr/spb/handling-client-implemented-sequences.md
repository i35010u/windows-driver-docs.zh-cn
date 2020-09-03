---
title: 处理客户端实现的序列
description: 可选的 EvtSpbControllerLock 和 EvtSpbControllerUnlock 事件回调函数执行互补运算。
ms.assetid: C1DED853-059D-481F-A524-E50772072018
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 703700f7b76034c0c620458ee41dbfc0f92d19d9
ms.sourcegitcommit: c766ab74e32eb44795cbbd1a4f352d3a6a9adc14
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89389595"
---
# <a name="handling-client-implemented-sequences"></a>处理客户端实现的序列


可选的 [*EvtSpbControllerLock*](/windows-hardware/drivers/ddi/spbcx/nc-spbcx-evt_spb_controller_lock) 和 [*EvtSpbControllerUnlock*](/windows-hardware/drivers/ddi/spbcx/nc-spbcx-evt_spb_controller_unlock) 事件回调函数执行互补运算。 *EvtSpbControllerLock*函数是用于[**IOCTL \_ SPB \_ 锁 \_ 控制器**](https://msdn.microsoft.com/library/windows/hardware/hh450858)请求的处理程序。 *EvtSpbControllerUnlock*函数是用于[**IOCTL \_ SPB \_ 解锁 \_ 控制器**](https://msdn.microsoft.com/library/windows/hardware/hh450859)请求的处理程序。 客户端 (即，总线上的外围设备的驱动程序) 将这些请求发送到开始和结束 [i/o 传输序列](./i-o-transfer-sequences.md)。 大多数 SPB 控制器驱动程序不支持 **ioctl \_ spb \_ 锁定 \_ 控制器** 和 **ioctl \_ spb \_ 解锁 \_ 控制器** 请求，因此，不实现 *EvtSpbControllerLock* 和 *EvtSpbControllerUnlock* 函数。

客户端可以将 i/o 传输序列作为一系列简单传输请求来执行， (即 [**IRP \_ mj \_ 读取**](../kernel/irp-mj-read.md) 和 [**irp \_ mj \_ 写入**](../kernel/irp-mj-write.md) 请求) 。 序列中的第一次传输必须在 **IOCTL \_ SPB \_ 锁 \_ 控制器** 请求之前，此请求会告知 SPB 控制器驱动程序在 i/o 传输序列期间锁定总线。 最后一个传输必须后跟 **IOCTL \_ SPB \_ UNLOCK \_ 控制器** 请求，通知驱动程序对总线进行解锁。 这种类型的 i/o 传输序列称为 [客户端实现的序列](./i-o-transfer-sequences.md#client-implemented-sequences) ，用于将其与 [单请求序列](./i-o-transfer-sequences.md#single-request-sequences)区分开来，该顺序使用 [**ioctl \_ spb \_ 执行 \_ 序列**](https://msdn.microsoft.com/library/windows/hardware/hh450857) 请求，而不是使用 **ioctl \_ spb \_ LOCK \_ 控制器** 和 **ioctl \_ spb \_ 解锁 \_ 控制器** 请求。

虽然外围设备的驱动程序持有总线上的锁，但总线控制器允许访问总线上的任何其他外围设备。 总线锁定操作的详细信息取决于总线类型。 对于 i2c 控制器，传输方向的更改 (读取后跟随写入，反之亦然) 需要执行 I-C 重新启动操作。 对于 SPI 控制器，当控制器锁定有效时，芯片选择目标设备必须保持不变。 有关详细信息，请参阅 [原子总线操作](./atomic-bus-operations.md)。

支持客户端实现的传输序列是可选的。 如果控制器可以执行以下操作，则你的 SPB 控制器驱动程序应声明仅支持它们：

-   在客户端实现的序列的持续时间内锁定总线。
-   随时解锁总线。 例如，如果在字节传输之间发生解锁请求，则控制器应能够解锁总线，而不会等待总线上的下一个字节传输。

锁定总线时，客户端可以发送任意顺序的简单传输请求。 也就是说，序列可以是任意长度，可以是读写的任意组合。

为了指示支持客户端实现的序列，SPB 控制器驱动程序实现了 *EvtSpbControllerUnlock* 函数。 如果你的驱动程序实现了此功能，则 SPB framework 扩展 (SpbCx) 接受来自客户端的 **ioctl \_ spb \_ 锁定 \_ 控制器** 和 **ioctl \_ spb \_ 解锁 \_ 控制器** 请求。 否则，SpbCx 会通过完成状态为 " \_ 不支持" 状态代码的请求来失败这些请求 \_ 。

实现 *EvtSpbControllerUnlock* 函数的 SPB 控制器驱动程序无需实现 *EvtSpbControllerLock* 函数。 但是，实现 *EvtSpbControllerLock* 函数的 SPB 控制器驱动程序还必须实现 *EvtSpbControllerUnlock* 函数。

如果驱动程序实现了 *EvtSpbControllerUnlock* 函数而不是 *EvtSpbControllerLock* 函数，SpbCx 将调用 *EvtSpbControllerUnlock* 函数来处理 **ioctl \_ spb \_ 解锁 \_ 控制器** 请求，但只需完成具有状态成功状态代码的 **ioctl \_ spb \_ 锁 \_ 控制器** 请求即可 \_ 。

你的驱动程序有两种方法来检测客户端实现的序列的开始。 首先，如果驱动程序实现了 *EvtSpbControllerLock* 函数，SpbCx 将调用此函数来处理来自客户端的 **IOCTL \_ SPB \_ 锁 \_ 控制器** 请求。 该驱动程序可依赖于在序列中第一个传输请求之前发生的此调用。 其次，如果您的驱动程序未实现 *EvtSpbControllerLock* 函数，则当驱动程序处理来自客户端的简单传输请求时，驱动程序可以调用 [**SpbRequestGetParameters**](/windows-hardware/drivers/ddi/spbcx/nf-spbcx-spbrequestgetparameters) 方法。 若要指示请求的传输为序列中的第一个传输，此方法会将该方法的输出结构中的 **Position** 成员设置为 **SpbRequestSequencePositionFirst**。

*EvtSpbControllerUnlock*回调是驱动程序可以确定序列何时结束的唯一方法。 不实现 *EvtSpbControllerUnlock* 函数的驱动程序不支持客户端实现的序列。

 

