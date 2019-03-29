---
title: 设计移动宽带应用中的消息
description: 设计移动宽带应用中的消息
ms.assetid: 314fd479-7dcf-4559-a195-26e4c020446c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3704008076dd6468d5f95adf4194ddca58f1a26e
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350232"
---
# <a name="design-messages-in-a-mobile-broadband-app"></a>设计移动宽带应用中的消息


移动宽带应用程序是向客户介绍重要的帐户信息与通信的简便方法。 应用应具有最终用户可以在其中查看重要帐户消息的主屏幕上的部分或链接。 While 重要运算符消息应显示为磁贴和 toast 通知，它们应还显示应用视图中的 toast 通知和有限的数量的磁贴通知可以显示的文本暂时性的性质。

不应混合以及运营商通知和警报，因为客户可能会遗漏重要运营商通知的消息部分中显示用户与用户聊天短信、 促销和播发。 可以在您的应用程序的布局中显示的促销和播发，并在用户界面的单独部分中显示用户与用户聊天文本消息。

![消息](images/message.png)

下表显示了一些示例运算符消息和警报。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>在任务栏的搜索框中键入</th>
<th>示例消息</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>国际漫游</p></td>
<td><p>欢迎使用英国。 必须为 5 美元 25 MB 的数据，并且则美元每 1 个 1 MB。 SMS 是为每个消息 0.49。了解详细信息，请 www.contoso.com/rates/uk。</p></td>
</tr>
<tr class="even">
<td><p>超额数据使用情况</p></td>
<td><p>已使用你的整个 4 GB 数据计划。 @ 10 美元/GB 超额费用账单。 通过升级计划立即在计划页上节省更多的数据。</p></td>
</tr>
<tr class="odd">
<td><p>数据使用情况状态</p></td>
<td><p>你已使用 65%的 40 GB 的数据计划。 @ 5 美元/GB 的任何超额费用账单。 提示：通过 Wi-fi，数据不受限制。 了解在计划页的详细信息。</p></td>
</tr>
<tr class="even">
<td><p>计划到期</p></td>
<td><p>你的计划已于 2013 年 7 月 1 日到期。 通过转到计划页中续订你的计划。</p></td>
</tr>
<tr class="odd">
<td><p>帐户更新</p></td>
<td><p>好消息 ！ 有效立即，Contoso 正在增加包含 DataPro Tethering 计划中从 2 GB 到 4 GB 的数据量。 将不会更改你的计划的每月费用和由你不需要任何操作。 感谢您成为很好的客户。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idquicksummaryspanspan-idquicksummaryspanspan-idquicksummaryspanquick-summary"></a><span id="Quick_summary"></span><span id="quick_summary"></span><span id="QUICK_SUMMARY"></span>快速摘要


显示运算符的消息适合的设计：

-   包括查看所有接收的消息列表的功能、 查看完整详细信息的一条消息，并删除一条消息。

-   在某一部分的应用程序或自己的应用中的页上的主屏幕中显示重要运算符的消息。

用于显示运算符的消息的设计不完善：

-   不显示用户与用户聊天文本消息和促销和运营商通知和警报以及混合的播发。

## <a name="span-idadditionalresourcesspanspan-idadditionalresourcesspanspan-idadditionalresourcesspanadditional-resources"></a><span id="Additional_resources"></span><span id="additional_resources"></span><span id="ADDITIONAL_RESOURCES"></span>其他资源


-   使用[ **ListView** ](https://msdn.microsoft.com/library/windows/apps/br211837)以显示消息。 有关详细信息，请参阅[添加列表视图、 语义缩放和其他数据控件](https://msdn.microsoft.com/library/windows/apps/hh465409)。

-   应用栏控件用于查看和删除消息。 有关详细信息，请参阅[指导原则的应用程序栏](https://msdn.microsoft.com/library/windows/apps/hh465302)。

-   [与其他 Windows 组件集成，移动宽带应用](integrate-a-mobile-broadband-app-with-other-windows-components.md#tileandtoast)

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[设计用户体验的移动宽带应用程序](designing-the-user-experience-of-a-mobile-broadband-app.md)

 

 






