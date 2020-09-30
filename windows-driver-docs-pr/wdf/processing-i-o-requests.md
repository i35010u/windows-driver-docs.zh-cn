---
title: 处理 I/O 请求
description: 了解处理 i/o 请求。 例如，当驱动程序收到 i/o 请求时，它可以重新排队、完成或取消请求。
ms.assetid: 90b1cc51-da40-45c1-9d6c-57f637f474d9
keywords:
- I/o 请求 WDK KMDF，处理
- 请求对象 WDK KMDF，处理 i/o 请求
- 请求处理 WDK KMDF，选项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5db04d2ce265d39e86a54dec4e2df3b55f408b6
ms.sourcegitcommit: f1d6c2d0cdbecdc69ba65ed3b530755fc73c8e5e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/30/2020
ms.locfileid: "91590401"
---
# <a name="processing-io-requests"></a>处理 I/O 请求





当驱动程序 [收到](receiving-i-o-requests.md) i/o 请求时，它可以：

-   将请求[重新排队](requeuing-i-o-requests.md)到不同的队列。

-   [完成](completing-i-o-requests.md) 请求。

-   [取消](canceling-i-o-requests.md) 请求。

-   将请求[转发](forwarding-i-o-requests.md)到 i/o 目标。

驱动程序无法忽略或删除请求。

 

 





