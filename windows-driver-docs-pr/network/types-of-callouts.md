---
title: 标注类型
description: 标注类型
ms.assetid: d9539403-7657-4e95-8791-309673d1207d
keywords:
- 挂起数据包 WDK Windows 筛选平台
- 标注类型 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 56d309451f2c6d4e3a4b37ef195080cd392db58e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368437"
---
# <a name="types-of-callouts"></a>标注类型


可使用 WFP 标注的以下类型：

<a href="" id="inline-inspection-callout-------"></a>**内联检查标注**   
此标注类型始终返回**FWP\_操作\_继续**从[ *classifyFn* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nc-fwpsk-fwps_callout_classify_fn0)函数并不会修改网络流量以任何方式。 收集网络统计信息的标注示范了这种类型的标注。

对于此类型的标注，筛选器操作类型 (由指定**类型**的成员[ **FWPS\_ACTION0** ](https://docs.microsoft.com/windows/desktop/api/fwpstypes/ns-fwpstypes-fwps_action0_)结构) 应设置为**FWP\_操作\_标注\_检查**。

<a href="" id="out-of-band-inspection-callout-------"></a>**带外检查标注**   
此标注类型不会修改网络流量。 相反，它将推迟之外执行任何检查*classifyFn*的"挂起"的函数所指示的数据，然后 reinjecting 挂起数据恢复到 TCP/IP 堆栈之一[数据包注入函数](packet-injection-functions.md). 实现挂起的第一个克隆所指示的数据，返回后跟**FWP\_操作\_阻止**从*classifyFn*具有函数**FWPS\_分类\_出\_标志\_消除**位集。

<a href="" id="inline-modification-callout-------"></a>**内联修改标注**   
此标注类型修改网络流量通过第一个进行克隆的所指示的数据，然后修改克隆，并最后将修改后的克隆注入返回到 TCP/IP 堆栈从*classifyFn*函数。 此标注类型也会返回**FWP\_操作\_阻止**从*classifyFn*具有函数**FWPS\_分类\_OUT\_标志\_消除**位集。

此标注类型的筛选器操作类型应设置为**FWP\_操作\_标注\_正在终止**。

<a href="" id="out-of-band-modification-callout-------"></a>**带外修改标注**   
此标注类型首次使用来引用所指示的数据包[ **FwpsReferenceNetBufferList0** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsreferencenetbufferlist0)具有函数*intentToModify*参数设置为**TRUE**。 然后返回标注**FWP\_操作\_阻止**与**FWPS\_分类\_出\_标志\_消除**位设置从*classifyFn*函数。 当该数据包已准备好外修改*classifyFn*，标注克隆引用的数据包 （只要克隆，原始数据包可以然后取消引用）。 标注然后修改克隆，并返回将修改后的数据包注入的 TCP/IP 堆栈。

此标注类型的筛选器操作类型应设置为**FWP\_操作\_标注\_正在终止**。

<a href="" id="redirection-callout"></a>**重定向标注**  
有关此类型的标注的详细信息，请参阅[使用绑定或连接重定向](using-bind-or-connect-redirection.md)。

有两种类型的重定向的标注：

-   绑定重定向标注允许要修改的本地地址和本地端口的套接字的标注驱动程序。
-   连接重定向标注允许标注驱动程序来修改远程地址和连接的远程端口。

此标注类型的筛选器操作类型应设置为**FWP\_操作\_允许**。

有关详细信息**FWPS\_分类\_OUT\_标志\_消除**，请参阅[ **FWPS\_分类\_OUT0**](https://docs.microsoft.com/windows/desktop/api/fwpstypes/ns-fwpstypes-fwps_classify_out0_). 此标志无效，不能在任何 WFP 放弃层。 返回**FWP\_操作\_阻止**与**FWPS\_分类\_出\_标志\_消除**从设置标志*classifyFn*函数会导致数据包以无提示方式被放弃，数据包将不命中任何 WFP 的方式放弃层，也不能将它会导致审核事件生成。

尽管可以修改克隆 net 缓冲区列表，例如，通过添加或删除网络缓冲区 MDLs，和 / 或标注必须撤消此类修改它们调用之前[ **FwpsFreeCloneNetBufferList0** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsfreeclonenetbufferlist0)函数。

若要与之前的数据包是写入到的引用/克隆-删除-重新接入机制执行数据包检查、 数据包修改或重定向连接，其他标注共存，标注"很难"必须-删除原始数据包通过清除**FWPS\_右\_操作\_编写**标记中**rights**隶属[ **FWPS\_分类\_OUT0**](https://docs.microsoft.com/windows/desktop/api/fwpstypes/ns-fwpstypes-fwps_classify_out0_)返回的结构*classifyFn*函数。 如果**FWPS\_右\_操作\_编写**时设置标志*classifyFn*称为 （这意味着数据包可能被挂起，而稍后重新插入或修改)，标注必须不挂起指示并不应更改当前的操作类型;它必须等待一个更高版本权重标注注入可能会被修改的克隆。

**FWPS\_右\_操作\_编写**每当标注等待分类时，应设置标志。 标注驱动程序应进行测试以**FWPS\_右\_操作\_编写**标志，用于检查在标注返回操作的权限。 如果未设置此标志，在标注仍会返回**FWP\_操作\_阻止**为了能否决操作**FWP\_操作\_允许**操作，返回上一个标注。 在示例中所示[深度检测用于标注](using-a-callout-for-deep-inspection.md)，如果未设置该标志只需退出函数。

[ **FwpsPendOperation0** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpspendoperation0)函数将用来为源自的挂起数据包**FWPM\_层\_ALE\_资源\_分配\_** <em>XXX</em>， **FWPM\_层\_ALE\_AUTH\_侦听\_** <em>XXX</em>，或**FWPM\_层\_ALE\_身份验证\_CONNECT\_** <em>XXX</em>[筛选层管理](https://docs.microsoft.com/windows-hardware/drivers/network/management-filtering-layer-identifiers)。

[ **FwpsPendClassify0** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpspendclassify0)函数将用来为源自以下挂起数据包[运行时筛选层](https://docs.microsoft.com/windows-hardware/drivers/network/run-time-filtering-layer-identifiers):

FWPS\_层\_ALE\_终结点\_闭包\_V4 FWPS\_层\_ALE\_终结点\_闭包\_V6 FWPS\_层\_ALE\_CONNECT\_重定向\_V4 FWPS\_层\_ALE\_CONNECT\_重定向\_V6 FWPS\_层\_ALE\_绑定\_重定向\_V4 FWPS\_层\_ALE\_绑定\_重定向\_V6
 

 





