---
title: 加载通知对象 DLL 和类对象
description: 加载通知对象 DLL 和类对象
ms.assetid: 846c0ed8-5299-4803-983a-9347e912d96b
keywords:
- 通知对象 WDK 网络，加载对象
- 网络通知对象 WDK，加载对象
- 将对象加载 WDK 通知对象
- Dll WDK 通知对象
- 类对象 WDK 通知对象
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4aaa800978ff03f38d81704879b0b3b3a51e31c8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575276"
---
# <a name="loading-the-notify-object-dll-and-class-object"></a>加载通知对象 DLL 和类对象





通知对象的网络组件应实现作为组件对象模型 (COM) 对象。 这些 COM 对象驻留在 Dll 是 COM 组件服务器。 有关开发 DLL COM 服务器的详细信息，请参阅 Microsoft Windows SDK。

应实现的特定通知对象的 DLL 导出一组的入口点函数：

-   一个**DllMain**函数以便将 DLL 加载到子系统的虚拟地址空间的网络配置子系统。

-   **DllRegisterServer**并**DllUnregisterServer**函数以将操作系统注册表的信息放的 DLL 的类对象。 网络配置子系统使用此注册表信息来定位和加载网络组件的通知的对象。

-   一个**DllCanUnloadNow**函数以便确定 DLL 是否正在使用的网络配置子系统。 如果 DLL 未正在使用中，子系统可以安全地卸载 DLL 从内存。

为了使通知对象 DLL 是 COM 服务器，它必须公开一个类工厂的通知对象服务器支持。 此类工厂允许创建的通知对象实例的网络配置子系统。 类工厂应继承自**IClassFactory**接口。 有关实现继承的类的详细信息**IClassFactory**，请参阅 Windows SDK。

 

 





