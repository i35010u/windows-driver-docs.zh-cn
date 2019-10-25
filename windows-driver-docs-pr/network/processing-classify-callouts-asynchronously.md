---
title: 以异步方式处理分类标注
description: 以异步方式处理分类标注
ms.assetid: 1026f917-7b21-4b01-8cfd-4d14e92106fe
keywords:
- 异步处理 WFP 分类标注 WDK Windows 筛选平台
- Windows 筛选平台标注驱动程序 WDK，异步处理分类标注
- 挂起的 WFP 分类标注 WDK Windows 筛选平台
- 分类标注 WDK Windows 筛选平台，异步处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f029c730dafb842ed99a49dd1e7189731c03dfb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843492"
---
# <a name="processing-classify-callouts-asynchronously"></a>以异步方式处理分类标注


WFP 标注驱动程序可以通过返回操作类型 **.fwp\_操作**来授权或拒绝网络操作，或允许或丢弃网络数据包，\_允许、 **.fwp\_操作\_CONTINUE**或 **.fwp\_操作 @no_** [*classifyFn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_classify_fn0)标注函数的 _t_8_ 块。 通常，标注驱动程序无法从其*classifyFn*函数返回检查决策，直到指示的信息（如 classifiable 字段、元数据或数据包）可以转发给另一个组件（例如用户模式）。程序. 在这些情况下，可能需要在以后的某个时间异步做出决定。

### <a name="general-rules-for-asynchronous-processing"></a>异步处理的一般规则

WFP 支持*classifyFn*标注函数的异步处理。 但是，执行此操作的机制因不同的层而异。

<a href="" id="asynchronous-ale-classify-------"></a>**异步 ALE 分类**   
标注驱动程序必须从*classifyFn*调用[**FwpsPendOperation0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpspendoperation0)函数。 必须通过调用[**FwpsCompleteOperation0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpscompleteoperation0)函数来完成异步操作。

<a href="" id="asynchronous-packet-classify-------"></a>**异步数据包分类**   
标注驱动程序应从*classifyFn*函数返回 **\_块的 .fwp\_操作**， **FWPS\_分类\_** ，\_吸收标志集。 必须引用或克隆网络数据包。 异步操作是通过 reinjecting 克隆或修改的数据包或通过无提示丢弃数据包来完成的。

<a href="" id="asynchronous-ale-classify-that-includes-packets-------"></a>**异步 ALE 分类，包括数据包**   
使用前两个过程的组合： "分类" 操作挂起，并引用或克隆数据包，稍后对*classifyFn*的调用完成，克隆的数据包将被重新插入文本或丢弃。

### <a name="special-cases-and-considerations"></a>特殊情况和注意事项

<a href="" id="ale-connect-vs--receive-accept-layers-------"></a>**ALE 连接与接收/接受层**   
当调用**FwpsCompleteOperation0**来完成 ALE 连接层上挂起的分类操作时（**FWPS\_层\_ale\_AUTH\_连接\_V4**或**FWPS\_\_ALE\_身份验证\_连接\_V6**），将在各自的 ale 连接层触发 ALE 重新授权分类操作。 标注驱动程序应根据此重新授权分类操作返回检查决定。 您可以通过检查是否 **\_已设置了\_\_条件标志\_，** 来检测 ALE 重新授权分类操作。

标注驱动程序必须为每个挂起的 ALE\_身份验证\_连接分类操作维护一种独特的状态，以便能够在**FwpsCompleteOperation0**触发的过程中查找每个分类操作的检查决策重新授权. 如果在挂起的 ALE\_AUTH\_连接分类操作（例如，对于非 TCP 连接）时引用或克隆数据包，则可以在重新授权之后重新插入文本。

在**FwpsCompleteOperation0**的过程中，如果在 ALE 接收/接受层（**FWPS\_层\_ale\_authentication\_接收\_\_V4**或**FWPS\_层进行分类操作时调用ALE\_AUTH\_接收\_ACCEPT\_V6**）， **FwpsCompleteOperation0**不会触发 ALE 重新授权。 如果修改不太重要而无法绕过筛选器，则在克隆的数据包重新插入文本传入时，将再次调用*classifyFn* 。 允许来自 ALE\_\_的自注入克隆可以有效地授权传入连接。 如果不允许传入连接，请在调用**FwpsCompleteOperation0**后丢弃传入的数据包。

<a href="" id="ale-reauthorization-------"></a>**ALE 重新授权**   
对于事件（例如，在层中添加或删除筛选器）、检测新的到达接口以及使用 IPsec 重新加密连接，可以在 ALE 连接或接收/接受层上对标注驱动程序进行重新分类。 无法通过调用**FwpsCompleteOperation0**来挂起此类重新授权，这不是必需的。 标注驱动程序应使用前面列出的规则来处理在重新授权期间指示的数据包。

请注意，传入和传出数据包都可以在 ALE\_authentication\_CONNECT 或 ALE\_接收\_接受层之间进行重新授权。 例如，可以在 ALE\_AUTH\_CONNECT 层上重新授权传入的数据包。 标注驱动程序不得假设数据包的方向与连接方向相同。

<a href="" id="ale-flow-established-layers-------"></a> **\_建立的层的 ALE\_流**   
这些层不支持异步处理（**FWPS\_层\_ALE\_流\_已建立\_V4**或**FWPS\_\_\_V6\_**

<a href="" id="inbound-transport-layers-------"></a>**入站\_传输层**   
标注驱动程序不得在传入（入站）传输层（**FWPS\_层\_入站\_传输\_V4**或**FWPS\_层上需要 ALE 分类处理的数据包进行异步处理\_入站\_传输\_V6**）。 这样做可能会干扰流创建。 当 WFP 在传入传输层调用*classifyFn* callout 函数时，它会将**FWPS\_元数据设置\_字段\_ALE\_分类**需要 ALE 分类的那些数据包\_必需标志字处理. 标注驱动程序应该允许来自入站\_传输层的此类数据包，并应将处理延迟，直到它们达到 ALE\_接收\_接受层。

<a href="" id="stream-layers-------"></a>**流层**   
在流层（**FWPS\_层\_stream\_V4**或**FWPS\_层\_流\_V6**），指示 TCP 数据段而不是 IP 或 TCP 标头。 流层还可以在一次调用*classifyFn* callout 函数时指示网络缓冲区列表的链。 WFP 为要使用的流层标注提供专用的克隆和注入函数（ [**FwpsCloneStreamData0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsclonestreamdata0)和[**FwpsStreamInjectAsync0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsstreaminjectasync0)）。

由于流层数据的按序送达性质，如果任何流数据仍处于挂起状态，则标注驱动程序必须继续克隆和吸收数据。 为给定流流混合使用异步和同步操作可能导致未定义的行为。

 

 





