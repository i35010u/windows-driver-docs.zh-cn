---
title: 帐户管理
description: 帐户管理
ms.assetid: 8201a4ac-1344-4a96-b0d5-d4ba8123c4dd
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cae3fce4b27b55dbfe9ae24baa0017bf3cf97780
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386897"
---
# <a name="account-management"></a>帐户管理


用户已购买了订阅后，它们可以执行以下任务：

-   **查看当前数据使用情况**用户可以查看其当前的数据使用情况并了解其计费周期 （或会话结束日期） 上他们的数据使用做出适当的决策。

-   **管理帐户设置**用户可以查看和安全地管理付款和帐户详细信息 （如密码、 电子邮件地址和自动付款信息）。

-   **支付帐单**用户可以通过使用你的 UWP 应用付款定期或一次性帐单。

帐户管理功能提供订阅者的关系，其中一个运算符。 可以使用此创建品牌化的经验，可以从竞争对手的服务区分你的服务。

设计注意事项包括：

-   **进行本地和后端的信息的组合的数据使用情况**以减少最大程度地在后端服务器上的负载，Windows 提供了一个本地的数据使用情况 API，可用于将组合后端数据使用情况。 你可以定期从后端获取使用情况信息并关联的本地数据使用情况。

-   **定期更新数据使用情况与 Windows**设计为 Windows 10 以智能地按流量计费网络上。 这可以节省大量的网络容量，因为 Windows 和 UWP 应用可以使用移动宽带网络进行必要的流量。 若要更准确并包括应用程序 （例如，数据限制和使用情况） 的详细信息，Windows 依赖于您定期提供正确的信息。 您的应用程序可以使用数据使用情况 Api 来设置此信息。

    ![帐户概述](images/mb-fig2-accountoverview.png)

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[移动宽带应用方案](mobile-broadband-app-scenarios.md)

 

 






