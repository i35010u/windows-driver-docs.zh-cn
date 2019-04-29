---
title: 用户模式库
description: 用户模式库
ms.assetid: a471ae15-bbdd-47c8-ad77-9b82281dd430
keywords:
- 筛选器管理器 WDK 文件系统微筛选器，用户模式库
- 用户模式下库 WDK 文件系统微筛选器
- Fltlib.dll
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01d57cbc7cebe19d46a33505edff7188921fef6f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389598"
---
# <a name="user-mode-library"></a>用户模式库


筛选器管理器用户模式接口提供常见功能包括筛选器驱动程序的产品。 用户模式下库是*Fltlib.dll*。 应用程序包括标头文件*FltUser.h*并*FltUserStructures.h*，并将其链接到*FltLib.lib*。

这些用户模式接口使常规控制微筛选器驱动程序和用户模式服务或控件的程序和筛选器驱动程序之间的通信。 用户模式接口还允许筛选器、 卷和实例的枚举的管理工具提供接口。

对于微筛选器，用户模式下通信 Api 不需要管理员权限。 相反，微筛选器定义必要的权限使用[ **ACL** ](https://msdn.microsoft.com/library/windows/hardware/ff538866)端口上定义。

### <a name="span-idfiltermanageruser-modelibraryroutinesspanspan-idfiltermanageruser-modelibraryroutinesspanspan-idfiltermanageruser-modelibraryroutinesspanfilter-manager-user-mode-library-routines"></a><span id="Filter_Manager_User-Mode_Library_Routines"></span><span id="filter_manager_user-mode_library_routines"></span><span id="FILTER_MANAGER_USER-MODE_LIBRARY_ROUTINES"></span>筛选管理器用户模式下库例程

筛选器管理器提供用户模式应用程序提供加载和卸载微筛选器驱动程序使用了以下支持的例程：

[**FilterLoad**](https://msdn.microsoft.com/library/windows/hardware/ff541504)

[**FilterUnload**](https://msdn.microsoft.com/library/windows/hardware/ff541516)

有关创建和关闭微筛选器驱动程序和实例句柄提供了以下支持例程：

[**FilterClose**](https://msdn.microsoft.com/library/windows/hardware/ff540453)

[**FilterCreate**](https://msdn.microsoft.com/library/windows/hardware/ff540467)

[**FilterInstanceClose**](https://msdn.microsoft.com/library/windows/hardware/ff540524)

[**FilterInstanceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff540528)

附加和分离微筛选器驱动程序实例提供以下支持例程：

[**FilterAttach**](https://msdn.microsoft.com/library/windows/hardware/ff540442)

[**FilterAttachAtAltitude**](https://msdn.microsoft.com/library/windows/hardware/ff540448)

[**FilterDetach**](https://msdn.microsoft.com/library/windows/hardware/ff540475)

用于枚举筛选器、 卷和实例提供了以下支持例程：

[**FilterFindFirst**](https://msdn.microsoft.com/library/windows/hardware/ff540485)

[**FilterFindNext**](https://msdn.microsoft.com/library/windows/hardware/ff540488)

[**FilterInstanceFindFirst**](https://msdn.microsoft.com/library/windows/hardware/ff540541)

[**FilterInstanceFindNext**](https://msdn.microsoft.com/library/windows/hardware/ff541493)

[**FilterVolumeFindFirst**](https://msdn.microsoft.com/library/windows/hardware/ff541525)

[**FilterVolumeFindNext**](https://msdn.microsoft.com/library/windows/hardware/ff541530)

[**FilterVolumeInstanceFindFirst**](https://msdn.microsoft.com/library/windows/hardware/ff541541)

[**FilterVolumeInstanceFindNext**](https://msdn.microsoft.com/library/windows/hardware/ff541551)

有关信息的查询提供了以下支持例程：

[**FilterGetDosName**](https://msdn.microsoft.com/library/windows/hardware/ff540492)

[**FilterGetInformation**](https://msdn.microsoft.com/library/windows/hardware/ff540500)

[**FilterInstanceGetInformation**](https://msdn.microsoft.com/library/windows/hardware/ff541499)

通过用户操作发起的通信提供了以下支持例程：

[**FilterConnectCommunicationPort**](https://msdn.microsoft.com/library/windows/hardware/ff540460)

[**FilterSendMessage**](https://msdn.microsoft.com/library/windows/hardware/ff541513)

为响应由微筛选器驱动程序启动的通信提供了以下支持例程：

[**FilterGetMessage**](https://msdn.microsoft.com/library/windows/hardware/ff540506)

[**FilterReplyMessage**](https://msdn.microsoft.com/library/windows/hardware/ff541508)

 

 




