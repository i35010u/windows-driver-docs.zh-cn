---
title: 广播驱动程序体系结构属性、 事件和方法集
description: 广播驱动程序体系结构属性、 事件和方法集
ms.assetid: 4323c19a-e47d-4ec6-a39c-3f2e95c526e4
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c1f6c9ddf7941cc9cd6a2b8a0f68d76d1b1cc9d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521093"
---
# <a name="broadcast-driver-architecture-property-event-and-method-sets"></a>广播驱动程序体系结构属性、 事件和方法集


## <span id="ddk_broadcast_driver_architecture_property_event_and_method_sets_ks"></span><span id="DDK_BROADCAST_DRIVER_ARCHITECTURE_PROPERTY_EVENT_AND_METHOD_SETS_KS"></span>


本部分介绍 BDA 微型驱动程序实现的属性、 事件和方法集。 这些设置中定义*bdamedia.h*。 BDA 微型驱动程序可以调度的一些属性并在这些集中到 BDA 支持库中的默认实现的方法。 有关详细信息，请参阅[广播驱动程序体系结构微型驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff556588)微型驱动程序如何使用函数 BDA 支持库提供两个集的默认处理。

以下各节提供有关 BDA 属性、 事件和方法集的详细信息：

<span id="KSPROPSETID_BdaAutodemodulate"></span><span id="kspropsetid_bdaautodemodulate"></span><span id="KSPROPSETID_BDAAUTODEMODULATE"></span>[KSPROPSETID\_BdaAutodemodulate](kspropsetid-bdaautodemodulate.md)  
BDA autodemodulate 属性设置控件可自动确定调制的信号的特征和解调信号解调器节点。

<span id="KSPROPSETID_BdaCA"></span><span id="kspropsetid_bdaca"></span><span id="KSPROPSETID_BDACA"></span>[KSPROPSETID\_BdaCA](kspropsetid-bdaca.md)  
BDA 条件性访问设置的属性查询状态或用户界面 (UI) 来显示有关的授权控件消息 (ECM) 站点地图节点。

<span id="KSEVENTSETID_BdaCAEvent"></span><span id="kseventsetid_bdacaevent"></span><span id="KSEVENTSETID_BDACAEVENT"></span>[KSEVENTSETID\_BdaCAEvent](kseventsetid-bdacaevent.md)  
BDA 条件性访问事件集通知条件性访问 (CA) 插件以更改状态或关于 UI，以检索并显示存在可选的。

<span id="KSMETHODSETID_BdaChangeSync"></span><span id="ksmethodsetid_bdachangesync"></span><span id="KSMETHODSETID_BDACHANGESYNC"></span>[KSMETHODSETID\_BdaChangeSync](ksmethodsetid-bdachangesync.md)  
BDA 更改同步方法集同时提交多个更改在筛选器或其 pin 和节点上。

<span id="KSMETHODSETID_BdaDeviceConfiguration"></span><span id="ksmethodsetid_bdadeviceconfiguration"></span><span id="KSMETHODSETID_BDADEVICECONFIGURATION"></span>[KSMETHODSETID\_BdaDeviceConfiguration](ksmethodsetid-bdadeviceconfiguration.md)  
BDA 设备配置方法集配置连接筛选器的实际拓扑。

<span id="KSPROPSETID_BdaDigitalDemodulator"></span><span id="kspropsetid_bdadigitaldemodulator"></span><span id="KSPROPSETID_BDADIGITALDEMODULATOR"></span>[KSPROPSETID\_BdaDigitalDemodulator](kspropsetid-bdadigitaldemodulator.md)  
BDA 数字解调器属性设置控制不能自动确定调制的信号的特征的信号解调器节点。

<span id="KSPROPSETID_BdaFrequencyFilter"></span><span id="kspropsetid_bdafrequencyfilter"></span><span id="KSPROPSETID_BDAFREQUENCYFILTER"></span>[KSPROPSETID\_BdaFrequencyFilter](kspropsetid-bdafrequencyfilter.md)  
BDA 频率筛选器属性设置控制 RF 调谐器节点接收方拓扑中。

<span id="KSPROPSETID_BdaLNBInfo"></span><span id="kspropsetid_bdalnbinfo"></span><span id="KSPROPSETID_BDALNBINFO"></span>[KSPROPSETID\_BdaLNBInfo](kspropsetid-bdalnbinfo.md)  
BDA 低干扰块 (LNB) 属性集提供了有关卫星电视的 LNB 设备的信息与 RF 调谐器。

<span id="KSPROPSETID_BdaNullTransform"></span><span id="kspropsetid_bdanulltransform"></span><span id="KSPROPSETID_BDANULLTRANSFORM"></span>[KSPROPSETID\_BdaNullTransform](kspropsetid-bdanulltransform.md)  
BDA null 转换属性集通知节点将通过不变的信号。

<span id="KSPROPSETID_BdaPIDFilter"></span><span id="kspropsetid_bdapidfilter"></span><span id="KSPROPSETID_BDAPIDFILTER"></span>[KSPROPSETID\_BdaPIDFilter](kspropsetid-bdapidfilter.md)  
BDA 数据包标识符 (PID) 筛选器属性设置控制 PID 筛选器节点。 PID 筛选器节点筛选出不需要从接收到广播流的流。

<span id="KSPROPSETID_BdaPinControl"></span><span id="kspropsetid_bdapincontrol"></span><span id="KSPROPSETID_BDAPINCONTROL"></span>[KSPROPSETID\_BdaPinControl](kspropsetid-bdapincontrol.md)  
BDA pin 控件属性集检索从该 pin 的 pin 的属性。

<span id="KSEVENTSETID_BdaPinEvent"></span><span id="kseventsetid_bdapinevent"></span><span id="KSEVENTSETID_BDAPINEVENT"></span>[KSEVENTSETID\_BdaPinEvent](kseventsetid-bdapinevent.md)  
其他筛选器或插件的 pin 与相关的事件会通知 BDA pin 事件集。

<span id="KSPROPSETID_BdaSignalStats"></span><span id="kspropsetid_bdasignalstats"></span><span id="KSPROPSETID_BDASIGNALSTATS"></span>[KSPROPSETID\_BdaSignalStats](kspropsetid-bdasignalstats.md)  
BDA 信号统计信息属性集的控件节点或 pin 中检索信号统计信息。 若要获取 pin 从信号统计信息，请设置**NodeId**成员的 KSP 的\_到 − 1 的节点结构。

<span id="KSPROPSETID_BdaTableSection"></span><span id="kspropsetid_bdatablesection"></span><span id="KSPROPSETID_BDATABLESECTION"></span>[KSPROPSETID\_BdaTableSection](kspropsetid-bdatablesection.md)  
BDA 表部分属性集提供到节点上的节点的输出传递数据时要使用表部分。

<span id="KSPROPSETID_BdaTopology"></span><span id="kspropsetid_bdatopology"></span><span id="KSPROPSETID_BDATOPOLOGY"></span>[KSPROPSETID\_BdaTopology](kspropsetid-bdatopology.md)  
BDA 拓扑属性集检索的节点功能和筛选器中建立的连接。

<span id="KSPROPSETID_BdaVoidTransform"></span><span id="kspropsetid_bdavoidtransform"></span><span id="KSPROPSETID_BDAVOIDTRANSFORM"></span>[KSPROPSETID\_BdaVoidTransform](kspropsetid-bdavoidtransform.md)  
节点启动和停止操作时，设置控件 BDA void 转换属性。

**请注意**   BDA 属性、 事件和方法集是适用于 Windows XP 及更高版本。 这些设置是适用于 Windows 2000 平台只有当在该平台上安装了 DirectX 9.0 和更高版本。

 

 

 





