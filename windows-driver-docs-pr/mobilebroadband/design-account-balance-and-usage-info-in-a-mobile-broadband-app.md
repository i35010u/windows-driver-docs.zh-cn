---
title: 设计移动宽带应用中的帐户余额和使用情况信息
description: 设计移动宽带应用中的帐户余额和使用情况信息
ms.assetid: aec4e4b3-d207-4319-a134-29b4a773c3a6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 20e9e4f99455143d7232b6b7d34415a6ab32d10d
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215365"
---
# <a name="design-account-balance-and-usage-info-in-a-mobile-broadband-app"></a>设计移动宽带应用中的帐户余额和使用情况信息


用户主要使用移动宽带应用来查看帐户余额和使用情况信息。 此数据应清楚地显示在应用的主屏幕上。

![支付后计划摘要](images/mb-fig1-postpaidplansummary.png)

支付后帐户的相关帐户信息包括以下内容：

-   帐户的移动电话号码

-   剩余帐户余额

-   使用的数据、使用的漫游数据和剩余使用量

-   计费周期或计划到期日期

用户可以一目了然地了解他们使用的数据量、剩余的数据量，以及在每月帐户)  (的计费周期。

![预付付计划摘要](images/mb-fig2-prepaidplansummary.png)

预付帐户的相关帐户信息包括：

-   帐户的移动电话号码

-   剩余帐户余额

-   "立即充电" 按钮，其中的链接可生成付款页

-   使用的数据和剩余数据

-   计划到期日期 (（如果存在）) 

## <a name="span-idquick_summaryspanspan-idquick_summaryspanspan-idquick_summaryspanquick-summary"></a><span id="Quick_summary"></span><span id="quick_summary"></span><span id="QUICK_SUMMARY"></span>快速摘要


显示帐户信息的适当设计：

-   显示相关帐户信息

-   显示上次更新数据的时间

-   使用图表和图形等插图来可视化数据

    **提示**   如[添加进度控件](/previous-versions/windows/apps/hh465428(v=win.10))中所述，可以使用确定性进度栏控件实现条形图。

     

-   当剩余使用率较低时，显示指向 "计划" 页的链接以升级计划

用于显示帐户信息的不适当的设计：

-   请勿在数据使用旁显示法律免责声明的长段。 这会将用户从 "帐户使用情况" 部分的主要焦点上分散。 而是显示一个链接，该链接指向应用中具有完全法律免责声明的单独部分。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[设计移动宽带应用的用户体验](designing-the-user-experience-of-a-mobile-broadband-app.md)

 

