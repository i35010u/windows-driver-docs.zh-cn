---
title: IViewHelper Clone-View COM 对象的要求
description: IViewHelper Clone-View COM 对象的要求
ms.assetid: ef599874-64c5-480e-a7bc-666ababd4d08
keywords:
- TMM WDK 显示，IViewHelper 要求
- 监视器配置 WDK 显示区域，IViewHelper 要求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0adbda8fae172221a8a7789908c9bcaa1656552
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385662"
---
# <a name="requirements-of-an-iviewhelper-clone-view-com-object"></a>IViewHelper Clone-View COM 对象的要求


硬件供应商的克隆视图[IViewHelper](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index) COM 接口对象必须满足以下要求：

-   COM 对象必须驻留在动态链接库 (DLL)，它是 COM 进程 （进程内） 服务器。

-   COM 对象的实现必须是不透明的操作系统。

-   [IViewHelper](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)接口必须提供用于获取和设置拓扑数据，其中包括克隆视图的方法。

-   因此，会显示两个或多个监视器上硬件供应商必须找到克隆视图的显示模式工作。

-   如果 COM 对象调用[ **IViewHelper::Commit** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568167(v=vs.85))方法不会生成模式下更改**提交**必须调用 Win32 **BroadcastSystemMessage**函数，并始终必须发布 (使用 BSF\_POSTMESSAGE 广播选项) WM\_DISPLAYCHANGE 消息。 有关详细信息**BroadcastSystemMessage**，请参阅 Microsoft Windows SDK 文档。

-   [ **IViewHelper::Commit** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568167(v=vs.85))方法不能使用代替调用 Win32 **ChangeDisplaySettingsEx**(**NULL**， **NULL**， **NULL**，0， **NULL**) 具有所指示的参数的函数。 有关详细信息**ChangeDisplaySettingsEx**，请参阅 Windows SDK 文档。

 

 





