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
ms.openlocfilehash: b06941107443b7f571ec4440055e53a4de587f4e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373299"
---
# <a name="removing-network-components"></a>删除网络组件





网络配置子系统通过移除网络组件。

**若要删除某个网络组件**

1.  网络配置子系统创建通知对象的实例并调用该对象的[ **INetCfgComponentControl::Initialize** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547729(v=vs.85))方法。 此方法将对象初始化，并提供对组件和网络配置的所有方面的访问。

2.  子系统调用通知对象的[ **INetCfgComponentSetup::Removing** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547769(v=vs.85))方法执行删除该组件所需的操作。 **删除**方法执行清理操作，准备用于组件的删除。

3.  子系统调用通知对象的[ **INetCfgComponentControl::ApplyRegistryChanges** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547727(v=vs.85))方法从注册表中删除有关网络组件的信息。

 

 





