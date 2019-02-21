---
title: 设计移动宽带应用中的计费页面
description: 设计移动宽带应用中的计费页面
ms.assetid: 44c5a273-1dd4-4ff5-90aa-9d1f4f855439
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2abd40354ef9dd74f550d750593324007ca59070
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543782"
---
# <a name="design-billing-pages-in-a-mobile-broadband-app"></a>设计移动宽带应用中的计费页面


用户应提供的功能，可以查看帐单摘要，帐单历史记录、 付款，或重新充电计划。

![帐单视图页](images/mb-fig1-viewbillpage.png)

**付款**窗体应遵守窗体中所述的准则[移动宽带应用中的设计购买流](design-purchase-flows-in-a-mobile-broadband-app.md)。 此页可以从链接到**计费**页面后, 付费计划，并通过**现在重新充电**预付计划的登录页面上的按钮。

![使付款窗体](images/mb-fig2-makepaymentform.png)

## <a name="span-idquicksummaryspanspan-idquicksummaryspanspan-idquicksummaryspanquick-summary"></a><span id="Quick_summary"></span><span id="quick_summary"></span><span id="QUICK_SUMMARY"></span>快速摘要


适合的计费页面的设计：

-   请遵循窗体的指导原则，包括左的对齐、 空格、 正确的网格对齐方式和触摸友好性。

-   使用简单布局以提高可读性。

-   使用垂直滚动的长长的表格，因为这将以选项卡并使用联机键盘更容易。

-   这会让付款处理简单的体验。

计费页面的设计不完善：

-   请勿尝试填满的空白区域。

-   不要使用 iframe 来托管流。 相反，构建流直接到应用程序体验。

-   不要让用户等候长时间而无需提供可视反馈。

-   不链接到应用外部的外部站点。

## <a name="span-idadditionalresourcesspanspan-idadditionalresourcesspanspan-idadditionalresourcesspanadditional-resources"></a><span id="Additional_resources"></span><span id="additional_resources"></span><span id="ADDITIONAL_RESOURCES"></span>其他资源


-   有关视图和布局的详细信息： 请参阅[选择一种布局](https://msdn.microsoft.com/library/windows/apps/hh465327)。

-   有关 Listview 的详细信息，请参阅[快速入门：添加 ListView](https://msdn.microsoft.com/library/windows/apps/hh465496)。

-   错误处理的设计指南，请参阅[布置 UI](https://msdn.microsoft.com/library/windows/apps/hh465304)。

-   有关可访问性的指南，请参阅[中使用 c + +，UWP 应用的辅助功能C#，或 Visual Basic](https://msdn.microsoft.com/library/windows/apps/hh452680)。

-   有关如何使用内置控件的详细信息，请参阅[添加控件和内容](https://msdn.microsoft.com/library/windows/apps/hh465393)。

-   触摸输入准则，请参阅[快速入门：触摸输入](https://msdn.microsoft.com/library/windows/apps/xaml/hh465387)。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[设计用户体验的移动宽带应用程序](designing-the-user-experience-of-a-mobile-broadband-app.md)

 

 






