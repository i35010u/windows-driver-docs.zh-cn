---
title: IViewHelper Clone-View COM 对象的要求
description: IViewHelper Clone-View COM 对象的要求
ms.assetid: ef599874-64c5-480e-a7bc-666ababd4d08
keywords:
- TMM WDK 显示，IViewHelper 要求
- 监视配置 WDK 显示，IViewHelper 要求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 33ace32fcf71b47d94f8cc7f2772c3833078f79e
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066374"
---
# <a name="requirements-of-an-iviewhelper-clone-view-com-object"></a>IViewHelper Clone-View COM 对象的要求


硬件供应商的 [IViewHelper](/windows-hardware/drivers/ddi/index) COM interface 对象必须满足以下要求：

-   COM 对象必须驻留在动态链接库 (DLL) ，后者是 COM 进程内 (进程内) 服务器。

-   COM 对象的实现必须对操作系统不透明。

-   [IViewHelper](/windows-hardware/drivers/ddi/index)接口必须提供方法来获取和设置拓扑数据，其中包括克隆视图。

-   硬件供应商必须找到克隆视图的显示模式，以便显示显示在两个或多个监视器上。

-   如果对 COM 对象的 [**IViewHelper：： commit**](/previous-versions/windows/hardware/drivers/ff568167(v=vs.85)) 方法的调用不会生成模式更改，则 **Commit** 必须调用 Win32 **BroadcastSystemMessage** 函数，并且必须始终使用 BSF \_ POSTMESSAGE 广播选项) WM DISPLAYCHANGE 消息来 post (\_ 。 有关 **BroadcastSystemMessage**的详细信息，请参阅 Microsoft Windows SDK 文档。

-   不能使用 [**IViewHelper：： Commit**](/previous-versions/windows/hardware/drivers/ff568167(v=vs.85)) 方法代替对 Win32 **ChangeDisplaySettingsEx** 的调用 (**null**、 **null**、 **null**、0、 **null**) 函数与指示的参数。 有关 **ChangeDisplaySettingsEx**的详细信息，请参阅 Windows SDK 文档。

 

