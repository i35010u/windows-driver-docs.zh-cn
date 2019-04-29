---
title: 删除网络组件
description: 删除网络组件
ms.assetid: db1928ff-7570-411c-b770-274428a0d432
keywords:
- 通知对象 WDK 网络，删除网络组件
- 网络通知对象 WDK，删除网络组件
- 网络组件删除 WDK
- 删除网络组件
- 通知 WDK 网络，删除网络组件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c41c95fcf2fa73e00c534cbc793adc70573c2fb3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358797"
---
# <a name="removing-network-components"></a>删除网络组件





网络配置子系统通过移除网络组件。

**若要删除某个网络组件**

1.  网络配置子系统创建通知对象的实例并调用该对象的[ **INetCfgComponentControl::Initialize** ](https://msdn.microsoft.com/library/windows/hardware/ff547729)方法。 此方法将对象初始化，并提供对组件和网络配置的所有方面的访问。

2.  子系统调用通知对象的[ **INetCfgComponentSetup::Removing** ](https://msdn.microsoft.com/library/windows/hardware/ff547769)方法执行删除该组件所需的操作。 **删除**方法执行清理操作，准备用于组件的删除。

3.  子系统调用通知对象的[ **INetCfgComponentControl::ApplyRegistryChanges** ](https://msdn.microsoft.com/library/windows/hardware/ff547727)方法从注册表中删除有关网络组件的信息。

 

 





