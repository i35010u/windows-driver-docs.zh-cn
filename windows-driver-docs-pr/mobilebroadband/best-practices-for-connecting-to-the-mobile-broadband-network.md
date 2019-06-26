---
title: 连接到移动宽带网络的最佳做法
description: 连接到移动宽带网络的最佳做法
ms.assetid: 6106d026-1c5f-4990-8ef2-467c1a77a38e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cfe730a408b7dc61089d1aff6c0305330189d882
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364999"
---
# <a name="best-practices-for-connecting-to-the-mobile-broadband-network"></a>连接到移动宽带网络的最佳做法


活动连接到移动宽带网络可以是不必要消耗电池寿命和帐户数据配额。 我们建议使用仔细判断来确定连接是否是必需的。

使用移动宽带网络连接有关的以下最佳实践：

-   不使用预配代理&lt;*激活*&gt;指令。 这些指令仅适用于特定情况下在激活后。

-   使用移动宽带 API 建立临时连接。 此 API 提供连接操作结果和断开连接的简单方法。

-   将连接生存期保持最小。

-   只要这些信息可通过 Internet 连接的接口使用的连接。 您可以通过使用观察可用性[ **NetworkInformation** ](https://docs.microsoft.com/uwp/api/Windows.Networking.Connectivity.NetworkInformation) API。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[使用移动宽带 Windows 运行时 API 的最佳实践](best-practices-for-using-mobile-broadband-windows-runtime-api.md)

 

 






