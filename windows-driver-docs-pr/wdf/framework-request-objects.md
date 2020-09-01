---
title: 框架请求对象
description: 框架请求对象
ms.assetid: 564f3600-4784-4a37-ac13-38338c38a9d2
keywords:
- I/o 请求 WDK KMDF，请求对象
- 请求对象 WDK KMDF
- 请求处理 WDK KMDF，请求对象
- framework 对象 WDK KMDF、i/o 请求对象
- 请求对象 WDK KMDF，关于请求对象
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c60b09f56ece71a8a8a88c0ef132d1eb8052c468
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184617"
---
# <a name="framework-request-objects"></a>框架请求对象





Framework 请求对象表示 i/o 管理器发送到驱动程序的 i/o 请求。 基于框架的驱动程序通过调用 [框架请求对象方法](/windows-hardware/drivers/ddi/wdfrequest/)来处理每个 i/o 请求。

每个 i/o 请求都包含一个 WDM *i/o 请求数据包* ([**IRP**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp) 结构) ，但基于框架的驱动程序通常不需要访问 IRP 结构。

## <a name="in-this-section"></a>本节内容


-   [创建框架请求对象](creating-framework-request-objects.md)
-   [使用请求对象上下文](using-request-object-context.md)
-   [请求所有权](request-ownership.md)
-   [处理 I/O 请求](processing-i-o-requests.md)
-   [获取有关 I/O 请求的信息](obtaining-information-about-an-i-o-request.md)
-   [在 WDF 驱动程序（KMDF 或 UMDF）中访问数据缓冲区](accessing-data-buffers-in-wdf-drivers.md)
-   [管理 UMDF 驱动程序中的缓冲区访问方法](managing-buffer-access-methods-in-umdf-drivers.md)
-   [重复使用框架请求对象](reusing-framework-request-objects.md)

 

