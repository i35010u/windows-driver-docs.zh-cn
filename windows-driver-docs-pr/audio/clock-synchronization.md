---
title: 时钟同步
description: 时钟同步
ms.assetid: dc0071b0-a22c-4bb5-90ea-a69e5dcdba6f
keywords:
- 合成器 WDK 音频、 时钟同步
- 时钟 WDK 音频同步
- 延迟 WDK 音频、 时钟
- 时间 WDK 音频
- 引用时钟 WDK 音频
- 示例时钟 WDK 音频
- 批接收器 WDK 音频、 时钟同步
- 偏移量时间 WDK 音频
- 主时钟 WDK 音频，同步
- 阶段锁定循环 WDK 音频
- 同步 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6fdbc238053392478af94f198a3faa36d6162ea1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333870"
---
# <a name="clock-synchronization"></a>时钟同步


## <span id="clock_synchronization"></span><span id="CLOCK_SYNCHRONIZATION"></span>


若要执行的批接收器的关键任务是解析引用时钟和水晶重新排列，示例时钟之间的时间偏移。 做到这一点与阶段锁定循环的软件等效项。

跟踪的缓冲区它可以将写入到下一步中哪些示例数的批接收器。 因此即使它知道它位于，例如，示例 20，批接收器仍需要检查 master 的时钟，以获得引用时间。 它具有大约每隔 20 毫秒被唤醒，并要求提供当前时间主时钟的线程。 当前时间 （以毫秒为单位） 是 420，例如，主时钟可能会返回报告。

批接收器还维护延迟时钟，其中显示了根据主时钟的当前时间的示例时间之间的偏移量。 它使用此信息来计算预期主时钟时间，并将此与实际主时钟阅读，请参阅是否两个时钟有偏差分开进行比较。

批接收器使用阶段锁定循环来调整采样时间。 在检查时偏差，批接收器不调整的整个数量，因为读数中包含的一些抖动。 相反，它将示例时钟移动由入 master 时钟的距离的某些部分。 这样一来，批接收器保持大致保持同步时平滑处理，从而解决抖动错误。它还采用这一次，并将其转换为相对于主时钟延迟时钟时间。 这非常重要，因为该应用程序可能需要知道其中合成器呈现任何位置。

延迟时钟告诉应用程序将在其中可以计划新便笺播放的最早时间。 主时钟时间加上偏移量，表示合成器的延迟，延迟时钟时间。 这种延迟表示从应用程序提交新便笺合成器实际玩便笺的时间要播放的时间短的延迟时间。 在任何时刻，该应用程序可以计划下为播放在或更高版本比-但不是能早于-当前延迟时钟时间。

例如，如果当前在时 420 是主时钟并且该应用程序下，其目的是尽可能快地播放，延迟时钟会指示它可以播放注意的最早时间。 如果软件合成器具有 100 毫秒的延迟，在时间 520 进行下一次它可以播放便笺。

假设事件进行标记，以便在时间 520 引用时播放。 合成器通过向下的说明呈现为示例和示例及时执行所有计算来实现其工作。 因此，它需要知道 520 引用时间的示例时间的转换。 在用户模式下，批接收器提供合成器使用的两个函数：

[**IDirectMusicSynthSink::SampleToRefTime**](https://msdn.microsoft.com/library/windows/hardware/ff536526)

[**IDirectMusicSynthSink::RefTimeToSample**](https://msdn.microsoft.com/library/windows/hardware/ff536525)

若要执行转换在这种情况下，合成器调用**IDirectMusicSynthSink::RefTimeToSample**批接收器上。

然后批接收器并发回采样时间 (例如，600)。 在示例时 600 获取呈现问题的说明。 然后，当合成[ **IDirectMusicSynth::Render** ](https://msdn.microsoft.com/library/windows/hardware/ff536541)批接收器来呈现的下一部分 （例如，从示例时间 600 到 800） 的流调用方法，请注意呈现到在示例时 600 的缓冲区。

**请注意**  采样时间保留为 64 位数字，以避免滚动更新。 （DWORD 值滚动 27 小时内。）

 

总之，合成器执行其内部的所有数学示例时间并批接收器都执行转换为示例时间从引用时间，反之亦然。 批接收器还管理同步主制并提供延迟信息。 隐藏批接收器中的此功能使得编写更容易合成器。

 

 




