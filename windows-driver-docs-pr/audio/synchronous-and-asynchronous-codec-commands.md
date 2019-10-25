---
title: 同步和异步编解码器命令
description: 同步和异步编解码器命令
ms.assetid: c37cc94d-37eb-4a3e-b7ae-63fed8827d21
keywords:
- TransferCodecVerbs
- 编解码器命令 WDK 音频
- HD 音频、编解码器命令
- 高清晰音频（HD 音频），编解码器命令
- 同步编解码器命令 WDK 音频
- 异步编解码器命令 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38d6d87722d4b914b00821e9a2723e48462c1af9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830100"
---
# <a name="synchronous-and-asynchronous-codec-commands"></a>同步和异步编解码器命令


[**TransferCodecVerbs**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-ptransfer_codec_verbs)例程允许功能驱动程序将命令发送到连接到 HD 音频控制器的音频和调制解调器编解码器。 编解码器命令可以同步或异步执行：

-   如果对[**TransferCodecVerbs**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-ptransfer_codec_verbs)的调用提交了要同步处理的命令的列表，则仅当编解码器或编解码器处理完所有命令后，例程才会返回。

-   如果对[**TransferCodecVerbs**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-ptransfer_codec_verbs)的调用提交要异步处理的命令的列表，则当 HD 音频总线驱动程序将命令添加到其内部命令队列后，例程将立即返回，而不会等待编解码器或编解码器处理这些命令。 编解码器处理完命令后，总线驱动程序会通过调用回调例程通知函数驱动程序。

函数驱动程序使用以下一种或多种方法从编解码器检索响应，具体取决于它所发送的编解码器命令的性质：

-   如果函数驱动程序必须具有来自编解码器的响应，然后才能执行任何其他处理，则它将使用同步模式。

-   如果函数驱动程序无需等待编解码器命令完成，则若要查看编解码器响应并了解命令何时完成，则它将使用异步模式，忽略回调例程（对于编解码器命令的存储除外），并放弃或忽略对编解码器命令的响应。

-   如果函数驱动程序必须知道编解码器命令完成的时间，但不需要查看响应，则它将使用异步模式并依赖回调例程进行通知。 但是，它会丢弃或忽略对编解码器命令的响应。 回调例程可能使用[内核流式处理（KS）事件](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-events)将通知发送到驱动程序的主要部分。

-   如果函数驱动程序必须知道何时完成了编解码器命令和响应，但必须立即继续处理而不是等待命令完成，则它将使用异步模式并避免读取响应，直到接收回调例程。 回调例程或驱动程序的主要部分都可以检查响应。

如果[*TransferCodecVerbs*](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-ptransfer_codec_verbs)成功地将命令列表添加到总线驱动程序的内部命令队列中，则它将返回成功状态\_成功。 即使调用成功，响应可能仍然无效。 函数驱动程序必须检查编解码器响应中的状态位，以确定它们是否有效。 此规则适用于同步和异步模式。

无效响应的原因可能是下列其中一项：

-   命令未到达编解码器。

-   编解码器做出响应，但当 RIRB 中发生先进先出（FIFO）溢出时，响应就会丢失。

后一个问题表明 RIRB FIFO 的大小不足。

每个编解码器响应都包含一个**IsValid**标志，用于指示响应是否有效，以及指示是否发生了 RIRB FIFO 溢出的**HasFifoOverrun**标志。 如果**IsValid** = 0，指示响应无效， **HasFifoOverrun**标志可帮助确定故障的根源：

-   如果**HasFifoOverrun** = 0，则编解码器在所需的时间间隔内未能响应。 可能的原因是该命令从未到达编解码器。

-   如果**HasFifoOverrun** = 1，则该命令可能已到达编解码器，但由于 FIFO 溢出，响应丢失。

在调用*TransferCodecCommands*期间，调用方提供指向[**HDAUDIO\_编解码器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_codec_transfer)的数组的指针\_传输结构。 每个结构都包含一个命令，并为响应提供空间。 总线驱动程序始终将每个响应写入结构中，该结构包含触发响应的命令。

对于每个对*TransferCodecCommands*的调用，处理命令的顺序取决于命令在数组中的顺序。 处理第一个命令之前，处理数组中的第一个命令始终完成，依此类推。

此外，如果客户端对*TransferCodecCommands*进行异步调用，然后再次调用*TransferCodecCommands* ，而无需等待第一次调用的回调例程，这两组命令的相对顺序处理两个调用时，由客户端提交两组命令的顺序定义。 因此，在开始处理第二次调用中的命令之前，总线驱动程序会处理第一个调用中的所有命令。

但两个不同的函数驱动程序实例发送的命令的相对顺序是不确定的。 （每个实例都有自己的物理设备对象。）例如，如果实例1调用*TransferCodecCommands*来发送命令 a、b 和 C （顺序为 a、b 和 c），并且实例2调用*TransferCodecCommands*以 x y z 顺序发送命令 x、Y 和 Z，则总线驱动程序可能会执行顺序： X-Y-Z-C。

当单独的函数驱动程序线程共享同一组硬件资源的访问权限时，来自不同驱动程序线程的命令的相对顺序可能非常重要。 如果是这样，则函数驱动程序负责同步线程之间的资源共享。

例如，将数据字节序列写入编解码器的硬件接口可能包含索引注册和8位数据寄存器。 首先，函数驱动程序提交编解码器命令，以将起始索引加载到索引寄存器。 接下来，驱动程序提交一个命令，将第一个字节的数据写入数据寄存器。 索引注册将在每次连续写入数据时递增，直到传输完成。 但是，如果两个驱动程序线程无法正确地同步其索引和数据寄存器的访问，则这两个线程的单个寄存器访问的相对顺序是不确定的，可能的结果是数据损坏或硬件无效configuration.

这两个版本的 HD audio DDI 都提供[*TransferCodecVerbs*](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-ptransfer_codec_verbs)例程。

 

 




