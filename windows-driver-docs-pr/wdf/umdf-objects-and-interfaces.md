---
title: UMDF 对象和接口
description: UMDF 对象和接口
ms.assetid: da816fef-a24f-4456-9d4a-36f291afe8b5
keywords:
- 用户模式驱动程序框架 WDK，对象
- 用户模式驱动程序 WDK UMDF，对象
- 对象 WDK UMDF
- UMDF 对象 WDK
- 接口 WDK UMDF
- 框架对象 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e90fe18f018bf8c55359c38ef47e7c3c55f58ede
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191383"
---
# <a name="umdf-objects-and-interfaces"></a>UMDF 对象和接口


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

用户模式驱动程序框架 (UMDF) 由一组协同对象构成。 UMDF 创建并管理一系列向用户模式设备驱动程序公开的对象。 其中一些对象是由 UMDF 为响应应用程序触发的操作而创建的，例如 i/o 请求，而当驱动程序调用 UMDF 接口方法时，则会创建其他 UMDF 对象。 例如，若要创建 i/o 队列对象，驱动程序将调用 [**IWDFDevice：： CreateIoQueue**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createioqueue) 方法。

以下主题描述核心框架对象、组件对象模型的子集 (它们所基于的 COM) ，以及 UMDF DDI 编程模型：

-   [框架对象](framework-objects.md)
-   [框架对象层次结构](framework-object-hierarchy.md)
-   [基于 COM 子集的 UMDF](umdf-based-on-com-subset.md)
-   [UMDF DDI 编程模型](umdf-ddi-programming-model.md)
-   [管理对象的生存期](managing-the-lifetime-of-objects.md)

 

