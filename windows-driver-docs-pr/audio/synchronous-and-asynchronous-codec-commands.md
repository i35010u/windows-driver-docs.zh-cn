---
title: 同步和异步编解码器命令
description: 同步和异步编解码器命令
ms.assetid: c37cc94d-37eb-4a3e-b7ae-63fed8827d21
keywords:
- TransferCodecVerbs
- 编解码器命令 WDK 音频
- HD 音频编解码器命令
- 高清晰度音频 (HD Audio) 编解码器命令
- 同步的编解码器命令 WDK 音频
- 异步编解码器命令 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04c30120d4704271e6f36585ac930eeebf2742d6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354212"
---
# <a name="synchronous-and-asynchronous-codec-commands"></a>同步和异步编解码器命令


[ **TransferCodecVerbs** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-ptransfer_codec_verbs)例程允许函数驱动程序将命令发送到已连接到高清晰度音频控制器的音频和调制解调器编解码器。 同步或异步，可以执行的编解码器命令：

-   如果调用[ **TransferCodecVerbs** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-ptransfer_codec_verbs)提交一系列命令是同步处理编解码器后，才返回的例程或编解码器已处理的所有命令。

-   如果调用[ **TransferCodecVerbs** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-ptransfer_codec_verbs)提交一系列命令是以异步方式处理例程返回只要 HD Audio 总线驱动程序会将命令而不添加到其内部命令队列，正在等待的编解码器或编解码器来处理命令。 编解码器有处理这些命令后，总线驱动程序通知功能驱动程序通过调用回调例程。

具体取决于它将发送的编解码器命令的性质，函数驱动程序将使用一个或多个以下方法来检索从编解码器的响应：

-   如果功能驱动程序必须拥有来自编解码器的响应，它可以执行任何其他处理，则使用同步模式。

-   如果功能驱动程序不需要等待编解码器命令来完成，若要查看的编解码器响应，并了解这些命令完成，然后，它使用异步模式下，将忽略回调例程 （除外，若要释放的编解码器命令的存储）并放弃或忽略的编解码器命令的响应。

-   如果编解码器的命令完成，但不需要以查看响应时，必须知道功能驱动程序，然后它使用的异步模式，并依赖于通知的回调例程。 但是，它会丢弃或忽略的编解码器命令的响应。 可以使用回调例程[流式处理 (KS) 事件的内核](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-events)若要将通知发送到该驱动程序的主要部分。

-   如果编解码器命令完成并响应，但必须立即处理，而不是等待命令来完成恢复时，功能驱动程序必须了解两者，然后使用异步模式并可避免直到它读取响应接收回调例程。 回调例程或驱动程序的主要部分可以检查响应。

[*TransferCodecVerbs* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-ptransfer_codec_verbs)将返回状态\_成功，如果成功添加到总线驱动程序的内部命令队列的命令的列表中。 即使调用成功，响应仍可能无效。 功能驱动程序必须检查以确定它们是否有效的编解码器响应中的状态位。 此规则适用于同步和异步模式。

无效的原因是响应的，可能需要以下项之一：

-   该命令未达到编解码器。

-   编解码器回复，但是，响应已丢失时第一个中，先出 (FIFO) 溢出发生 RIRB 中。

后一个问题表示 RIRB 先进先出的足够的大小。

每个编解码器的响应包含**IsValid**标志，用于指示响应是否有效并**HasFifoOverrun**标志，用于指示是否已发生 RIRB FIFO 溢出。 如果**IsValid** = 0，指示响应无效的**HasFifoOverrun**标志有助于识别失败的原因：

-   如果**HasFifoOverrun** = 0，则该编解码器所需的时间间隔内响应而失败。 可能的原因是该命令永远不会到达编解码器。

-   如果**HasFifoOverrun** = 1，则该命令可能达到编解码器，但响应是由于 FIFO 溢出而丢失。

在调用期间*TransferCodecCommands*，调用方提供一个指针指向的数组[ **HDAUDIO\_编解码器\_传输**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_codec_transfer)结构。 每个结构包含的命令，并提供响应的空间。 总线驱动程序始终将每个响应写入到包含触发响应的命令的结构。

每次调用*TransferCodecCommands*，命令的处理的顺序由数组中的命令的顺序决定。 始终处理数组中的第一个命令完成之前处理第二个命令将开始，依次类推。

此外，如果客户端进行异步调用，向*TransferCodecCommands* ，然后调用*TransferCodecCommands*第二次而无需等待将首次调用的回调例程由客户端在其中提交命令的两个组的顺序定义的两次调用的命令的两个组的处理的相对顺序。 因此，总线驱动程序处理的所有第一次调用中的命令之前将开始处理第二次调用中的命令。

但是，由两个不同的函数的驱动程序实例发送命令的相对顺序是未定义。 （每个实例有其自己的物理设备对象。）例如，如果实例 1 将调用*TransferCodecCommands*发送命令 A、 B 和 C A B C 的顺序和实例 2 电话*TransferCodecCommands*发送命令 X、 Y 和 Z 顺序 X Y Z，则总线驱动程序可能会按顺序 A-X-Y-B-Z-C 执行命令。

当单独的函数驱动程序线程都共享相同的硬件资源集的访问从不同的驱动程序线程的命令的相对顺序可能重要。 如果是这样，功能驱动程序负责同步在线程之间资源共享。

例如，用于编写一系列数据字节编解码器可能包含的索引寄存器和 8 位数据的硬件接口注册。 首先，功能驱动程序提交编解码器命令加载到索引寄存器的起始索引。 接下来，驱动程序提交命令以将数据的第一个字节写入到的数据寄存器。 以下每个后续写入到数据的索引寄存器增量注册直到传输完成。 但是，如果两个驱动程序线程无法正确同步其访问的索引和数据寄存器，由两个线程的单个注册访问权限的相对顺序是不确定，结果可能是数据损坏或无效的硬件配置。

[ *TransferCodecVerbs* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-ptransfer_codec_verbs)例程是 HD 音频 DDI 的这两个版本中可用。

 

 




