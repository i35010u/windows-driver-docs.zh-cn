---
title: 验证后台事件
description: 验证后台事件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 996d7a9d8b1688e1e8c24af4ae83086d0a6b38e2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815025"
---
# <a name="verify-background-events"></a>验证后台事件


连接到热点网络后，请检查是否启动了后台事件。 否则，请检查以下各项：

-   **Windows 是否检测到热点？** 如果是这样，则网络列表应表示连接受限。 如果 Windows 在连接到网络后检测到与 Internet 的连接，则不会执行任何热点身份验证操作。

-   **Windows 是否在热点上检测到 WISPr？** 如果是这样，将触发后台事件，否则系统将提示用户输入凭据。 如果 Windows 打开浏览器，则未检测到 WISPr。 检查 XML 消息是否存在于浏览器的重定向页面中，以及它是否符合 WISPr 规范。

-   **您的应用程序是否与该配置文件正确关联？** 如果是这样，将触发后台事件。 如果不是，则在手动连接到网络时，系统将提示用户提供凭据。 检查指定为 ExtensionId 的应用程序家族名称是否与您的应用程序相匹配，并且该设置是否已成功。

接下来，请检查是否可以成功地向网络进行身份验证。 特别是，应涵盖以下情况：

-   **身份验证成功** 在理想情况下，你的应用程序可以提供凭据，并将用户连接到网络。

-   **用户交互** 如果需要在某些情况下与用户交互，请确保你的应用程序启动到正确的上下文来执行交互，而不只是应用程序的主页。

-   **身份验证失败** 特别是在使用前缀时，应该处理网络是否与你的前缀相匹配的可能性，但无法为其生成凭据。 在这种情况下，应停止身份验证。

-   **拒绝访问** 在某些情况下，应用程序将接收后台事件，但可能无法检索身份验证尝试的详细信息。 在这种情况下，您的后台事件应该尽快停止。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[热点身份验证应用入门](review-the-hotspot-authentication-sample.md)

 

 






