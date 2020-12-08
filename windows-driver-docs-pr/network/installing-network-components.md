---
title: 安装网络组件
description: 安装网络组件
keywords:
- 通知对象 WDK 网络，安装网络组件
- 网络通知对象 WDK，安装网络组件
- 安装网络组件 WDK，步骤
- 网络组件安装 WDK，步骤
- 通知 WDK 网络，安装网络组件
ms.date: 01/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: 2c09e696dd423aa9191ab7d1e65814e621ddc37e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840901"
---
# <a name="installing-network-components"></a>安装网络组件

网络组件由网络配置子系统安装。

**安装网络组件**

1.  网络配置子系统为特定组件类型调用类安装程序。 然后，类安装程序调用安装程序 API 以从组件的 INF 文件中检索信息并安装组件。

    如果组件拥有 notify 对象，则类安装程序将检索包含 notify 对象的 DLL 的名称。 此 DLL 出现在组件的 INF 文件中，如下所示：

    ```INF
    HKR, Ndi, ComponentDll,     0,     "notifyobject.dll"
    ```

    类安装程序调用 DLL 的入口点函数以注册通知对象。 网络配置子系统创建 notify 对象的一个实例，并调用该对象的 [**INetCfgComponentControl：： Initialize**](/previous-versions/windows/hardware/network/ff547729(v=vs.85)) 方法。 此方法初始化对象，并提供对组件和网络配置的所有方面的访问。

2.  若要执行安装组件所需的操作，网络配置子系统将调用 notify 对象的 [**INetCfgComponentSetup：： install**](/previous-versions/windows/hardware/network/ff547762(v=vs.85)) 方法。

    如果组件的安装处于无人参与，则网络配置子系统将调用 notify 对象的 [**INetCfgComponentSetup：： ReadAnswerFile**](/previous-versions/windows/hardware/network/ff547765(v=vs.85)) 方法。 此方法将打开一个文件中的组件参数，并从该文件中检索称为 *应答文件* 的无人参与安装程序的参数。

3.  网络配置子系统创建实例并初始化 notify 对象之后，子系统将调用 notify 对象的 [**INetCfgComponentNotifyGlobal：： GetSupportedNotifications**](/previous-versions/windows/hardware/network/ff547734(v=vs.85)) 方法来检索该对象所需的通知类型。 子系统使用该信息将所需的通知发送到对象。 对象可以使用这些通知控制可能影响拥有对象的组件的网络设置和配置的各个方面。 例如，如果子系统调用 [**INetCfgComponentNotifyGlobal：： SysNotifyComponent**](/previous-versions/windows/hardware/network/ff547736(v=vs.85)) 方法来通知对象子系统安装或删除了另一个网络组件，则该对象有机会执行与更改相关的操作。

    网络配置子系统创建实例并初始化 notify 对象之后，子系统还会调用通知对象的 [INetCfgComponentNotifyBinding](/previous-versions/windows/hardware/network/ff547730(v=vs.85)) 接口的任何方法，以通知对象对子系统将其他网络组件绑定到拥有通知对象的组件的方式发生了更改。

4.  当网络配置子系统准备好将组件的属性应用于操作系统时，它将调用 notify 对象的 [**INetCfgComponentControl：： ApplyRegistryChanges**](/previous-versions/windows/hardware/network/ff547727(v=vs.85)) 方法以在组件的注册表项下分配组件的参数。 Notify 对象调用其组件的 [**INetCfgComponent：： OpenParamKey**](/previous-versions/windows/hardware/network/ff547890(v=vs.85)) 方法来打开和检索组件的注册表项。

5.  若要配置组件的驱动程序，网络配置子系统将调用 notify 对象的 [**INetCfgComponentControl：： ApplyPnpChanges**](/previous-versions/windows/hardware/network/ff547726(v=vs.85)) 方法并传递 [**INetCfgPnpReconfigCallback**](/previous-versions/windows/hardware/network/ff547935(v=vs.85)) 接口。 Notify 对象调用 [**INetCfgPnpReconfigCallback：： SendPnpReconfig**](/previous-versions/windows/hardware/network/ff547943(v=vs.85)) 方法将配置信息发送到其组件的驱动程序。

有关无人参与安装的安装程序 API 和文件的详细信息，请参阅 Microsoft Windows SDK。
