---
title: 验证后台事件
description: 验证后台事件
ms.assetid: c840f555-2e09-409d-9d4f-4d9e8bd8d5a5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 032a0a6056235b9a55faceee0137ee00f0d071c5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386249"
---
# <a name="verify-background-events"></a>验证后台事件


连接到热点网络后，检查启动后台事件。 如果没有，请检查以下各项：

-   **Windows 未检测到你热点吗？** 如果是这样，网络列表应指示有限的连接。 如果 Windows 检测到 Internet 连接到连接到网络后，不执行任何热点身份验证操作。

-   **Windows 未检测您热点的 WISPr？** 如果是这样，背景事件将激发，或将提示用户提供凭据。 如果 Windows 改为打开浏览器，WISPr 未检测到。 检查 XML 消息浏览器的重定向页中存在，并且它符合 WISPr 规范。

-   **是你正确配置文件与相关联的应用？** 如果是这样，会触发后台事件。 如果没有，用户将会提示输入凭据时手动连接到网络。 检查指定为扩展 Id 的应用程序系列名称与你的应用程序和预配已成功。

接下来，检查，您可以成功进行身份验证到网络。 具体而言，应包括以下情况：

-   **成功进行身份验证**在理想情况下，您的应用程序可以提供凭据和连接到网络的用户。

-   **用户交互**如果你需要在某些情况下的用户进行交互，请确保您的应用程序将启动到正确的上下文来执行交互，并不只是到你的应用的主页。

-   **不成功的身份验证**尤其是在使用前缀，应处理网络匹配您的前缀，但不能生成其凭据的可能性。 在这种情况下，您应停止身份验证。

-   **访问被拒绝**在某些情况下，你的应用将会收到背景事件，但可能无法检索身份验证尝试的详细信息。 在这种情况下，背景事件应完全停止越早越好。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[热点身份验证应用入门](get-started-with-a-hotspot-authentication-app.md)

 

 






