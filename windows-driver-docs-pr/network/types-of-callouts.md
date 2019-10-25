---
title: 标注类型
description: 标注类型
ms.assetid: d9539403-7657-4e95-8791-309673d1207d
keywords:
- 挂起的数据包 WDK Windows 筛选平台
- 标注类型 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca6f4829515cd5852b740c0f0118b7e2f043426a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841772"
---
# <a name="types-of-callouts"></a>标注类型


以下类型的标注可与 WFP 一起使用：

<a href="" id="inline-inspection-callout-------"></a>**内联检查标注**   
这种类型的标注始终返回 **.fwp\_操作\_** 从[*CLASSIFYFN*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_classify_fn0)函数继续执行，并且不会以任何方式修改网络流量。 收集网络统计信息的标注就是这种类型的标注的示例。

对于这种类型的标注，筛选器操作类型（由[**FWPS\_ACTION0**](https://docs.microsoft.com/windows/desktop/api/fwpstypes/ns-fwpstypes-fwps_action0_)结构的**type**成员指定）应设置为 **.fwp\_操作\_标注\_检查**。

<a href="" id="out-of-band-inspection-callout-------"></a>带外**检查标注**   
此类型的标注不会修改网络流量。 相反，它会通过 "挂起" 所指示的数据来推迟在*classifyFn*函数之外完成的所有检查，然后使用其中一个[数据包注入函数](packet-injection-functions.md)将挂起的数据重新 reinjecting 到 tcp/ip 堆栈中。 "挂起" 是通过首先克隆所指示的数据来实现的，然后从具有**FWPS\_\_分类**的*classifyFn*函数中返回 **\_操作的 .FWP\_块**，\_吸收位集。

<a href="" id="inline-modification-callout-------"></a>**内联修改标注**   
这种类型的标注将首先创建所指示的数据的克隆，然后修改克隆，最后将修改后的克隆从*classifyFn*函数注入回 tcp/ip 堆栈，从而修改网络流量。 这种类型的标注还会从*classifyFn*函数返回 **\_块的 .fwp\_操作**，该函数的**FWPS\_将\_OUT\_标志\_吸收**位集。

此类型的标注的筛选器操作类型应设置为 " **\_操作"\_标注\_终止**的 ".fwp"。

<a href="" id="out-of-band-modification-callout-------"></a>带外**修改标注**   
此类型的标注首先通过使用[**FwpsReferenceNetBufferList0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsreferencenetbufferlist0)函数（该函数将*intentToModify*参数设置为**TRUE**）来引用指示的数据包。 然后，标注会返回 **\_操作的\_块的 .fwp** ， **\_将\_OUT\_标志\_吸收**从*classifyFn*函数中进行设置。 当数据包准备好在*classifyFn*外进行修改时，标注将克隆引用的数据包（一旦克隆，就可以对其进行取消引用。） 然后，标注会修改克隆，并将修改后的数据包注入回 TCP/IP 堆栈中。

此类型的标注的筛选器操作类型应设置为 " **\_操作"\_标注\_终止**的 ".fwp"。

<a href="" id="redirection-callout"></a>**重定向标注**  
有关此类型标注的详细信息，请参阅[使用 Bind 或 Connect 重定向](using-bind-or-connect-redirection.md)。

重定向标注的类型有两种：

-   使用绑定重定向标注，标注驱动程序可以修改套接字的本地地址和本地端口。
-   连接重定向标注允许标注驱动程序修改连接的远程地址和远程端口。

此类型的标注的筛选器操作类型应设置为 " **\_操作\_允许**" 的 ".fwp"。

有关 FWPS 的详细信息，请[ **\_** ](https://docs.microsoft.com/windows/desktop/api/fwpstypes/ns-fwpstypes-fwps_classify_out0_)参阅 **\_\_吸收\_\_分类** 此标志在任何 WFP 丢弃层上无效。 使用 FWPS\_分类 **\_块返回 .fwp\_操作** **分类\_OUT\_标志**从*classifyFn*函数设置的吸收标志会导致数据包被悄悄地丢弃，使数据包将不会到达任何 WFP 丢弃层，也不会导致生成审核事件。

尽管可以修改克隆的网络缓冲区列表，例如，通过添加或删除 net buffer 或 MDLs，或者两者都必须在调用[**FwpsFreeCloneNetBufferList0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsfreeclonenetbufferlist0)函数之前撤销此类修改。

为了与执行数据包检查、数据包修改或连接重定向的其他标注共存，在使用 reference/clone-reinject 机制挂起数据包之前，标注必须 "硬"-通过清除**FWPS\_右\_操作\_** 在 classifyFn 函数返回的函数的**权限** [ **\_\_** ](https://docs.microsoft.com/windows/desktop/api/fwpstypes/ns-fwpstypes-fwps_classify_out0_)成员中写入标志写入标志。 如果调用*classifyFn*时设置了**FWPS\_RIGHT\_操作\_写入**标志，这意味着包可能会挂起，以后重新插入文本或修改），标注不得挂起指示，不应更改当前操作类型;它必须等待较高的标注来注入可能修改的克隆。

**\_FWPS\_操作\_写入**标志应在每个标注 pends 分类时设置。 标注驱动程序应 **\_操作\_写入**标志来测试\_FWPS，以检查标注的权限以返回操作。 如果未设置此标志，则标注仍可返回 **.fwp\_操作\_阻止**操作，以否决前一个标注返回的**允许的\_操作\_允许**的操作。 在[使用标注进行深层检查](using-a-callout-for-deep-inspection.md)的示例中，如果未设置标志，则函数将退出。

[**FwpsPendOperation0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpspendoperation0)函数用于挂起源自**FWPM\_层\_ALE\_资源\_分配\_** <em>XXX</em>， **FWPM\_层\_ALE\_AUTH 的数据包\_侦听\_** <em>XXX</em>或**FWPM\_层\_ALE\_authentication\_连接\_** <em>XXX</em> [管理筛选层](https://docs.microsoft.com/windows-hardware/drivers/network/management-filtering-layer-identifiers)。

[**FwpsPendClassify0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpspendclassify0)函数用于从以下[运行时筛选层](https://docs.microsoft.com/windows-hardware/drivers/network/run-time-filtering-layer-identifiers)暂挂包：

FWPS\_层\_ALE\_终结点\_关闭\_V4 FWPS\_层\_ALE\_终结点\_关闭\_V6 FWPS\_层\_ALE\_连接\_重定向\_V4 FWPS\_层\_ALE\_连接\_重定向\_V6 FWPS\_层\_ALE\_绑定\_\_V4 FWPS\_层\_ALE\_BIND\_重定向\_V6
 

 





