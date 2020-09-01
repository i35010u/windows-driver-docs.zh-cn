---
title: 设计移动宽带应用中的消息
description: 设计移动宽带应用中的消息
ms.assetid: 314fd479-7dcf-4559-a195-26e4c020446c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b31aa184bc96472fbfa485307501ece53de2b8ec
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215333"
---
# <a name="design-messages-in-a-mobile-broadband-app"></a>设计移动宽带应用中的消息


你的移动宽带应用程序是与客户沟通重要帐户信息的简便方法。 应用应在主屏幕上有一个 "部分" 或 "链接"，最终用户可以在其中查看重要的帐户消息。 尽管重要的操作员消息应显示为磁贴和 toast 通知，但是，它们还应显示在应用视图中，因为 toast 通知的暂时性性质以及磁贴通知中可显示的文本数量有限。

不应在 "消息" 部分中显示用户到用户的聊天文本消息、促销和广告，并将其与操作员通知和警报混合在一起，因为客户可能会错过重要的操作员通知。 可以在应用布局中显示促销和广告，并将用户到用户聊天文本消息显示在用户界面的单独部分中。

![message](images/message.png)

下表显示了一些示例操作员消息和警报。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>类型</th>
<th>示例消息</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>国际漫游</p></td>
<td><p>欢迎使用英国。 对于每日 $5，你有 25 MB 的数据，然后每 1 MB 就会 $1。 每条消息的短信为 $0.49。有关详细信息，请参阅 www.contoso.com/rates/uk。</p></td>
</tr>
<tr class="even">
<td><p>数据使用量超额</p></td>
<td><p>你已使用了整个 4 GB 数据计划。 超额票据 @ $ 10/GB。 立即在 "计划" 页中升级计划，以节省更多数据。</p></td>
</tr>
<tr class="odd">
<td><p>数据使用状态</p></td>
<td><p>你使用了65% 的 40 GB 数据计划。 任何超额帐单 @ $ 5/GB。 提示：通过 Wi-fi 无限制数据。 在 "计划" 页中了解详细信息。</p></td>
</tr>
<tr class="even">
<td><p>计划到期</p></td>
<td><p>计划在2013年7月1日过期。 转到 "计划" 页，续订你的计划。</p></td>
</tr>
<tr class="odd">
<td><p>帐户更新</p></td>
<td><p>好消息！ Contoso 立即有效地将 DataPro Tethering 计划中包含的数据量从 2 GB 增加到 4 GB。 计划的每月费用将不会更改，因此不需要执行任何操作。 感谢您成为一个优秀的客户。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idquick_summaryspanspan-idquick_summaryspanspan-idquick_summaryspanquick-summary"></a><span id="Quick_summary"></span><span id="quick_summary"></span><span id="QUICK_SUMMARY"></span>快速摘要


显示操作员消息的适当设计：

-   包含查看接收到的所有消息的列表、查看邮件的完整详细信息和删除消息的功能。

-   将重要的操作员消息显示在应用程序主屏幕的一部分中，或显示在应用程序中其自身的页面上。

显示操作员消息的不当设计：

-   不要向用户与用户聊天文本消息和促销和广告显示混合了操作员通知和警报。

## <a name="span-idadditional_resourcesspanspan-idadditional_resourcesspanspan-idadditional_resourcesspanadditional-resources"></a><span id="Additional_resources"></span><span id="additional_resources"></span><span id="ADDITIONAL_RESOURCES"></span>其他资源


-   使用 [**ListView**](/previous-versions/windows/apps/br211837(v=win.10)) 显示消息。 有关详细信息，请参阅 [添加列表视图、语义缩放和其他数据控件](/previous-versions/windows/apps/hh465409(v=win.10))。

-   使用应用程序栏控件查看和删除消息。 有关详细信息，请参阅 [应用栏的准则](/windows/uwp/controls-and-patterns/app-bars)。

-   [将移动宽带应用与其他 Windows 组件集成](integrate-a-mobile-broadband-app-with-other-windows-components.md#tileandtoast)

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[设计移动宽带应用的用户体验](designing-the-user-experience-of-a-mobile-broadband-app.md)

 

