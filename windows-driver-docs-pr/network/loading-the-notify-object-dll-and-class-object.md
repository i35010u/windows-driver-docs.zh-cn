---
title: 加载通知对象 DLL 和类对象
description: 加载通知对象 DLL 和类对象
keywords:
- 通知对象 WDK 网络，加载对象
- 网络通知对象 WDK，加载对象
- 加载对象 WDK 通知对象
- Dll WDK 通知对象
- 类对象 WDK 通知对象
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef509de6bc7ca381154ef6bdc9a6c941fc281984
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833407"
---
# <a name="loading-the-notify-object-dll-and-class-object"></a>加载通知对象 DLL 和类对象





网络组件的通知对象应作为组件对象模型实现 (COM) 对象。 这些 COM 对象驻留在作为 COM 组件服务器的 Dll 中。 有关开发 DLL COM 服务器的详细信息，请参阅 Microsoft Windows SDK。

应该实现特定通知对象的 DLL，以便导出一组入口点函数：

-   一个 **DllMain** 函数，可让网络配置子系统将 DLL 加载到子系统的虚拟地址空间。

-   **DllRegisterServer** 和 **DllUnregisterServer** 函数将信息放入 DLL 的类对象的操作系统注册表。 网络配置子系统使用此注册表信息来查找和加载网络组件的通知对象。

-   一个 **DllCanUnloadNow** 函数，它允许网络配置子系统确定 DLL 是否正在使用中。 如果未使用 DLL，则子系统可以从内存中安全地卸载 DLL。

为了使通知对象 DLL 成为 COM 服务器，它必须为服务器支持的通知对象公开类工厂。 此类工厂允许网络配置子系统创建通知对象的实例。 类工厂应继承自 **IClassFactory** 接口。 有关实现继承自 **IClassFactory** 的类的详细信息，请参阅 Windows SDK。

 

 





