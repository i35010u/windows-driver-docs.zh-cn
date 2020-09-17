---
title: 时钟同步
description: 时钟同步
ms.assetid: dc0071b0-a22c-4bb5-90ea-a69e5dcdba6f
keywords:
- 合成 WDK 音频，时钟同步
- 时钟 WDK 音频，同步
- 延迟 WDK 音频，时钟
- 时间 WDK 音频
- 引用时钟 WDK 音频
- 示例时钟 WDK 音频
- 波形接收器音频，时钟同步
- 偏移时间 WDK 音频
- 主时钟 WDK 音频，同步
- 阶段锁定的循环 WDK 音频
- 同步 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b9b41901f9da34aa98176ca62fbfbbd15cac4b1
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90714818"
---
# <a name="clock-synchronization"></a>时钟同步


## <span id="clock_synchronization"></span><span id="CLOCK_SYNCHRONIZATION"></span>


波形接收器的一项关键任务就是解决时钟与 crystals 之间的时间偏差。 它通过与阶段锁定的循环等效的软件来实现此操作。

波形接收器跟踪缓冲区中可向下写入的示例数。 因此，即使它知道它已打开（例如，示例20），波形接收器仍需要检查主时钟以获取引用时间。 它有一个线程，该线程大约每20毫秒唤醒一次，并向当前时间请求主时钟。 例如，主时钟可能会报告当前时间 (以毫秒为单位) 为420。

波形接收器还会保持延迟时钟，这会根据主时钟和采样时间显示当前时间之间的偏移量。 它使用此信息来计算预期的主时钟时间，并将其与实际的主时钟读取进行比较，以查看两个时钟是否已偏移。

波形接收器使用相位锁定循环来调整示例时间。 检查偏移量时，波形接收器不会按整个量进行调整，因为读数包含一定的抖动。 相反，它会将示例时钟移动到与主时钟接近的某个部分。 通过这种方式，wave 接收器平滑了抖动错误，同时保持大致同步。它还需要此时间，并将其转换为相对于主时钟的延迟时钟时间。 这一点很重要，因为应用程序可能需要知道合成器在任何位置呈现的位置。

延迟时钟会向应用程序通知最早的时间，可以安排新便笺的播放时间。 延迟时钟时间是主时钟时间加上表示合成器滞后时间的偏移量。 此延迟表示应用程序提交要播放到合成器实际播放便笺的时间的最小延迟时间。 无论何时，应用程序都可以计划在或晚于--但不早于--当前延迟时钟时间播放的便笺。

例如，如果主时钟当前处于时间420，并且应用程序有一个要尽快运行的注释，则延迟时钟会将便笺通知给它最早的播放时间。 如果软件合成器的延迟为100毫秒，则下一次它可以在时间520运行。

假设某个事件被标记为在引用时间520时播放。 合成器通过将注释向下呈示为样本并在采样时执行其所有计算来完成工作。 因此，它需要知道引用时间520在采样时转换为。 在用户模式下，波形接收器提供两个合成使用的函数：

[**IDirectMusicSynthSink::SampleToRefTime**](/windows/win32/api/dmusics/nf-dmusics-idirectmusicsynthsink-sampletoreftime)

[**IDirectMusicSynthSink::RefTimeToSample**](/windows/win32/api/dmusics/nf-dmusics-idirectmusicsynthsink-reftimetosample)

若要在这种情况下执行转换，合成会在波形接收器上调用 **IDirectMusicSynthSink：： RefTimeToSample** 。

然后，波形接收器回 (例如 600) 的采样时间。 相关注释在采样时600。 然后，当该 [**IDirectMusicSynth：： Render**](/windows/win32/api/dmusics/nf-dmusics-idirectmusicsynth-render) 方法获取由波形接收器调用以呈现流的下一部分时 (例如，从采样时间600到 800) ，该注释将在采样600时呈现到缓冲区中。

**注意**   示例时间保留为64位数字，以避免滚动更新。  (DWORD 值滚动27小时。 ) 

 

概括而言，合成会在样本时间内完成其所有的内部数学计算，而波形接收器会从引用时间转换到样本时间，反之亦然。 波形接收器还管理与主时钟的同步，并提供滞后时间信息。 在 wave 接收器中隐藏此功能可以更轻松地编写合成合成。

 

