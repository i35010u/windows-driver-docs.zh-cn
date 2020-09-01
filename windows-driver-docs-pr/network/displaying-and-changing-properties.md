---
title: 显示和更改属性
description: 显示和更改属性
ms.assetid: 657b687d-b0c0-46e0-a948-242509590a4b
keywords:
- 通知对象 WDK 网络，属性页
- 网络通知对象 WDK，属性页
- 属性页 WDK 网络
- 属性 WDK 网络
- 显示网络配置属性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 59623c055d7e215ae00bafe6975cebe208b85b23
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212515"
---
# <a name="displaying-and-changing-properties"></a>显示和更改属性





网络配置子系统显示网络组件的属性页，并更改该组件的参数。

可以从 "控制面板" 中显示和修改组件的属性。 单击 **网络** 图标时，会启动网络配置子系统，该子系统创建通知对象的实例并调用该对象的 [**INetCfgComponentControl：： Initialize**](/previous-versions/windows/hardware/network/ff547729(v=vs.85)) 方法。 此方法初始化对象，并提供对组件和网络配置的所有方面的访问。

应用程序调用组件的 [**INetCfgComponent：： RaisePropertyUi**](/previous-versions/windows/hardware/network/ff547895(v=vs.85)) 方法来显示组件的属性。 然后， **RaisePropertyUi** 方法调用以下通知对象方法：

-   [**INetCfgComponentPropertyUi：： QueryPropertyUi**](/previous-versions/windows/hardware/network/ff547749(v=vs.85)) 方法来确定特定上下文是否适合显示该组件的属性。

-   [**INetCfgComponentPropertyUi：： SetContext**](/previous-versions/windows/hardware/network/ff547752(v=vs.85)) 方法，以指示组件的通知对象在指定的上下文中显示组件的属性。

-   [**INetCfgComponentPropertyUi：： MergePropPages**](/previous-versions/windows/hardware/network/ff547746(v=vs.85)) 方法用于创建组件的属性表并将其合并到默认集。

如果用户在一个自定义页上更改了某个组件的参数， **RaisePropertyUi** 将调用 notify 对象的 [**INetCfgComponentPropertyUi：： ApplyProperties**](/previous-versions/windows/hardware/network/ff547741(v=vs.85)) 方法，以将更改存储在内存中。

若要应用更改，网络配置子系统将调用 notify 对象的 [**INetCfgComponentControl：： ApplyRegistryChanges**](/previous-versions/windows/hardware/network/ff547727(v=vs.85)) 方法来修改有关注册表中的网络组件的信息。 若要用修改后的信息配置组件的驱动程序，网络配置子系统将调用 notify 对象的 [**INetCfgComponentControl：： ApplyPnpChanges**](/previous-versions/windows/hardware/network/ff547726(v=vs.85)) 方法并传递 [**INetCfgPnpReconfigCallback**](/previous-versions/windows/hardware/network/ff547935(v=vs.85)) 接口。

 

