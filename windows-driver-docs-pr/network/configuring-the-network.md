---
title: 配置网络
description: 配置网络
ms.assetid: 9529467b-353d-41c3-9d4e-bb5df5c43665
keywords:
- 通知对象 WDK 网络，网络配置
- 网络通知对象 WDK，网络配置
- 通知 WDK 网络，网络配置
- 网络配置 WDK 通知 ofbject
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e4c22b9a84685413a23825d069fb6d1a45a56a42
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207613"
---
# <a name="configuring-the-network"></a>配置网络





Notify 对象可以为其提供网络组件，该组件对网络配置进行编程控制。

网络组件的属性可从网络控制面板应用程序进行配置。 单击 **网络** 图标时，会启动网络配置子系统，该子系统创建通知对象的实例并调用该对象的 [**INetCfgComponentControl：： Initialize**](/previous-versions/windows/hardware/network/ff547729(v=vs.85)) 方法。 此方法初始化对象，并提供对组件和网络配置的所有方面的访问。

网络配置子系统创建实例并初始化 notify 对象之后，子系统将调用 notify 对象的 [**INetCfgComponentNotifyGlobal：： GetSupportedNotifications**](/previous-versions/windows/hardware/network/ff547734(v=vs.85)) 方法来检索该对象所需的通知类型。 使用此信息，子系统可以将所需的通知发送到对象。 对象可以使用这些通知控制可能影响拥有对象的组件的网络设置和配置的各个方面。 例如，如果子系统调用 notify 对象的 [**INetCfgComponentNotifyGlobal：： SysQueryBindingPath**](/previous-versions/windows/hardware/network/ff547737(v=vs.85)) 方法来通知对象，子系统将要添加其他网络组件所属的绑定路径，则对象有机会请求子系统禁用该绑定路径。 此外，子系统还会调用 notify 对象的 [INetCfgComponentNotifyBinding](/previous-versions/windows/hardware/network/ff547730(v=vs.85)) 接口的任何方法。 这些方法通知对象有关子系统将其他网络组件绑定到拥有通知对象的组件的方式的更改。

 

