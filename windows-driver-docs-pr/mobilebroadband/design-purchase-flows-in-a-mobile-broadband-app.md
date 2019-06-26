---
title: 设计移动宽带应用中的购买流
description: 设计移动宽带应用中的购买流
ms.assetid: 1243b255-aac6-4d75-826a-e42482f5ac1b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44539ff103b25ae0ace9b1d8800a1efc0f6c1200
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379334"
---
# <a name="design-purchase-flows-in-a-mobile-broadband-app"></a>设计移动宽带应用中的购买流


移动宽带应用可以包含用户用来购买计划购买流。 首次购买，在 web 上的支持你购买的流。 以下是一些标准建议购买流程。

**请注意**  不要使用 iframe 来托管这些应用程序中的流。

 

1.  向用户显示的计划详细信息，并允许他们选择的计划之前将它们转发到完成采购流程。

    ![计划的详细信息](images/mb-fig1-purchaseflow-plandetails.png)

2.  你可以选择提供数据细分的用户来估计将需要的数据。 这可以帮助用户选择要购买的最佳计划。

    ![查看计划的详细信息](images/mb-fig2-reviewplandetails.png)

3.  如果你购买的流包含窗体，请遵循以下准则：

    -   允许窗体页中的垂直滚动。

    -   请确保所有窗体字段都是左对齐。

    -   由于应用程序必须与多个外形规格兼容，我们建议你提供触摸功能的窗体字段之间的间距。

    -   保留足够的空白区域以促进简单起见。

    -   遵循的窗体支持的最佳实践。 这包括但不限于，对于地址、 号和信用卡字段提供适当的支持。

    -   请确保输入的范围已定义的窗体字段，以便相应触摸键盘显示的字段 — 例如，数字、 文本和等等。

    -   请确保窗体具有所有控件和字段正确对齐。

    -   单击和字段的数量降至最低。

4.  用户输入他们的信息后，允许它们以完成购买之前查看的顺序。 如果激活是快速提交订单后，继续进行激活，并且将应用程序重定向到登录页。 如果激活预计需要花费更长，你可以包括激活进度的占位符页和进度控件用于显示发生了激活。 关于进度控件的详细信息，请参阅[快速入门： 将进度控件添加](https://docs.microsoft.com/previous-versions/windows/apps/hh465487(v=win.10))。

## <a name="span-idquicksummaryspanspan-idquicksummaryspanspan-idquicksummaryspanquick-summary"></a><span id="Quick_summary"></span><span id="quick_summary"></span><span id="QUICK_SUMMARY"></span>快速摘要


适合购买页面的设计：

-   遵循这些窗体指南，其中包括左的对齐、 空格、 正确的网格对齐方式和触摸友好性。

-   使用简单布局以提高可读性。

-   使用长窗体的垂直滚动以使其更易于选项卡，并使用屏幕键盘。

-   让的用户查看和选择计划之前启动的采购流程。

-   支持通过 web 和首次购买购买。

购买、 充电、 重填，和计费页面的设计不完善：

-   请勿使用长窗体的水平滚动。

-   不被填满所有空白区域。

-   不要使用 iframe 来托管流。

-   不要让用户等待很长时间，而无需提供可视反馈。

-   未链接到应用外部的网站。

## <a name="span-idadditionalresourcesspanspan-idadditionalresourcesspanspan-idadditionalresourcesspanadditional-resources"></a><span id="Additional_resources"></span><span id="additional_resources"></span><span id="ADDITIONAL_RESOURCES"></span>其他资源


-   有关视图和布局的详细信息： 请参阅[选择一种布局](https://docs.microsoft.com/previous-versions/windows/apps/hh465327(v=win.10))。

-   有关 Listview 的详细信息，请参阅[快速入门：添加 ListView](https://docs.microsoft.com/previous-versions/windows/apps/hh465496(v=win.10))。

-   错误处理的设计指南，请参阅[布置 UI](https://docs.microsoft.com/previous-versions/windows/apps/hh465304(v=win.10))。

-   有关可访问性的指南，请参阅[中使用的 UWP 应用的辅助功能C++， C#，或 Visual Basic](https://docs.microsoft.com/previous-versions/windows/apps/hh452680(v=win.10))。

-   有关如何使用内置控件的详细信息，请参阅[添加控件和内容](https://docs.microsoft.com/previous-versions/windows/apps/hh465393(v=win.10))。

-   触摸输入准则，请参阅[快速入门：触摸输入](https://docs.microsoft.com/previous-versions/windows/apps/hh465387(v=win.10))。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[设计用户体验的移动宽带应用程序](designing-the-user-experience-of-a-mobile-broadband-app.md)

 

 






