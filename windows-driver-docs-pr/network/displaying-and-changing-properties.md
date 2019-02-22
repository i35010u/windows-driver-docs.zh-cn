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
ms.openlocfilehash: 7f23c47240e50ac78268d69fa11bd29fbe410cbf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521703"
---
# <a name="displaying-and-changing-properties"></a>显示和更改属性





网络配置子系统显示的网络组件的属性页并更改组件的参数。

可以显示和修改从控制面板组件的属性。 当您单击**网络**图标，在开始网络配置子系统，它创建的通知对象实例并调用该对象的[ **INetCfgComponentControl::Initialize**](https://msdn.microsoft.com/library/windows/hardware/ff547729)方法。 此方法将对象初始化，并提供对组件和网络配置的所有方面的访问。

应用程序调用该组件的[ **INetCfgComponent::RaisePropertyUi** ](https://msdn.microsoft.com/library/windows/hardware/ff547895)方法以显示组件的属性。 **RaisePropertyUi**方法然后调用以下通知对象方法：

-   [**INetCfgComponentPropertyUi::QueryPropertyUi** ](https://msdn.microsoft.com/library/windows/hardware/ff547749)方法来确定特定上下文是否适合以显示该组件的属性。

-   [**INetCfgComponentPropertyUi::SetContext** ](https://msdn.microsoft.com/library/windows/hardware/ff547752)方法指示组件的通知对象中指定的上下文中显示组件的属性。

-   [**INetCfgComponentPropertyUi::MergePropPages** ](https://msdn.microsoft.com/library/windows/hardware/ff547746)方法创建并合并到默认组的自定义组件的属性表页。

如果用户更改其中一个自定义页面上的组件的参数之一**RaisePropertyUi**调用通知对象[ **INetCfgComponentPropertyUi::ApplyProperties** ](https://msdn.microsoft.com/library/windows/hardware/ff547741)方法将更改保存到内存。

若要应用更改，网络配置子系统调用通知对象[ **INetCfgComponentControl::ApplyRegistryChanges** ](https://msdn.microsoft.com/library/windows/hardware/ff547727)方法来修改有关中的网络组件的信息在注册表中。 若要修改的信息配置组件的驱动程序的网络配置子系统调用通知对象[ **INetCfgComponentControl::ApplyPnpChanges** ](https://msdn.microsoft.com/library/windows/hardware/ff547726)方法，并传递[ **INetCfgPnpReconfigCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff547935)接口。

 

 





