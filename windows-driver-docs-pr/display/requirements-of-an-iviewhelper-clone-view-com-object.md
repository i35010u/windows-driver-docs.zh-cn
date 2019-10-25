---
title: IViewHelper Clone-View COM 对象的要求
description: IViewHelper Clone-View COM 对象的要求
ms.assetid: ef599874-64c5-480e-a7bc-666ababd4d08
keywords:
- TMM WDK 显示，IViewHelper 要求
- 监视配置 WDK 显示，IViewHelper 要求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 750bd627aa864e3fdaa646a7bf1e9867942b2a61
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825851"
---
# <a name="requirements-of-an-iviewhelper-clone-view-com-object"></a>IViewHelper Clone-View COM 对象的要求


硬件供应商的[IViewHelper](https://docs.microsoft.com/windows-hardware/drivers/ddi/index) COM interface 对象必须满足以下要求：

-   COM 对象必须驻留在动态链接库（DLL）中，这是一个 COM 进程内（进程内）服务器。

-   COM 对象的实现必须对操作系统不透明。

-   [IViewHelper](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)接口必须提供方法来获取和设置拓扑数据，其中包括克隆视图。

-   硬件供应商必须找到克隆视图的显示模式，以便显示显示在两个或多个监视器上。

-   如果对 COM 对象的[**IViewHelper：： commit**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568167(v=vs.85))方法的调用不会生成模式更改，则**Commit**必须调用 Win32 **BroadcastSystemMessage**函数，并且必须始终 post （使用 BSF\_POSTMESSAGE 广播选项） WM\_DISPLAYCHANGE 消息。 有关**BroadcastSystemMessage**的详细信息，请参阅 Microsoft Windows SDK 文档。

-   不能使用[**IViewHelper：： Commit**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568167(v=vs.85))方法代替对带有指定参数的 Win32 **ChangeDisplaySettingsEx**（**null**， **null** **，null，0**， **null**）函数的调用。 有关**ChangeDisplaySettingsEx**的详细信息，请参阅 Windows SDK 文档。

 

 





