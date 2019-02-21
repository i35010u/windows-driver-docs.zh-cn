---
title: AVStream 管道和线路
description: AVStream 管道和线路
ms.assetid: 7e4db0da-7faf-4155-ab9d-f8651db834ec
keywords:
- AVStream 分配器 WDK
- 分配器 WDK AVStream
- 用户模式下源 WDK AVStream
- 帧 WDK AVStream
- 转换筛选器 WDK AVStream
- 通过管道传递 WDK AVStream
- AVStream 管道 WDK
- 共享 WDK AVStream 的分配器
- 就地转换筛选器 WDK AVStream
- 源筛选器 WDK AVStream
- 呈现器筛选 WDK AVStream
- 非就地转换筛选器 WDK AVStream
- 线路 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 195d552a0c888a9dbf8faa0e61fd25da45c8e2e0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533578"
---
# <a name="avstream-pipes-and-circuits"></a>AVStream 管道和线路





一个*管道*是一组共享一个公共的 AVStream 筛选器[分配器](avstream-allocators.md)。

下图显示了管道组成三个 AVStream 筛选器： 源筛选器，*就地*转换筛选器和呈现器筛选器。

![说明使用 avstream 的所有筛选器管道的关系图](images/pipe1.png)

在此示例中， [KSProxy](https://msdn.microsoft.com/library/windows/hardware/ff560877) （未显示） 已选的分配器，由表示**Alloc**中图块。

AVStream 创建与源筛选器相关联的内部请求者对象。 在关系图中，会显示为的请求者**Req**。微型驱动程序中指定**AllocatorFraming**的成员[ **KSPIN\_描述符\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff563534)的内存和量连续类型若要将分配给一个帧的内存。 相应地，请求者从分配器获取帧，并将其传递给在线路中的下一个组件。

源筛选器的数据流入转换筛选器由另一个 AVStream 驱动程序实现。

最后，数据流入呈现器的筛选器由第三个 AVStream 筛选器实现。

因为所有球瓶中此图形都是 AVStream 插针，AVStream 使用它自己的内部传输接口而不是发送通过 Irp [ **IoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff548336)、 减少延迟并提高性能.

具体而言，导致时应用程序转换为图形[ **KSSTATE\_ACQUIRE** ](https://msdn.microsoft.com/library/windows/hardware/ff566856) (例如，当用户单击**播放**GraphEdit 中)，AVStream 直接连接的筛选器队列，如上所示。

因此，发送下游帧返回给请求者，其中它们可以在回收时呈现已完成。 此 AVStream 数据路径*线路*。

请考虑第二个示例中，在下图中，在其中转换筛选器不是 AVStream 筛选器，但仍是内核模式筛选器所示。

![说明使用非 avstream 内核模式转换筛选器管道的关系图](images/pipe2.png)

在第一个示例中，此示例包含三个筛选器： AVStream 源，KS 转换 （这可能是直接使用 KS 的驱动程序或流类下的微型驱动程序） 和 AVStream 呈现器。

如第一个图例中所示的第一次互连球瓶。 当筛选器关系图将转换为**KSSTATE\_ACQUIRE**，但是，内核流式处理 1.0 筛选器不支持 AVStream 传输接口。 因此，AVStream 未跳过的 pin;相反，它必须使用 I/O 的筛选器之间移动数据。

具体而言，当一个帧离开源筛选器的队列，AVStream 调用[ **IoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff548336)。 在此调用中， *Irp*参数包含要将源的输出插针从传递到转换筛选器的框架。

当呈现器的输入插针接收 IRP 时，pin 将 IRP 放在队列中。 完成后该呈现器驱动程序框架，它返回帧到呈现器的输入插针第二个示例中所示。

AVStream 现在调用[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)返回上游的帧。 源筛选器的输出插针接收完成通知。 微型驱动程序的[ *pin 进程回调*](https://msdn.microsoft.com/library/windows/hardware/ff556351)然后可以调用例程[ **KsStreamPointerUnlock** ](https://msdn.microsoft.com/library/windows/hardware/ff567137)并将帧移回请求者若要回收到线路。

请考虑在该框架源是在用户模式下的最后一个示例。 （或者，最后一帧目标可以是在用户模式下。）

下面，内核模式的图示*非就地*转换筛选器从用户模式下 DirectShow 筛选器接收的帧并将转换后的帧发送到内核模式 AVStream 呈现器：

![说明框架从用户模式下源接收和发送到 avstream 呈现器的关系图](images/pipe3.png)

当帧从用户模式下，AVStream pin 对象会将它们放在输入的管道部分的队列中。

非就地转换筛选器分配内核模式中转换后的框架，然后这些帧与线路使用第二个管道。 呈现器是一个 AVStream 筛选器，因为 AVStream 绕过球瓶，并使用 AVStream 传输接口操作将直接在呈现筛选器的队列中的帧。

微型驱动程序可以[注入帧](frame-injection.md)到通过调用线路[ **KsPinSubmitFrame** ](https://msdn.microsoft.com/library/windows/hardware/ff563529)或者[ **KsPinSubmitFrameMdl**](https://msdn.microsoft.com/library/windows/hardware/ff563530). 如果微型驱动程序使用此方法，AVStream 请求者会收到帧由于这些调用，而不是从内核模式分配器。

 

 




