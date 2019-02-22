---
title: 配置网络
description: 配置网络
ms.assetid: 9529467b-353d-41c3-9d4e-bb5df5c43665
keywords:
- 通知对象 WDK 网络，网络配置
- 通知对象 WDK，网络配置网络
- 通知 WDK 网络，网络配置
- 网络配置 WDK 通知 ofbject
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f78f81f9bf90ee0f6076269363ce9cdea10b6adf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525968"
---
# <a name="configuring-the-network"></a>配置网络





通知对象可以提供以编程方式控制网络配置与拥有它的网络组件。

可以从网络控制面板应用程序中配置网络组件的属性。 当您单击**网络**图标，在开始网络配置子系统，它创建的通知对象实例并调用该对象的[ **INetCfgComponentControl::Initialize**](https://msdn.microsoft.com/library/windows/hardware/ff547729)方法。 此方法将对象初始化，并提供对组件和网络配置的所有方面的访问。

子系统的网络配置子系统创建的实例并初始化通知对象后，调用通知对象的[ **INetCfgComponentNotifyGlobal::GetSupportedNotifications** ](https://msdn.microsoft.com/library/windows/hardware/ff547734)方法来检索通知所需的对象的类型。 使用此信息，子系统可以将所需的通知发送到对象。 该对象可以使用这些通知来控制的网络安装和配置可能会影响该对象所属的组件的方面。 例如，如果子系统调用通知对象的[ **INetCfgComponentNotifyGlobal::SysQueryBindingPath** ](https://msdn.microsoft.com/library/windows/hardware/ff547737)方法以通知子系统是要将绑定路径添加到其中的对象属于其他网络组件，该对象具有请求的子系统，禁用该绑定路径的机会。 此外，该子系统调用的任何通知对象的方法[INetCfgComponentNotifyBinding](https://msdn.microsoft.com/library/windows/hardware/ff547730)接口。 这些方法通知子系统的方式的更改的对象将其他网络组件绑定到通知对象所属的组件。

 

 





