---
title: 连接到移动宽带网络的最佳做法
description: 连接到移动宽带网络的最佳做法
ms.assetid: 6106d026-1c5f-4990-8ef2-467c1a77a38e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: edb0ad2eb8ab0139197dc3deb84ffdcc3d7ddf61
ms.sourcegitcommit: 7e4d9508198a30bdc1cb6eda83852dda4e42213e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89304304"
---
# <a name="best-practices-for-connecting-to-the-mobile-broadband-network"></a>连接到移动宽带网络的最佳做法


与移动宽带网络建立活动连接可能不必要地消耗电池寿命和帐户数据配额。 建议使用仔细判断来确定是否需要连接。

请使用以下有关连接到移动宽带网络的最佳实践：

-   不要使用预配代理的 &lt; *激活* &gt; 指令。 这些指令仅用于激活后的特定情况。

-   使用移动宽带 API 建立临时连接。 此 API 提供连接操作结果和一种简单的断开连接方式。

-   保持最小连接生存期。

-   使用连接到 Internet 的接口时，可以使用连接。 可以通过使用 [**System.net.networkinformation**](/uwp/api/Windows.Networking.Connectivity.NetworkInformation) API 来观察可用性。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[使用移动宽带 Windows 运行时 API 的最佳做法](best-practices-for-handling-account-arrival-and-removal-events.md)

 

