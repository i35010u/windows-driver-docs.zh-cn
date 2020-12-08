---
title: 删除网络组件
description: 删除网络组件
keywords:
- 通知对象 WDK 网络，删除网络组件
- 网络通知对象 WDK，删除网络组件
- 网络组件删除 WDK
- 删除网络组件
- 通知 WDK 网络，删除网络组件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8615745d4a7635b7a797b4f36d3149a54498a094
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815911"
---
# <a name="removing-network-components"></a>删除网络组件





网络组件由网络配置子系统删除。

**删除网络组件**

1.  网络配置子系统创建 notify 对象的一个实例，并调用该对象的 [**INetCfgComponentControl：： Initialize**](/previous-versions/windows/hardware/network/ff547729(v=vs.85)) 方法。 此方法初始化对象，并提供对组件和网络配置的所有方面的访问。

2.  子系统调用 notify 对象的 [**INetCfgComponentSetup：：**](/previous-versions/windows/hardware/network/ff547769(v=vs.85)) remove 方法，以执行删除组件所需的操作。 **删除** 方法执行清理操作来准备组件的删除。

3.  子系统调用 notify 对象的 [**INetCfgComponentControl：： ApplyRegistryChanges**](/previous-versions/windows/hardware/network/ff547727(v=vs.85)) 方法来从注册表删除网络组件的相关信息。

 

