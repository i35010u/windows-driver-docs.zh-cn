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
ms.openlocfilehash: 931c81330d0ea0cac01d831382359a6eb19441b5
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212797"
---
# <a name="removing-network-components"></a>删除网络组件





网络组件由网络配置子系统删除。

**删除网络组件**

1.  网络配置子系统创建 notify 对象的一个实例，并调用该对象的 [**INetCfgComponentControl：： Initialize**](/previous-versions/windows/hardware/network/ff547729(v=vs.85)) 方法。 此方法初始化对象，并提供对组件和网络配置的所有方面的访问。

2.  子系统调用 notify 对象的 [**INetCfgComponentSetup：：**](/previous-versions/windows/hardware/network/ff547769(v=vs.85)) remove 方法，以执行删除组件所需的操作。 **删除**方法执行清理操作来准备组件的删除。

3.  子系统调用 notify 对象的 [**INetCfgComponentControl：： ApplyRegistryChanges**](/previous-versions/windows/hardware/network/ff547727(v=vs.85)) 方法来从注册表删除网络组件的相关信息。

 

