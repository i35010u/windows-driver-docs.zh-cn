---
title: 用户模式库
description: 用户模式库
ms.assetid: a471ae15-bbdd-47c8-ad77-9b82281dd430
keywords:
- 筛选器管理器 WDK 文件系统微筛选器，用户模式库
- 用户模式库 WDK 文件系统微筛选器
- Fltlib.dll
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03ca180cba8a1c155ee566e1c97320d207a85053
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065508"
---
# <a name="user-mode-library"></a>用户模式库


筛选器管理器用户模式接口为包含筛选器驱动程序的产品提供通用功能。 用户模式库 *Fltlib.dll*。 应用程序包括头文件 *FltUser* 和 *FltUserStructures*，并链接到 *FltLib*。

这些用户模式接口可以实现对微筛选器驱动程序的常规控制，以及用户模式服务或控制程序与筛选器驱动程序之间的通信。 用户模式接口还为允许枚举筛选器、卷和实例的管理工具提供接口。

对于 minifilters，用户模式通信 Api 不需要管理员权限。 相反，微筛选器使用端口上定义的 [**ACL**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_acl) 来定义所需的权限。

### <a name="span-idfilter_manager_user-mode_library_routinesspanspan-idfilter_manager_user-mode_library_routinesspanspan-idfilter_manager_user-mode_library_routinesspanfilter-manager-user-mode-library-routines"></a><span id="Filter_Manager_User-Mode_Library_Routines"></span><span id="filter_manager_user-mode_library_routines"></span><span id="FILTER_MANAGER_USER-MODE_LIBRARY_ROUTINES"></span>筛选器管理器用户模式库例程

筛选器管理器为用户模式应用程序提供了以下用于加载和卸载微筛选器驱动程序的支持例程：

[**FilterLoad**](/windows/desktop/api/fltuser/nf-fltuser-filterload)

[**FilterUnload**](/windows/desktop/api/fltuser/nf-fltuser-filterunload)

提供以下支持例程用于创建和关闭微筛选器驱动程序和实例句柄：

[**FilterClose**](/windows/desktop/api/fltuser/nf-fltuser-filterclose)

[**FilterCreate**](/windows/desktop/api/fltuser/nf-fltuser-filtercreate)

[**FilterInstanceClose**](/windows/desktop/api/fltuser/nf-fltuser-filterinstanceclose)

[**FilterInstanceCreate**](/windows/desktop/api/fltuser/nf-fltuser-filterinstancecreate)

提供以下支持例程用于附加和分离微筛选器驱动程序实例：

[**FilterAttach**](/windows/desktop/api/fltuser/nf-fltuser-filterattach)

[**FilterAttachAtAltitude**](/windows/desktop/api/fltuser/nf-fltuser-filterattachataltitude)

[**FilterDetach**](/windows/desktop/api/fltuser/nf-fltuser-filterdetach)

提供以下支持例程用于枚举筛选器、卷和实例：

[**FilterFindFirst**](/windows/desktop/api/fltuser/nf-fltuser-filterfindfirst)

[**FilterFindNext**](/windows/desktop/api/fltuser/nf-fltuser-filterfindnext)

[**FilterInstanceFindFirst**](/windows/desktop/api/fltuser/nf-fltuser-filterinstancefindfirst)

[**FilterInstanceFindNext**](/windows/desktop/api/fltuser/nf-fltuser-filterinstancefindnext)

[**FilterVolumeFindFirst**](/windows/desktop/api/fltuser/nf-fltuser-filtervolumefindfirst)

[**FilterVolumeFindNext**](/windows/desktop/api/fltuser/nf-fltuser-filtervolumefindnext)

[**FilterVolumeInstanceFindFirst**](/windows/desktop/api/fltuser/nf-fltuser-filtervolumeinstancefindfirst)

[**FilterVolumeInstanceFindNext**](/windows/desktop/api/fltuser/nf-fltuser-filtervolumeinstancefindnext)

提供以下支持例程来查询信息：

[**FilterGetDosName**](/windows/desktop/api/fltuser/nf-fltuser-filtergetdosname)

[**FilterGetInformation**](/windows/desktop/api/fltuser/nf-fltuser-filtergetinformation)

[**FilterInstanceGetInformation**](/windows/desktop/api/fltuser/nf-fltuser-filterinstancegetinformation)

为用户操作启动的通信提供以下支持例程：

[**FilterConnectCommunicationPort**](/windows/desktop/api/fltuser/nf-fltuser-filterconnectcommunicationport)

[**FilterSendMessage**](/windows/desktop/api/fltuser/nf-fltuser-filtersendmessage)

提供了以下支持例程来响应微筛选器驱动程序启动的通信：

[**FilterGetMessage**](/windows/desktop/api/fltuser/nf-fltuser-filtergetmessage)

[**FilterReplyMessage**](/windows/desktop/api/fltuser/nf-fltuser-filterreplymessage)

 

