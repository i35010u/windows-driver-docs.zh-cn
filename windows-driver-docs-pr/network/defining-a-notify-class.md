---
title: 定义通知类
description: 定义通知类
ms.assetid: e21cf020-0bf8-4091-aac4-6324a680194a
keywords:
- 通知对象 WDK 网络，通知类
- 网络通知对象 WDK，通知类
- 通知类 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d31b6488ee7cd9db7dee3632769479c7512606a2
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211097"
---
# <a name="defining-a-notify-class"></a>定义通知类





必须实现通知类，以便它们继承自 [**INetCfgComponentControl**](/previous-versions/windows/hardware/network/ff547725(v=vs.85)) 接口。 但是，如果 "通知对象" 执行某些操作，还必须实现其通知类，才能从以下接口继承：

-   如果通知对象执行的操作与安装、升级和删除拥有对象的组件有关，则关联的通知类必须继承自 [**INetCfgComponentSetup**](/previous-versions/windows/hardware/network/ff547758(v=vs.85)) 接口。

-   如果某个通知对象显示拥有该对象的组件的自定义属性页，则关联的通知类必须继承自 [**INetCfgComponentPropertyUi**](/previous-versions/windows/hardware/network/ff547738(v=vs.85)) 接口。

-   如果通知对象评估网络配置子系统将拥有对象的组件绑定到其他网络组件的方式的更改，则关联的 notify 类必须继承自 [INetCfgComponentNotifyBinding](/previous-versions/windows/hardware/network/ff547730(v=vs.85)) 接口。

-   如果通知对象评估可能会影响拥有对象的组件的网络配置更改，则关联的通知类必须继承自 [**INetCfgComponentNotifyGlobal**](/previous-versions/windows/hardware/network/ff547733(v=vs.85)) 接口。

通知类中的某些数据成员应定义为所有通知对象共有的数据成员。 某些数据成员应定义为特定于其组件的数据成员。 所有通知对象应定义的数据成员包括：

-   指向网络组件的实例的指针，该对象拥有 [**INetCfgComponent**](/previous-versions/windows/hardware/network/ff547715(v=vs.85)) 接口类型的对象。 通知对象的实例使用此指针访问和控制拥有对象的组件。

-   指向 [**INetCfg**](/previous-versions/windows/hardware/network/ff547694(v=vs.85)) 接口类型的网络配置对象的实例的指针。 Notify 对象的实例使用此指针来访问网络配置的所有方面。

-   用于存储拥有通知对象的组件的参数信息的变量

-   一个变量，该变量指定通知对象先前执行的操作。 定义常量以指示对象可能执行的不同操作。 当网络配置子系统调用 notify 对象的 [**INetCfgComponentControl：： ApplyRegistryChanges**](/previous-versions/windows/hardware/network/ff547727(v=vs.85)) 方法将配置更改应用到注册表时， **ApplyRegistryChanges** 将使用此变量来确定如何更改注册表。 例如，如果通知对象先前执行了与在其 [**INetCfgComponentSetup：： Install**](/previous-versions/windows/hardware/network/ff547762(v=vs.85)) 方法中安装拥有对象的组件相关的操作，则 **安装** 应将此变量设置为将操作指示为 "安装"。

-   **HKEY**类型的注册表项。 Notify 对象调用拥有对象的组件的 [**INetCfgComponent：： OpenParamKey**](/previous-versions/windows/hardware/network/ff547890(v=vs.85)) 方法来打开和检索包含组件参数的注册表项。 然后，通知对象将 **HKEY** 成员设置为该密钥。

为 notify 类定义构造函数和析构函数。 还应考虑定义只有 notify 类可以使用的私有方法。

应为 notify 类实现所有 **IUnknown** 接口方法。 如果通知类从前面的列表中所述的任何可选接口继承，则必须实现这些接口的所有方法。 请注意， \_ 对于任何通知对象接口的方法，E NOTIMPL 不是有效的返回类型。 如果通知对象不需要特定方法的实现，只需实现方法即可返回 \_ "OK"。

 

