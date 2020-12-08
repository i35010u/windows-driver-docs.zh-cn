---
title: 帐户管理
description: 帐户管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3466b035c0de7cf1427a18c0cfca40455c40892f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782569"
---
# <a name="account-management"></a>帐户管理


用户购买订阅后，可以执行以下任务：

-   **查看当前数据使用情况** 用户可以查看他们当前的数据使用情况，并了解他们的计费周期 (或会话结束日期) 以便对其数据使用做出适当的决策。

-   **管理帐户设置** 用户可以查看并安全地管理其支付和帐户详细信息 (例如密码、电子邮件地址和) 的自动付款信息。

-   **支付帐单** 用户可以使用 UWP 应用支付定期或一次性帐单。

帐户管理功能显示订阅服务器与操作员之间的关系。 可以使用它来创建可将服务与竞争对手的服务区分开来的品牌体验。

设计注意事项包括：

-   将 **数据使用组合为本地和后端信息** 为了尽可能减少后端服务器上的负载，Windows 提供了本地数据使用 API，你可以使用它来合并后端数据使用。 可以定期从后端获取使用情况信息，并将其与本地数据使用关联起来。

-   **使用数据使用定期更新 Windows** Windows 10 旨在智能地在按流量计费的网络上运行。 这可以节省大量网络容量，因为 Windows 和 UWP 应用可以使用移动宽带网络来实现重要的流量。 若要更准确地了解应用程序的详细信息 (例如，数据限制和使用情况) ，Windows 需要定期提供正确的信息。 应用可以使用数据使用情况 Api 来设置此信息。

    ![帐户概述](images/mb-fig2-accountoverview.png)



