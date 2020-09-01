---
title: 设计移动宽带应用中的购买流
description: 设计移动宽带应用中的购买流
ms.assetid: 1243b255-aac6-4d75-826a-e42482f5ac1b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16993d87f4f663d1a1d71c61a515d9ce9fcd502d
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215337"
---
# <a name="design-purchase-flows-in-a-mobile-broadband-app"></a>设计移动宽带应用中的购买流


你的移动宽带应用可以包含供用户用来购买计划的购买流程。 第一次购买时，支持通过 web 的购买流程。 下面是有关采购流的一些标准建议。

**注意**   不要使用 iframe 来托管应用中的这些流。

 

1.  向用户显示计划的详细信息，并允许他们选择计划，然后将其转发到完整的购买流程。

    ![计划详细信息](images/mb-fig1-purchaseflow-plandetails.png)

2.  您可以选择为用户提供数据细分，以估计他们将需要的数据。 这可以帮助用户选择要购买的最佳计划。

    ![查看计划详细信息](images/mb-fig2-reviewplandetails.png)

3.  如果购买流包含表单，请遵循以下准则：

    -   允许在窗体页中进行垂直滚动。

    -   请确保所有窗体字段都左对齐。

    -   由于应用程序必须与多个窗体规格兼容，因此我们建议您在窗体字段之间提供触摸友好的间距。

    -   留出足够的空白以提高简易性。

    -   遵循窗体支持的最佳实践。 这包括但不限于，提供正确的地址、编号和信用卡字段支持。

    -   请确保为窗体字段定义了输入作用域，以便相应的触摸键盘显示字段，例如，数字、文本等。

    -   请确保窗体已正确对齐所有控件和字段。

    -   最大程度地减少点击数和字段数。

4.  用户输入其信息后，允许他们在完成购买之前查看订单。 如果放置了订单并且激活速度很快，请继续激活，然后将应用重定向到登陆页面。 如果需要更长的激活时间，你可以包含一个用于激活进度的占位符页面，并使用进度控制来显示正在进行的激活。 有关进度控件的详细信息，请参阅 [快速入门：添加进度控件](/previous-versions/windows/apps/hh465487(v=win.10))。

## <a name="span-idquick_summaryspanspan-idquick_summaryspanspan-idquick_summaryspanquick-summary"></a><span id="Quick_summary"></span><span id="quick_summary"></span><span id="QUICK_SUMMARY"></span>快速摘要


适用于购买页面的设计：

-   遵循窗体准则，其中包括左对齐、空格、适当的网格对齐方式和触控友好性。

-   使用简单的布局来提高可读性。

-   为长窗体使用垂直滚动，使选项卡和屏幕键盘更易于使用。

-   让用户在开始购买流程之前查看和选择计划。

-   支持通过 web 和首次购买来购买。

采购、重充电、重填和计费页面的设计不适当：

-   不要对长格式使用水平滚动。

-   不要填满所有空格。

-   不要使用 iframe 来托管流。

-   不要让用户等待很长时间，而不提供视觉反馈。

-   请勿链接到应用外部的网站。

## <a name="span-idadditional_resourcesspanspan-idadditional_resourcesspanspan-idadditional_resourcesspanadditional-resources"></a><span id="Additional_resources"></span><span id="additional_resources"></span><span id="ADDITIONAL_RESOURCES"></span>其他资源


-   有关视图和布局的详细信息，请参阅 [选择布局](/previous-versions/windows/apps/hh465327(v=win.10))。

-   有关 Listview 的详细信息，请参阅 [快速入门：添加 ListView](/previous-versions/windows/apps/hh465496(v=win.10))。

-   有关错误处理的设计指南，请参阅对 [UI 进行布局](/previous-versions/windows/apps/hh465304(v=win.10))。

-   有关辅助功能指南，请参阅 [使用 c + +、c # 或 Visual Basic 的 UWP 应用中的辅助功能](/previous-versions/windows/apps/hh452680(v=win.10))。

-   有关如何使用内置控件的详细信息，请参阅 [添加控件和内容](/previous-versions/windows/apps/hh465393(v=win.10))。

-   有关触控输入准则，请参阅 [快速入门：触控输入](/previous-versions/windows/apps/hh465387(v=win.10))。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[设计移动宽带应用的用户体验](designing-the-user-experience-of-a-mobile-broadband-app.md)

 

