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
ms.openlocfilehash: 18644a3283d40ecc94dc558f2bf6ab2f6a945db9
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215200"
---
# <a name="processing-classify-callouts-asynchronously"></a>以异步方式处理分类标注


WFP 标注驱动程序可以通过从[*classifyFn*](/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_classify_fn0) callout 函数返回操作类型 " **.fwp \_ 操作 \_ 允许**"、"继承** \_ 操作 \_ 继续**" 或 " **.fwp \_ 操作 \_ 块**"，来授权或拒绝网络操作，或允许或放弃网络数据包。 通常，标注驱动程序无法从其 *classifyFn* 函数返回检查决策，直到指示的信息（如 classifiable 字段、元数据或数据包）可以转发给其他组件（如用户模式应用程序）处理。 在这些情况下，可能需要在以后的某个时间异步做出决定。

### <a name="general-rules-for-asynchronous-processing"></a>异步处理的一般规则

WFP 支持 *classifyFn* 标注函数的异步处理。 但是，执行此操作的机制因不同的层而异。

<a href="" id="asynchronous-ale-classify-------"></a>**异步 ALE 分类**   
标注驱动程序必须从*classifyFn*调用[**FwpsPendOperation0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpspendoperation0)函数。 必须通过调用 [**FwpsCompleteOperation0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpscompleteoperation0) 函数来完成异步操作。

<a href="" id="asynchronous-packet-classify-------"></a>**异步数据包分类**   
标注驱动程序应从*classifyFn*函数返回 **.fwp \_ 操作 \_ 块**，并将**FWPS \_ 标记为 \_ \_ \_ 吸收**标志。 必须引用或克隆网络数据包。 异步操作是通过 reinjecting 克隆或修改的数据包或通过无提示丢弃数据包来完成的。

<a href="" id="asynchronous-ale-classify-that-includes-packets-------"></a>**包含数据包的异步 ALE 分类**   
使用前两个过程的组合： "分类" 操作挂起，并引用或克隆数据包，稍后对 *classifyFn* 的调用完成，克隆的数据包将被重新插入文本或丢弃。

### <a name="special-cases-and-considerations"></a>特殊情况和注意事项

<a href="" id="ale-connect-vs--receive-accept-layers-------"></a>**ALE 连接与接收/接受层**   
当调用 **FwpsCompleteOperation0** 来完成 ALE 连接层上的挂起的分类操作时 (**FWPS \_ 层 \_ ale \_ 身份验证 \_ 连接 \_ V4** 或 **FWPS \_ 层 \_ ale \_ 身份验证连接) \_ \_ V6** 。 标注驱动程序应根据此重新授权分类操作返回检查决定。 您可以通过检查是否设置了 " **.Fwp 条件" 标志是否 \_ \_ \_ 为 \_ 重新授权** 标志来检测 ALE 重新授权分类操作。

标注驱动程序必须为每个挂起的 ALE \_ 身份验证连接分类操作维护一个独特的状态 \_ ，以便可以在 **FwpsCompleteOperation0**触发的重新授权期间查找每个分类操作的检查决定。 如果在挂起的 ALE \_ 身份验证连接分类操作期间引用或克隆数据包 \_ (例如，对于非 TCP 连接) ，可以在重新授权之后重新插入文本。

当在 **FwpsCompleteOperation0** 中使用分类操作在 ALE 接收/接受 (层调用时， **FWPS \_ 层 \_ ale \_ 身份验证 \_ 接收 \_ accept \_ V4** 或 **FWPS \_ 层 \_ ale 身份验证 \_ \_ 接收 \_ accept \_ V6**) ， **FwpsCompleteOperation0** 不触发 ALE 重新授权。 如果修改不太重要而无法绕过筛选器，则在克隆的数据包重新插入文本传入时，将再次调用 *classifyFn* 。 允许从 ALE 接收接受层中自行注入的克隆会 \_ \_ 有效地授权传入连接。 如果不允许传入连接，请在调用 **FwpsCompleteOperation0**后丢弃传入的数据包。

<a href="" id="ale-reauthorization-------"></a>**ALE 重新授权**   
标注驱动程序可以在 ALE 连接或接收/接受层上对事件（如策略 (更改）进行重新分类（例如，在层) 添加或删除筛选器），检测新的到达接口，并使用 IPsec 重新对连接进行加密。 无法通过调用 **FwpsCompleteOperation0**来挂起此类重新授权，这不是必需的。 标注驱动程序应使用前面列出的规则来处理在重新授权期间指示的数据包。

请注意，可以在 ALE \_ 身份验证 \_ 连接或 ale \_ 接收 \_ 接受层上重新授权传入和传出数据包。 例如，可以在 ALE \_ 身份验证连接层重新授权传入的数据包 \_ 。 标注驱动程序不得假设数据包的方向与连接方向相同。

<a href="" id="ale-flow-established-layers-------"></a>**ALE \_ 流 \_ 建立的层**   
这些层不支持异步处理 (**FWPS \_ 层 \_ ale \_ 流建立的 \_ \_ V4** 或 **FWPS \_ 层 \_ ale \_ 流建立的 \_ \_ V6**) 。

<a href="" id="inbound-transport-layers-------"></a>**入站 \_ 传输层**   
标注驱动程序不得在传入 (入 () 站 ** \_ \_ \_ 传输 \_ V4** 或 **FWPS \_ 层入站传输 \_ \_ \_ V6**) 的传入入站传输 V4 或层时，对需要 ALE 分类处理的数据包进行异步处理。 这样做可能会干扰流创建。 当 WFP 在传入传输层调用 *classifyFn* callout 函数时，它会为需要 ALE 分类处理的数据包设置 **FWPS \_ METADATA \_ 字段 \_ ALE \_ 分类 \_ 必需** 标志。 标注驱动程序应该允许来自入站传输层的此类数据包 \_ ，并应将其处理延迟，直到它们达到 ALE \_ 接收 \_ 接受层。

<a href="" id="stream-layers-------"></a>**流层**   
在流层 (**FWPS \_ 层 \_ 流 \_ V4** 或 **FWPS \_ 层 \_ 流 \_ V6**) ，将指示 TCP 数据段而不是 IP 或 TCP 标头。 流层还可以在一次调用 *classifyFn* callout 函数时指示网络缓冲区列表的链。 WFP 为要使用的流层标注提供专用的克隆和注入函数（ [**FwpsCloneStreamData0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsclonestreamdata0) 和 [**FwpsStreamInjectAsync0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsstreaminjectasync0)）。

由于流层数据的按序送达性质，如果任何流数据仍处于挂起状态，则标注驱动程序必须继续克隆和吸收数据。 为给定流流混合使用异步和同步操作可能导致未定义的行为。

 

