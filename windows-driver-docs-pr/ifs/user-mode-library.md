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
ms.openlocfilehash: 018cd26d0cf3a0c9730fbd3be0d238091a27320d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380296"
---
# <a name="user-mode-library"></a>用户模式库


筛选器管理器用户模式接口提供常见功能包括筛选器驱动程序的产品。 用户模式下库是*Fltlib.dll*。 应用程序包括标头文件*FltUser.h*并*FltUserStructures.h*，并将其链接到*FltLib.lib*。

这些用户模式接口使常规控制微筛选器驱动程序和用户模式服务或控件的程序和筛选器驱动程序之间的通信。 用户模式接口还允许筛选器、 卷和实例的枚举的管理工具提供接口。

对于微筛选器，用户模式下通信 Api 不需要管理员权限。 相反，微筛选器定义必要的权限使用[ **ACL** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_acl)端口上定义。

### <a name="span-idfiltermanageruser-modelibraryroutinesspanspan-idfiltermanageruser-modelibraryroutinesspanspan-idfiltermanageruser-modelibraryroutinesspanfilter-manager-user-mode-library-routines"></a><span id="Filter_Manager_User-Mode_Library_Routines"></span><span id="filter_manager_user-mode_library_routines"></span><span id="FILTER_MANAGER_USER-MODE_LIBRARY_ROUTINES"></span>筛选管理器用户模式下库例程

筛选器管理器提供用户模式应用程序提供加载和卸载微筛选器驱动程序使用了以下支持的例程：

[**FilterLoad**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterload)

[**FilterUnload**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterunload)

有关创建和关闭微筛选器驱动程序和实例句柄提供了以下支持例程：

[**FilterClose**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterclose)

[**FilterCreate**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filtercreate)

[**FilterInstanceClose**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterinstanceclose)

[**FilterInstanceCreate**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterinstancecreate)

附加和分离微筛选器驱动程序实例提供以下支持例程：

[**FilterAttach**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterattach)

[**FilterAttachAtAltitude**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterattachataltitude)

[**FilterDetach**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterdetach)

用于枚举筛选器、 卷和实例提供了以下支持例程：

[**FilterFindFirst**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterfindfirst)

[**FilterFindNext**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterfindnext)

[**FilterInstanceFindFirst**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterinstancefindfirst)

[**FilterInstanceFindNext**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterinstancefindnext)

[**FilterVolumeFindFirst**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filtervolumefindfirst)

[**FilterVolumeFindNext**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filtervolumefindnext)

[**FilterVolumeInstanceFindFirst**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filtervolumeinstancefindfirst)

[**FilterVolumeInstanceFindNext**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filtervolumeinstancefindnext)

有关信息的查询提供了以下支持例程：

[**FilterGetDosName**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filtergetdosname)

[**FilterGetInformation**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filtergetinformation)

[**FilterInstanceGetInformation**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterinstancegetinformation)

通过用户操作发起的通信提供了以下支持例程：

[**FilterConnectCommunicationPort**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterconnectcommunicationport)

[**FilterSendMessage**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filtersendmessage)

为响应由微筛选器驱动程序启动的通信提供了以下支持例程：

[**FilterGetMessage**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filtergetmessage)

[**FilterReplyMessage**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterreplymessage)

 

 




