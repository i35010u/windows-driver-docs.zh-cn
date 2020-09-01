---
title: 广播驱动程序体系结构属性、事件和方法集
description: 广播驱动程序体系结构属性、事件和方法集
ms.assetid: 4323c19a-e47d-4ec6-a39c-3f2e95c526e4
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d8df76c6e9cd61b3953ecaf535cef93a233b680
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192409"
---
# <a name="broadcast-driver-architecture-property-event-and-method-sets"></a>广播驱动程序体系结构属性、事件和方法集


## <span id="ddk_broadcast_driver_architecture_property_event_and_method_sets_ks"></span><span id="DDK_BROADCAST_DRIVER_ARCHITECTURE_PROPERTY_EVENT_AND_METHOD_SETS_KS"></span>


本部分记录 BDA 微型驱动程序实现的属性、事件和方法集。 这些集是在 *bdamedia*中定义的。 BDA 微型驱动程序可以将这些集中的一些属性和方法发送到 BDA 支持库中的默认实现。 有关详细信息，请参阅 [广播驱动程序体系结构微型驱动程序](./broadcast-driver-architecture-minidrivers.md) 。有关微型驱动程序如何使用 BDA 支持库来提供这些集的默认处理的信息，请参阅。

以下各节提供了有关 BDA 属性、事件和方法集的详细信息：

<span id="KSPROPSETID_BdaAutodemodulate"></span><span id="kspropsetid_bdaautodemodulate"></span><span id="KSPROPSETID_BDAAUTODEMODULATE"></span>[KSPROPSETID \_ BdaAutodemodulate](kspropsetid-bdaautodemodulate.md)  
BDA autodemodulate 属性集控制可以自动确定调制信号和 demodulate 特征的信号解调器节点。

<span id="KSPROPSETID_BdaCA"></span><span id="kspropsetid_bdaca"></span><span id="KSPROPSETID_BDACA"></span>[KSPROPSETID \_ BdaCA](kspropsetid-bdaca.md)  
BDA 条件访问属性集查询授权控制消息 (ECM)  (UI) 要显示的 "状态" 或 "用户界面" 节点。

<span id="KSEVENTSETID_BdaCAEvent"></span><span id="kseventsetid_bdacaevent"></span><span id="KSEVENTSETID_BDACAEVENT"></span>[KSEVENTSETID \_ BdaCAEvent](kseventsetid-bdacaevent.md)  
BDA 条件访问事件集会将 (CA) 插件的条件性访问通知到状态更改或要检索和显示的 UI 的存在情况。

<span id="KSMETHODSETID_BdaChangeSync"></span><span id="ksmethodsetid_bdachangesync"></span><span id="KSMETHODSETID_BDACHANGESYNC"></span>[KSMETHODSETID \_ BdaChangeSync](ksmethodsetid-bdachangesync.md)  
BDA 更改同步方法集会同时对一个筛选器或其引脚和节点提交多个更改。

<span id="KSMETHODSETID_BdaDeviceConfiguration"></span><span id="ksmethodsetid_bdadeviceconfiguration"></span><span id="KSMETHODSETID_BDADEVICECONFIGURATION"></span>[KSMETHODSETID \_ BdaDeviceConfiguration](ksmethodsetid-bdadeviceconfiguration.md)  
"BDA 设备配置" 方法集配置已连接筛选器的实际拓扑。

<span id="KSPROPSETID_BdaDigitalDemodulator"></span><span id="kspropsetid_bdadigitaldemodulator"></span><span id="KSPROPSETID_BDADIGITALDEMODULATOR"></span>[KSPROPSETID \_ BdaDigitalDemodulator](kspropsetid-bdadigitaldemodulator.md)  
BDA 数字解调器属性集控制无法自动确定调制信号特征的信号解调器节点。

<span id="KSPROPSETID_BdaFrequencyFilter"></span><span id="kspropsetid_bdafrequencyfilter"></span><span id="KSPROPSETID_BDAFREQUENCYFILTER"></span>[KSPROPSETID \_ BdaFrequencyFilter](kspropsetid-bdafrequencyfilter.md)  
BDA frequency 筛选器属性集控制接收方拓扑中的 RF 调谐器节点。

<span id="KSPROPSETID_BdaLNBInfo"></span><span id="kspropsetid_bdalnbinfo"></span><span id="KSPROPSETID_BDALNBINFO"></span>[KSPROPSETID \_ BdaLNBInfo](kspropsetid-bdalnbinfo.md)  
 (LNB 的 BDA 低噪音块) 属性集向 RF 调谐器提供有关附属 dish 的 LNB 设备的信息。

<span id="KSPROPSETID_BdaNullTransform"></span><span id="kspropsetid_bdanulltransform"></span><span id="KSPROPSETID_BDANULLTRANSFORM"></span>[KSPROPSETID \_ BdaNullTransform](kspropsetid-bdanulltransform.md)  
"BDA null 转换" 属性集通知节点通过未更改传递信号。

<span id="KSPROPSETID_BdaPIDFilter"></span><span id="kspropsetid_bdapidfilter"></span><span id="KSPROPSETID_BDAPIDFILTER"></span>[KSPROPSETID \_ BdaPIDFilter](kspropsetid-bdapidfilter.md)  
BDA 数据包标识符 (PID) filter 属性集控制 PID 筛选器节点。 PID 筛选器节点从收到的广播流筛选掉不需要的流。

<span id="KSPROPSETID_BdaPinControl"></span><span id="kspropsetid_bdapincontrol"></span><span id="KSPROPSETID_BDAPINCONTROL"></span>[KSPROPSETID \_ BdaPinControl](kspropsetid-bdapincontrol.md)  
"BDA pin 控制" 属性集可从该 pin 检索 pin 属性。

<span id="KSEVENTSETID_BdaPinEvent"></span><span id="kseventsetid_bdapinevent"></span><span id="KSEVENTSETID_BDAPINEVENT"></span>[KSEVENTSETID \_ BdaPinEvent](kseventsetid-bdapinevent.md)  
BDA 引脚事件集通知其他筛选器或与 pin 相关的事件的插件。

<span id="KSPROPSETID_BdaSignalStats"></span><span id="kspropsetid_bdasignalstats"></span><span id="KSPROPSETID_BDASIGNALSTATS"></span>[KSPROPSETID \_ BdaSignalStats](kspropsetid-bdasignalstats.md)  
"BDA 信号统计信息" 属性集从控制节点或 pin 检索信号统计信息。 若要从 pin 获取信号统计信息，请**NodeId**将 KSP \_ 节点结构的节点2成员设置为−1。

<span id="KSPROPSETID_BdaTableSection"></span><span id="kspropsetid_bdatablesection"></span><span id="KSPROPSETID_BDATABLESECTION"></span>[KSPROPSETID \_ BdaTableSection](kspropsetid-bdatablesection.md)  
当在节点的输出上传递数据时，"BDA 表" 部分属性集向节点提供了一个要使用的节点。

<span id="KSPROPSETID_BdaTopology"></span><span id="kspropsetid_bdatopology"></span><span id="KSPROPSETID_BDATOPOLOGY"></span>[KSPROPSETID \_ BdaTopology](kspropsetid-bdatopology.md)  
BDA 拓扑属性集检索筛选器中的节点功能和连接。

<span id="KSPROPSETID_BdaVoidTransform"></span><span id="kspropsetid_bdavoidtransform"></span><span id="KSPROPSETID_BDAVOIDTRANSFORM"></span>[KSPROPSETID \_ BdaVoidTransform](kspropsetid-bdavoidtransform.md)  
BDA void 转换属性集控制节点启动和停止运行的时间。

**注意**   可在 Windows XP 和更高版本上使用 BDA 属性、事件和方法集。 仅当在该平台上安装了 DirectX 9.0 和更高版本时，才可在 Windows 2000 平台上使用这些集。

 

 

