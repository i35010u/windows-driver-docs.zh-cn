---
title: 用于连接到移动宽带网络最佳实践
description: 用于连接到移动宽带网络最佳实践
ms.assetid: 6106d026-1c5f-4990-8ef2-467c1a77a38e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0bed901b901260f9b9fb1927fe1ebac785b150a5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520128"
---
# <a name="best-practices-for-connecting-to-the-mobile-broadband-network"></a>用于连接到移动宽带网络最佳实践


活动连接到移动宽带网络可以是不必要消耗电池寿命和帐户数据配额。 我们建议使用仔细判断来确定连接是否是必需的。

使用移动宽带网络连接有关的以下最佳实践：

-   不使用预配代理&lt;*激活*&gt;指令。 这些指令仅适用于特定情况下在激活后。

-   使用移动宽带 API 建立临时连接。 此 API 提供连接操作结果和断开连接的简单方法。

-   将连接生存期保持最小。

-   只要这些信息可通过 Internet 连接的接口使用的连接。 您可以通过使用观察可用性[ **NetworkInformation** ](https://msdn.microsoft.com/library/windows/apps/br207293) API。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[使用移动宽带 Windows 运行时 API 的最佳实践](best-practices-for-using-mobile-broadband-windows-runtime-api.md)

 

 






