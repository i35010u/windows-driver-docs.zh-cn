---
title: 安装网络组件
description: 安装网络组件
ms.assetid: b4e5d73a-4943-498d-bf59-a08e3732baa8
keywords:
- 通知对象 WDK 网络，安装网络组件
- 网络通知对象 WDK，安装网络组件
- 安装网络组件 WDK，步骤
- 网络组件安装 WDK，步骤
- 通知 WDK 网络，安装网络组件
ms.date: 01/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: f308279c7ed2deecc7fc8692b8832f8b7a19a069
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385845"
---
# <a name="installing-network-components"></a>安装网络组件

网络配置子系统安装网络组件。

**若要安装网络组件**

1.  网络配置子系统为特定的组件类型调用类安装程序。 类安装程序然后调用安装程序 API 从组件的 INF 文件中检索信息和要安装该组件。

    如果该组件拥有通知对象，类安装程序会检索包含通知对象的 DLL 的名称。 此 DLL 组件的 INF 文件中显示，如下所示：

    ```INF
    HKR, Ndi, ComponentDll,     0,     "notifyobject.dll"
    ```

    类安装程序调用 DLL 的入口点函数，以注册通知对象。 网络配置子系统创建通知对象的实例并调用该对象的[ **INetCfgComponentControl::Initialize** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547729(v=vs.85))方法。 此方法将对象初始化，并提供对组件和网络配置的所有方面的访问。

2.  若要执行安装的组件所需操作，网络配置子系统调用通知对象[ **INetCfgComponentSetup::Install** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547762(v=vs.85))方法。

    如果无人参与安装的组件，网络配置子系统调用通知对象的[ **INetCfgComponentSetup::ReadAnswerFile** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547765(v=vs.85))方法。 此方法打开并检索从名为的无人参与安装文件中组件的参数*答案文件*。

3.  子系统的网络配置子系统创建的实例并初始化通知对象后，调用通知对象的[ **INetCfgComponentNotifyGlobal::GetSupportedNotifications** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547734(v=vs.85))方法来检索通知所需的对象的类型。 子系统使用此信息来将所需的通知发送到该对象。 该对象可以使用这些通知来控制的网络安装和配置可能会影响该对象所属的组件的方面。 例如，如果调用子系统[ **INetCfgComponentNotifyGlobal::SysNotifyComponent** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547736(v=vs.85))方法以通知对象子系统安装或删除另一个网络组件，对象有机会执行与更改相关的操作。

    网络配置子系统创建的实例并初始化通知对象后，子系统还调用任何一种通知对象的方法[INetCfgComponentNotifyBinding](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547730(v=vs.85))接口来通知对象有关更改的方式子系统将其他网络组件绑定到通知对象所属的组件。

4.  当网络配置子系统已准备好应用于操作系统的组件的属性时，它将调用的通知对象[ **INetCfgComponentControl::ApplyRegistryChanges** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547727(v=vs.85))若要分配组件的注册表项下的组件的参数的方法。 通知对象将调用其组件[ **INetCfgComponent::OpenParamKey** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547890(v=vs.85))方法以打开并检索组件的注册表项。

5.  若要配置该组件的驱动程序，网络配置子系统调用通知对象[ **INetCfgComponentControl::ApplyPnpChanges** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547726(v=vs.85))方法，并传递[ **INetCfgPnpReconfigCallback** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547935(v=vs.85))接口。 通知对象调用[ **INetCfgPnpReconfigCallback::SendPnpReconfig** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547943(v=vs.85))方法将发送到其组件的驱动程序的配置信息。

有关安装程序 API 和无人参与安装文件的详细信息，请参阅 Microsoft Windows SDK。