---
title: 标注类型
description: 标注类型
ms.assetid: d9539403-7657-4e95-8791-309673d1207d
keywords:
- 挂起的数据包 WDK Windows 筛选平台
- 标注类型 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4151b612517ac9aa6f3b2b88f6849689633bb1f6
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716882"
---
# <a name="types-of-callouts"></a>标注类型


以下类型的标注可与 WFP 一起使用：

<a href="" id="inline-inspection-callout-------"></a>**内联检查标注**   
此类型的标注始终从[*classifyFn*](/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_classify_fn0)函数返回 **.fwp \_ 操作 \_ ** ，并且不会以任何方式修改网络流量。 收集网络统计信息的标注就是这种类型的标注的示例。

对于这种类型的标注， [** (的 \_ 筛选**](/windows/win32/api/fwpstypes/ns-fwpstypes-fwps_action0_)器操作类型) 应设置为 " **.fwp \_ 操作 \_ 标注 \_ 检查** **"** 。

<a href="" id="out-of-band-inspection-callout-------"></a>**带外检查标注**   
此类型的标注不会修改网络流量。 相反，它会通过 "挂起" 所指示的数据来推迟在 *classifyFn* 函数之外完成的所有检查，然后使用其中一个 [数据包注入函数](packet-injection-functions.md)将挂起的数据重新 reinjecting 到 tcp/ip 堆栈中。 "挂起" 是通过首先克隆所指示的数据来实现的，然后从*classifyFn*函数返回包含 FWPS 的 "已**分类" 标记 " \_ \_ \_ \_ 吸收**位集" 的 **.fwp \_ 操作 \_ 块**。

<a href="" id="inline-modification-callout-------"></a>**内嵌修改标注**   
这种类型的标注将首先创建所指示的数据的克隆，然后修改克隆，最后将修改后的克隆从 *classifyFn* 函数注入回 tcp/ip 堆栈，从而修改网络流量。 此类型的标注还会从*classifyFn*函数返回包含 FWPS 的已** \_ 分类 \_ \_ \_ 标志**的 **.fwp \_ 操作 \_ 块**。

此类型的标注的筛选器操作类型应设置为 "正在终止" 的 " **.Fwp \_ 操作 \_ 标注 \_ **"。

<a href="" id="out-of-band-modification-callout-------"></a>**带外修改标注**   
此类型的标注首先通过使用 [**FwpsReferenceNetBufferList0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsreferencenetbufferlist0) 函数（该函数将 *intentToModify* 参数设置为 **TRUE**）来引用指示的数据包。 然后，该标注返回带 FWPS 的已扩展** \_ 操作 \_ 块**，并通过*classifyFn*函数** \_ \_ \_ \_ 吸收**位集。 当数据包准备好在 *classifyFn*外进行修改时，该标注将在克隆后克隆所引用的数据包 (，然后可以) 取消引用原始数据包。 然后，标注会修改克隆，并将修改后的数据包注入回 TCP/IP 堆栈中。

此类型的标注的筛选器操作类型应设置为 "正在终止" 的 " **.Fwp \_ 操作 \_ 标注 \_ **"。

<a href="" id="redirection-callout"></a>**重定向标注**  
有关此类型标注的详细信息，请参阅 [使用 Bind 或 Connect 重定向](using-bind-or-connect-redirection.md)。

重定向标注的类型有两种：

-   使用绑定重定向标注，标注驱动程序可以修改套接字的本地地址和本地端口。
-   连接重定向标注允许标注驱动程序修改连接的远程地址和远程端口。

此类型的标注的筛选器操作类型应设置为 " **.Fwp \_ 操作 \_ 允许**"。

有关 FWPS 的详细 **信息 \_ ， \_ \_ \_ **请参阅 [**FWPS \_ 分类 \_ OUT0**](/windows/win32/api/fwpstypes/ns-fwpstypes-fwps_classify_out0_)。 此标志在任何 WFP 丢弃层上无效。 通过*classifyFn*函数中的**FWPS " \_ 分类 \_ \_ 标志" \_ 吸收**标志来返回带区的 **.fwp \_ 操作 \_ 块**会使数据包无提示地被丢弃，这样，数据包将不会到达任何 WFP 丢弃层，也不会导致生成审核事件。

尽管可以修改克隆的网络缓冲区列表，例如，通过添加或删除 net buffer 或 MDLs，或者两者都必须在调用 [**FwpsFreeCloneNetBufferList0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsfreeclonenetbufferlist0) 函数之前撤销此类修改。

为了与执行数据包检查、数据包修改或连接重定向的其他标注共存，在使用 reference/clone-reinject 机制挂起数据包之前，标注必须 "硬"-通过在*classifyFn*函数返回的[**FWPS \_ 分类 \_ OUT0**](/windows/win32/api/fwpstypes/ns-fwpstypes-fwps_classify_out0_)结构的**权限**成员中清除**FWPS \_ 右 \_ 操作 \_ 写入**标志来删除原始数据包。 如果在调用*classifyFn*时设置了**FWPS \_ 右 \_ 操作 \_ 写入**标志 (这意味着包可以挂起并在以后重新插入文本或修改) ，则标注不得挂起指示，不应更改当前操作类型; 并且它必须等待较高的标注来注入可能修改的克隆。

只要标注 pends 分类，就应设置 **FWPS \_ 权限 \_ 操作 \_ 写入** 标志。 标注驱动程序应测试 **FWPS \_ 权限 \_ 操作 \_ 写入** 标志，以检查标注的权限以返回操作。 如果未设置此标志，则标注仍可返回 **.Fwp \_ 操作 \_ 阻止** 操作，以便否决先前标注返回的 **允许的 .fwp \_ 操作 \_ 允许** 操作。 在 [使用标注进行深层检查](using-a-callout-for-deep-inspection.md)的示例中，如果未设置标志，则函数将退出。

[**FwpsPendOperation0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpspendoperation0)函数用于挂起来自**FWPM \_ 层 \_ ale \_ 资源 \_ \_ 分配**<em>xxx</em>、 **FWPM \_ 层 \_ ale \_ 身份验证 \_ 侦听 \_ **<em>xxx</em>或**FWPM \_ 层 ale authentication authentication \_ \_ \_ CONNECT \_ **<em>xxx</em> [管理筛选层](./management-filtering-layer-identifiers.md)的数据包。

[**FwpsPendClassify0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpspendclassify0)函数用于从以下[运行时筛选层](./run-time-filtering-layer-identifiers.md)暂挂包：

FWPS \_ 层 \_ ale \_ 终结点 \_ 关闭 \_ V4 FWPS \_ 层 \_ ale \_ 终结点 \_ 关闭 \_ V6 FWPS \_ 层 \_ ALE \_ 连接 \_ 重定向 \_ V4 FWPS \_ 层 \_ ale \_ connect \_ 重定向 \_ V6 FWPS \_ 层 \_ ale \_ 绑定 \_ 重定向 \_ V4 FWPS \_ \_ \_ \_ \_
 

