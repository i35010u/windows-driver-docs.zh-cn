---
title: Windows 10 新增功能的音频驱动程序
description: 本主题提供了什么是适用于 Windows 10 的音频中的新增功能的高级别摘要。
ms.assetid: 9005966A-CCC2-478C-9221-56007B7FADFB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 502b99e61f97df9585478d4a02fda524acdb72fb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328458"
---
# <a name="windows-10-whats-new-for-audio-drivers"></a>Windows 10：What's New for 音频驱动程序


本主题提供了什么是适用于 Windows 10 的音频中的新增功能的高级别摘要。

## <a name="span-idfeaturesummaryspanspan-idfeaturesummaryspanspan-idfeaturesummaryspanfeature-summary"></a><span id="Feature_Summary"></span><span id="feature_summary"></span><span id="FEATURE_SUMMARY"></span>功能摘要


下面是 Windows 10 中的新音频功能。

-   [实现音频模块通信](implementing-audio-module-communication.md)

-   [较低的延迟音频改进](#lowlatency)

-   [信号处理模式和音频的类别](#signalprocessing)

-   [硬件卸载 APO 效果](#hardwareoffloaded)

-   [Cortana 语音激活](#cortanavoice)

-   [Windows 音频的通用驱动程序](#windowsuniversal)

-   [音频驱动程序的资源管理](#resourcemanagement)

-   [即插即用重新平衡的音频驱动程序](#pnprebalance)

## <a name="span-idlowlatencyspanspan-idlowlatencyspanspan-idlowlatencyspanlow-latency-audio-improvements"></a><span id="LowLatency"></span><span id="lowlatency"></span><span id="LOWLATENCY"></span>较低的延迟音频改进


音频的滞后时间是创建该声音的时间之间的延迟和时听说过。 具有较低的音频延迟是非常重要的几个主要方案，如下所示。

-   Pro 音频
-   音乐创建和混合
-   例如 Skype 通信
-   增强现实虚拟
-   游戏

设备的总滞后时间是以下组件的延迟的总和：

-   操作系统
-   音频处理对象
-   音频驱动程序
-   音频硬件

Windows 10 中已完成工作以减少在 OS 中的延迟。 无需更改任何驱动程序，Windows 10 中的应用程序将遇到 4.5 16ms年较低的延迟。 此外，如果已更新的驱动程序以利用新的低延迟 DDIs 使用小缓冲区处理音频数据，然后将滞后时间将减少更多。 如果驱动程序支持 3 毫秒音频缓冲区，则往返延迟的情况是 ~ 10 毫秒。

![显示应用程序、 音频引擎驱动程序和硬件的低延迟音频堆栈关系图](images/low-latency-audio-stack-diagram-1.png)

音频堆栈支持多个数据包大小和动态包大小调整，以优化延迟与 power 根据用户的方案之间的权衡。 此外，流将设置优先级，以确保高优先级流 （例如电话呼叫） 具有专用资源。

为了使音频驱动程序以支持较低的延迟，Windows 10 提供了以下 3 个新功能：

1. \[必需\]声明在每个模式下支持的最小缓冲区大小。
2. \[可选的但建议\]提高驱动程序和操作系统之间数据流的协调。
3. \[可选的但建议\]注册驱动程序资源 （中断、 线程），以便它们可以受到低延迟方案中的操作系统。
有关详细信息，请参阅[低滞后时间的音频](low-latency-audio.md)。

## <a name="span-idsignalprocessingspanspan-idsignalprocessingspanspan-idsignalprocessingspansignal-processing-modes-and-audio-categories"></a><span id="SignalProcessing"></span><span id="signalprocessing"></span><span id="SIGNALPROCESSING"></span>信号处理模式和音频的类别


**信号处理模式**

驱动程序声明支持的音频信号处理模式下为每个设备。

（所选应用程序） 的音频类别将映射到音频模式 （由驱动程序定义）。 Windows 定义了七个音频信号处理模式。 Oem 和 Ihv 可以确定他们想要实现的模式。 如下所示的表总结了模式。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><strong>模式</strong></td>
<td align="left"><strong>呈现/捕获</strong></td>
<td align="left"><strong>说明</strong></td>
</tr>
<tr class="even">
<td align="left">原始</td>
<td align="left">两者</td>
<td align="left"><p>Raw 模式指定不应不进行任何应用于流的信号处理。</p>
<p>应用程序可以请求将完全保持不变的原始流并执行其自己的信号处理。</p></td>
</tr>
<tr class="odd">
<td align="left">默认</td>
<td align="left">两者</td>
<td align="left"><p>此模式下定义的默认音频处理。</p></td>
</tr>
<tr class="even">
<td align="left">电影 *</td>
<td align="left">呈现</td>
<td align="left">电影音频播放</td>
</tr>
<tr class="odd">
<td align="left">媒体 *</td>
<td align="left">两者</td>
<td align="left">音频播放音乐 （大多数媒体流的默认值）</td>
</tr>
<tr class="even">
<td align="left">语音 *</td>
<td align="left">捕获</td>
<td align="left">（例如输入 Cortana） 的人的语音捕获</td>
</tr>
<tr class="odd">
<td align="left">通信 *</td>
<td align="left">两者</td>
<td align="left">VOIP 呈现并捕获 （例如 Skype、 Lync）</td>
</tr>
<tr class="even">
<td align="left">通知 *</td>
<td align="left">呈现</td>
<td align="left">铃声，警报、 警报等。</td>
</tr>
</tbody>
</table>

 

音频设备驱动程序需要至少支持 Raw 或默认模式。 在支持其他模式是可选的。

语音、 电影、 音乐和通信的专用的模式。 音频驱动程序将能够定义不同类型的音频格式和处理，根据流类型。

**音频类别**

下表显示 Windows 10 中的音频的类别。

有关音频流的使用情况情况通知给系统，以便应用程序可以选择以标记与特定的音频流类别流。 Windows 10 中有九个音频流类别。

|                |                                                                                                       |
|----------------|-------------------------------------------------------------------------------------------------------|
| **类别**   | **说明**                                                                                       |
| 电影\*        | 电影、 视频中，对话框 (替换 ForegroundOnlyMedia)                                              |
| 媒体\*        | 媒体的播放 (替换 BackgroundCapableMedia) 的默认类别                                 |
| 游戏聊天\*    | 中的游戏用户之间的沟通 （Windows 10 中的新类别）                                      |
| 语音\*       | 语音输入 （例如个人助理） 和输出 （例如导航应用程序） （Windows 10 中的新类别） |
| Communications | VOIP，实时聊天                                                                                  |
| 警报         | 警报、 电话铃声、 通知                                                                       |
| 声音效果  | 嘟嘟声、 磕碰等等                                                                                     |
| 游戏的媒体     | 在游戏的音乐                                                                                         |
| 游戏效果   | 球跳动，汽车引擎声音、 项目符号，等等。                                                      |
| 其他          | 未分类的流                                                                                 |

 

\* Windows 10 中的新增功能。

有关详细信息请参阅[音频信号处理模式](audio-signal-processing-modes.md)并[音频处理对象体系结构](audio-processing-object-architecture.md)。

## <a name="span-idhardwareoffloadedspanspan-idhardwareoffloadedspanspan-idhardwareoffloadedspanhardware-offloaded-apo-effects"></a><span id="HardwareOffloaded"></span><span id="hardwareoffloaded"></span><span id="HARDWAREOFFLOADED"></span>硬件卸载 APO 效果


Windows 10 支持硬件卸载 APO 效果。 不可以加载在卸载 pin 之上。 这允许音频处理在软件和硬件中完成。 此外，在处理可能会动态变化。 部分或全部处理可从移动软件 APO 到 DSP 有足够的硬件资源时，且然后移回软件 APO DSP 中的负载会增加。

有关详细信息，请参阅[实现硬件卸载 APO 效果](implementing-hardware-offloaded-apo-effects.md)。

## <a name="span-idcortanavoicespanspan-idcortanavoicespanspan-idcortanavoicespancortana-voice-activation---wake-on-voice"></a><span id="CortanaVoice"></span><span id="cortanavoice"></span><span id="CORTANAVOICE"></span>Cortana 语音激活-唤醒语音

Cortana，个人助理技术 2013年中已在 Microsoft BUILD 开发人员会议的第一个 demonstarted。 语音激活是一项功能，使用户能够通过说特定内容中的调用语音识别引擎从各种设备的电源状态"你好，小娜"。 "你好，小娜"语音激活 (VA) 功能允许用户快速的体验 (例如，Cortana) 吸引他或她 （即，什么是当前在屏幕上） 的活动上下文之外使用他或她的声音。 该功能被针对方案屏幕时关闭，空闲或完全处于活动状态。 如果硬件支持缓冲，用户可以然后链接的关键短语和命令短语在一起。 这可以提高端到端唤醒用户语音体验。 有关详细信息，请参阅[语音激活](voice-activation.md)。

## <a name="span-idwindowsuniversalspanspan-idwindowsuniversalspanspan-idwindowsuniversalspanwindows-universal-drivers-for-audio"></a><span id="WindowsUniversal"></span><span id="windowsuniversal"></span><span id="WINDOWSUNIVERSAL"></span>Windows 音频的通用驱动程序


Windows 10 支持适用于 PC 和 2:1 的一个驱动程序模型和 Windows 10 适用于手机和平板电脑小屏幕。 这意味着 Ihv 可以开发一个平台中的其驱动程序和该驱动程序适用于所有设备 （台式计算机、 便携式计算机、 平板电脑、 手机）。 结果是减少的开发时间和成本。

若要开发通用音频驱动程序，使用以下工具：

1. Visual Studio 2015:新的驱动程序设置，在"目标平台"设置为"通用"，以创建多平台驱动程序。
2. APIValidator:这是一种 WDK 工具，检查是否为通用驱动程序，并突出显示了需要更新的调用。
3. 在 GitHub 中的音频示例：Sysvad 和 SwapAPO 都已转换为通用驱动程序。
有关详细信息和指向 GitHub 示例代码，请参阅[音频的通用 Windows 驱动程序](audio-universal-drivers.md)。

## <a name="span-idresourcemanagementspanspan-idresourcemanagementspanspan-idresourcemanagementspanresource-management-for-audio-drivers"></a><span id="ResourceManagement"></span><span id="resourcemanagement"></span><span id="RESOURCEMANAGEMENT"></span>音频驱动程序的资源管理


在低成本的移动设备上创建很好的音频体验的难题之一是某些设备具有各种并发约束。 例如，就可以支持仅 2 没有负载的流和该设备只能同时播放最多 6 个音频流。 当在移动设备上有活动的电话呼叫时，就可以在设备支持只有 2 个音频流。 当设备捕获音频时，设备只能播放最多 4 个音频流。

Windows 10 包含一种机制来表达并发约束以确保高优先级音频流和移动电话网络使用电话呼叫将能够播放。 如果系统没有足够的资源，然后终止低优先级的流。 此机制才在手机和平板电脑不在台式机或便携式计算机中可用。

有关详细信息，请参阅[音频硬件资源管理](audio-hardware-resource-management.md)。

## <a name="span-idpnprebalancespanspan-idpnprebalancespanspan-idpnprebalancespanpnp-rebalance-for-audio-drivers"></a><span id="PNPRebalance"></span><span id="pnprebalance"></span><span id="PNPREBALANCE"></span>即插即用重新平衡的音频驱动程序


即插即用重新平衡是方案中使用某些 PCI 需要重新分配内存资源。 在这种情况下，某些驱动程序都卸载、，然后重新加载在不同的内存位置，若要创建可用连续内存空间。 可以在两个主要方案中触发再平衡：

1. PCI 热插拔：用户插入设备和 PCI 总线不具有足够的资源来加载新设备的驱动程序。 属于此类别的设备的一些示例包括闪电、 USB C 和 NVME 存储。 在此方案中，内存资源需要重新排列和合并 (rebalanced) 以支持要添加的其他设备。
2. PCI 可调整其大小栏：设备的驱动程序已成功加载到内存中后，它请求的其他资源。 设备的一些示例包括高端的图形卡和存储设备。
有关详细信息，请参阅[实现 PnP 重新平衡 PortCls 音频驱动程序](implement-pnp-rebalance-for-portcls-audio-drivers.md)。

 

 




