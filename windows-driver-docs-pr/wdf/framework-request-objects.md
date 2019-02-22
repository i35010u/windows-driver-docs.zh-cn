---
title: Framework 请求对象
description: Framework 请求对象
ms.assetid: 564f3600-4784-4a37-ac13-38338c38a9d2
keywords:
- I/O 请求 WDK KMDF，请求对象
- 请求对象 WDK KMDF
- 请求处理 WDK KMDF，请求对象
- framework 对象 WDK KMDF，I/O 请求对象
- 请求对象 WDK KMDF 关于请求对象
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 80436e8fb83717536cadfbe3c8fe822d40eb5731
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533545"
---
# <a name="framework-request-objects"></a>Framework 请求对象





Framework 请求对象表示 I/O 管理器已发送到驱动程序的 I/O 请求。 基于框架的驱动程序处理每个 I/O 请求通过调用[framework 请求对象方法](https://msdn.microsoft.com/library/windows/hardware/dn265664)。

每个 I/O 请求包含 WDM *I/O 请求数据包*([**IRP** ](https://msdn.microsoft.com/library/windows/hardware/ff550694)结构)，但基于框架的驱动程序通常无需访问 IRP 结构。

## <a name="in-this-section"></a>本部分内容


-   [创建框架请求对象](creating-framework-request-objects.md)
-   [使用请求对象上下文](using-request-object-context.md)
-   [请求所有权](request-ownership.md)
-   [处理 I/O 请求](processing-i-o-requests.md)
-   [获取有关的 I/O 请求的信息](obtaining-information-about-an-i-o-request.md)
-   [WDF 驱动程序 （KMDF 或 UMDF） 中访问数据缓冲区](accessing-data-buffers-in-wdf-drivers.md)
-   [管理缓冲区在 UMDF 驱动程序的访问方法](managing-buffer-access-methods-in-umdf-drivers.md)
-   [重复使用 Framework 的请求对象](reusing-framework-request-objects.md)

 

 





