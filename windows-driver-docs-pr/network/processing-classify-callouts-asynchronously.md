---
title: 以异步方式处理分类标注
description: 以异步方式处理分类标注
ms.assetid: 1026f917-7b21-4b01-8cfd-4d14e92106fe
keywords:
- 异步处理的 WFP 分类标注 WDK Windows 筛选平台
- Windows 筛选平台标注驱动程序 WDK，异步处理的分类标注
- 挂起的 WFP 分类标注 WDK Windows 筛选平台
- 分类标注 WDK Windows 筛选平台，异步处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17932ca1577d5817bc23c46c5f7359424751429b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327707"
---
# <a name="processing-classify-callouts-asynchronously"></a>以异步方式处理分类标注


WFP 标注驱动程序可以授权或拒绝网络操作，或者承认或放弃网络数据包时，通过返回的操作类型**FWP\_操作\_允许**， **FWP\_操作\_继续**，或**FWP\_操作\_阻止**从[ *classifyFn* ](https://msdn.microsoft.com/library/windows/hardware/ff544890)标注函数。 经常标注驱动程序不能返回检查决策及其*classifyFn*函数指示的信息，如与可分类字段、 元数据或数据包，直至可以转发到另一个处理例如，用户模式应用程序的组件。 在这些情况下可能需要在稍后的某个时间以异步方式进行决策。

### <a name="general-rules-for-asynchronous-processing"></a>异步处理的一般规则

WFP 支持异步处理*classifyFn*标注函数。 但是，执行此操作的机制不同根据不同的层。

<a href="" id="asynchronous-ale-classify-------"></a>**异步 ALE 分类**   
标注驱动程序必须调用[ **FwpsPendOperation0** ](https://msdn.microsoft.com/library/windows/hardware/ff551199)函数从*classifyFn*。 必须通过调用完成异步操作[ **FwpsCompleteOperation0** ](https://msdn.microsoft.com/library/windows/hardware/ff551152)函数。

<a href="" id="asynchronous-packet-classify-------"></a>**异步数据包进行分类**   
标注驱动程序应返回**FWP\_操作\_阻止**从*classifyFn*函数，与**FWPS\_分类\_OUT\_标志\_消除**标志设置。 网络数据包必须引用或克隆。 异步操作完成 reinjecting 克隆或已修改数据包或以无提示方式丢弃该数据包。

<a href="" id="asynchronous-ale-classify-that-includes-packets-------"></a>**异步 ALE 分类，包括数据包**   
前两个过程结合使用： 分类操作被挂起，并引用该数据包或克隆，而是在某些时间更高版本调用*classifyFn*完成和重新插入或丢弃克隆的数据包。

### <a name="special-cases-and-considerations"></a>特殊事例和注意事项

<a href="" id="ale-connect-vs--receive-accept-layers-------"></a>**ALE Connect vs。接收/接受层**   
当**FwpsCompleteOperation0**调用以完成挂起分类 ALE 操作连接层 (**FWPS\_层\_ALE\_身份验证\_CONNECT\_V4**或**FWPS\_层\_ALE\_身份验证\_CONNECT\_V6**)，ALE 重新授权分类操作在触发各自的 ALE 连接层。 标注驱动程序应返回检查此重新授权决策对操作进行分类。 可以检测 ALE 重新授权对操作进行检查分类是否**FWP\_条件\_标志\_IS\_重新授权**设置标志。

标注驱动程序必须保持唯一的状态为每个挂起 ALE\_身份验证\_CONNECT 分类中此类操作为每个检查决策对操作进行分类的一种方法可以查找期间**FwpsCompleteOperation0**-触发重新授权。 如果引用或克隆期间挂起 ALE 数据包\_身份验证\_CONNECT 进行分类 （例如，对于非 TCP 连接） 的操作，它们发生重新授权后可以重新插入。

当**FwpsCompleteOperation0**称为过程与在接收/接受 ALE 层分类操作 (**FWPS\_层\_ALE\_身份验证\_收到\_ACCEPT\_V4**或**FWPS\_层\_ALE\_身份验证\_收到\_接受\_V6**)， **FwpsCompleteOperation0**不会触发 ALE 重新授权。 而是对的新调用*classifyFn*试时进行重新插入克隆的数据包传入如果修改不明显，无法绕过该筛选器。 允许自注入的克隆通过 ALE\_收到\_接受层有效授权传入连接。 如果不希望允许将传入连接，它会调用后放弃传入数据包**FwpsCompleteOperation0**。

<a href="" id="ale-reauthorization-------"></a>**ALE 重新授权**   
可以在 ALE 重新分类标注驱动程序连接或事件的策略更改 （例如，添加或删除筛选器在层），例如接收/接受层检测新到达接口，并重新键入连接使用 IPsec。 此类重新授权不能被挂起，通过调用**FwpsCompleteOperation0**，并不需要执行此操作。 标注驱动程序应使用以指示在重新授权过程的过程数据包上面列出的规则。

请注意该传入和传出数据包可以重新授权在 ALE\_身份验证\_CONNECT 或 ALE\_收到\_接受层。 例如，传入数据包也可以在 ALE 重新授权\_身份验证\_连接层。 标注驱动程序必须假定数据包的方向是连接的方向相同。

<a href="" id="ale-flow-established-layers-------"></a>**ALE\_流\_已建立层**   
在这些层不支持异步处理 (**FWPS\_层\_ALE\_流\_已建立\_V4**或**FWPS\_层\_ALE\_流\_已建立\_V6**)。

<a href="" id="inbound-transport-layers-------"></a>**入站\_传输层**   
标注驱动程序必须执行异步处理需要 ALE 分类处理传入的数据包 （入站） 传输层 (**FWPS\_层\_入站\_传输\_V4**或**FWPS\_层\_入站\_传输\_V6**)。 执行此操作可能会影响创建流。 当调用 WFP *classifyFn*标注函数在传入的传输层，它会设置**FWPS\_元数据\_字段\_ALE\_分类\_所需**标记为需要 ALE 这些数据包对处理进行分类。 标注驱动程序应允许此类数据包从入站\_传输层和应延迟处理直到其达到 ALE\_收到\_接受层。

<a href="" id="stream-layers-------"></a>**流层**   
在流层 (**FWPS\_层\_流\_V4**或**FWPS\_层\_流\_V6**)，TCP 数据段表示而不是一个 IP 或 TCP 标头。 流层也是其中的网络缓冲区列表链可以指示调用一次*classifyFn*标注函数。 WFP 使可用的专用的克隆和注入函数[ **FwpsCloneStreamData0** ](https://msdn.microsoft.com/library/windows/hardware/ff551149)并[ **FwpsStreamInjectAsync0**](https://msdn.microsoft.com/library/windows/hardware/ff551213)，为流式传输层标注使用。

由于流层数据的按序的送达的性质，标注驱动程序必须继续进行克隆并应对数据所导致的任何长时间的流数据仍是挂起。 混合使用给定的流流的异步和同步操作可能会导致未定义的行为。

 

 





