---
title: 定义通知类
description: 定义通知类
ms.assetid: e21cf020-0bf8-4091-aac4-6324a680194a
keywords:
- 通知对象 WDK 网络、 通知类
- 网络通知对象 WDK、 通知类
- 通知类 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dab93541cd8638eab721a361aa4ef8da381f6c59
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354595"
---
# <a name="defining-a-notify-class"></a>定义通知类





通知类必须实现，以便它们继承自[ **INetCfgComponentControl** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547725(v=vs.85))接口。 但是，如果通知对象执行某些操作，还必须实现其通知类从以下接口继承：

-   如果通知对象执行与安装、 升级和删除该对象所属的组件相关的操作，关联的通知类必须继承[ **INetCfgComponentSetup** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547758(v=vs.85))接口。

-   如果通知对象显示该对象所属的组件的自定义属性页，关联的通知类必须继承[ **INetCfgComponentPropertyUi** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547738(v=vs.85))接口。

-   如果通知对象的计算结果对网络配置子系统将绑定到其他网络组件该对象所属的组件的方式的更改，关联的通知类必须继承[INetCfgComponentNotifyBinding](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547730(v=vs.85))接口。

-   如果通知对象的计算结果可能会影响该对象所属的组件的网络配置的更改，关联的通知类必须继承[ **INetCfgComponentNotifyGlobal** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547733(v=vs.85))接口。

某些数据中的成员通知类应定义为通用的所有通知对象。 特定数据成员应定义为特定于其组件。 所有通知应定义对象的数据成员包括：

-   指向拥有的对象类型的网络组件的实例的指针[ **INetCfgComponent** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547715(v=vs.85))接口。 通知对象的实例使用此指针来访问和控制该对象所属的组件。

-   指向类型的网络配置对象的实例[ **INetCfg** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547694(v=vs.85))接口。 通知对象的实例使用此指针来访问网络配置的所有方面。

-   变量来存储该通知对象所属的组件的参数信息

-   用于指定通知对象之前执行的操作的变量。 定义常数以指示不同通知对象可能执行的操作。 网络配置子系统时调用的通知对象[ **INetCfgComponentControl::ApplyRegistryChanges** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547727(v=vs.85))方法将配置更改应用到注册表， **ApplyRegistryChanges**使用此变量来确定如何进行注册表更改。 例如，如果通知对象之前执行与安装在该对象所属的组件相关的操作，则其[ **INetCfgComponentSetup::Install** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547762(v=vs.85))方法，**安装**应设置此变量，以指示作为安装的操作。

-   类型的注册表项**HKEY**。 通知对象将调用[ **INetCfgComponent::OpenParamKey** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547890(v=vs.85))拥有打开和检索包含为组件的参数的注册表项的对象的组件的方法。 通知对象然后设置**HKEY**该注册表项的成员。

定义一个构造函数和析构函数为您的通知类。 此外请考虑定义仅通知类可以使用的私有方法。

所有**IUnknown**应通知类实现接口方法。 如果通知类继承自任何上述列表中所述的可选接口，则必须实现这些接口的所有方法。 请注意该 E\_NOTIMPL 不是有效返回类型的任何一种方法的通知对象接口。 如果通知对象不需要使用的特定方法的实现，只需实现此方法应返回 S\_确定。

 

 





