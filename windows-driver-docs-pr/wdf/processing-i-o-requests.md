---
title: 处理 I/O 请求
description: 处理 I/O 请求
ms.assetid: 90b1cc51-da40-45c1-9d6c-57f637f474d9
keywords:
- I/O 请求 WDK KMDF，处理
- 请求对象 WDK KMDF，处理 I/O 请求
- 请求处理 WDK KMDF，选项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 95ecce43f97950304d03485a2813a4e9004af98c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534252"
---
# <a name="processing-io-requests"></a>处理 I/O 请求





当驱动程序[接收](receiving-i-o-requests.md)I/O 请求时，它可以：

-   [将重新排队](requeuing-i-o-requests.md)不同队列的请求。

-   [完整](completing-i-o-requests.md)请求。

-   [取消](canceling-i-o-requests.md)请求。

-   [前滚](forwarding-i-o-requests.md)对 I/O 目标的请求。

该驱动程序无法忽略或删除请求。

 

 





