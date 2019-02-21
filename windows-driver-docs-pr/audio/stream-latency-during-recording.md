---
title: 录制期间的 Stream 延迟
description: 录制期间的 Stream 延迟
ms.assetid: b9391b34-acd8-4434-b00c-48bbbc0b6647
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 36f1f5f4987e239ea0c05949b580bf1e7c2b81b5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540953"
---
# <a name="stream-latency-during-recording"></a>录制期间的 Stream 延迟


运行状态的音频记录流时，很小 WaveRT 端口驱动程序的角色。 在录制过程中，如下图中所示的音频设备捕获音频数据，并将其写入到循环缓冲区。 音频引擎然后从缓冲区读取此数据。 此活动无需干预从端口驱动程序。 换而言之，音频数据的音频硬件和用户模式应用程序之间直接流动而无需涉及到的任何内核模式软件组件。

下图中的记录和读取位置不断进度从左到右作为流流经缓冲区。 当记录或读取的位置到达缓冲区末尾时，它会绕到缓冲区的起始位置。

![说明录制流的延迟的关系图](images/wavert-record.png)

上图中标识*记录位置*作为示例，当前正在录制的音频设备 （从通过模拟到数字转换器或 ADC 麦克风捕获） 的缓冲区位置。 请注意，将记录位置到其中的音频设备后将写入该示例通过先进先出的未来的缓冲区位置。 *读取位置*是音频引擎从中读取下一个示例的缓冲区位置。

音频设备捕获在 ADC 的音频示例，直到客户端读取它的时间的延迟时间是只需记录和读取的位置之间的分离。 这种分离是以下的延迟源的总和 (标记为 A 和 B 在关系图中):

**延迟的**:在捕获后 ADC 中的数据，音频设备将数据存储硬件 FIFO 直到它可以在循环缓冲区中写入数据。

**延迟 B**:音频设备将数据写入到循环缓冲区后，数据驻留在缓冲区中，直到客户端读取的数据。

客户端具有无法控制的完全取决于硬件的延迟。 典型的先进先出可能存储 ADC 从大约 64 示例。 但是，客户端执行控制延迟 B.产生延迟 B 太大带来不必要的延迟到系统，使其读取数据的太小风险太早，音频设备之前已写入到缓冲区。

尽管客户端可以设置一个计时器定期激活其缓冲区读取线程，但此方法不会获得的最小的延迟。 若要进一步降低延迟，客户端可以配置生成每次设备完成新捕获数据块写入缓冲区的硬件通知的音频设备。 在这种情况下，通过硬件通知而不是由计时器激活客户端线程。

通过让定期通知音频引擎的音频设备，客户端可以缩小延迟比其他实用。

客户端 （通常的音频引擎） 可以获取的音频设备有助于流延迟，发送的延迟问题的摘要[ **KSPROPERTY\_RTAUDIO\_HWLATENCY** ](https://msdn.microsoft.com/library/windows/hardware/ff537378)WaveRT 端口驱动程序的请求。

客户端确定分离以记录和读取位置之间维护量后，客户端监视中的记录的位置确定应滞后多少读取的位置的更改。 在 Windows Server 2008 和更高版本操作系统中，客户端发出[ **KSPROPERTY\_音频\_位置**](https://msdn.microsoft.com/library/windows/hardware/ff537297)或者[ **KSPROPERTY\_RTAUDIO\_POSITIONREGISTER** ](https://msdn.microsoft.com/library/windows/hardware/ff537381)属性请求以确定记录位置。 后一种方法是更高效，因为它允许客户端读取无转换到内核模式例程的信息，可直接将记录位置。

 

 




