---
title: 安装、升级和删除组件
description: 安装、升级和删除组件
keywords:
- 通知对象 WDK 网络，删除网络组件
- 网络通知对象 WDK，删除网络组件
- 通知对象 WDK 网络，升级网络组件
- 网络通知对象 WDK，升级网络组件
- 通知对象 WDK 网络，安装网络组件
- 网络通知对象 WDK，安装网络组件
- 删除网络组件
- 升级网络组件 WDK，通知对象
- 安装网络组件 WDK，通知对象
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 97207a8d446773882317209ef6b85f3fcec95d34
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795961"
---
# <a name="installing-upgrading-and-removing-the-component"></a>安装、升级和删除组件





当网络配置子系统安装、升级或删除网络组件时，子系统还会调用组件的通知对象来完成安装、升级和删除。 可以实现组件的通知对象，以执行组件可能需要的操作。 例如：

-   可以实现用于虚拟 LAN 的多路复用器通知对象，以便在子系统安装多路复用器时，通知对象将安装多路复用器协议绑定到的虚拟适配器。

    若要安装虚拟适配器，notify 对象将调用网络配置的 [**INetCfgClassSetup：： install**](/previous-versions/windows/hardware/network/ff547711(v=vs.85)) 方法。 在此调用中，通知对象传递要安装的虚拟适配器的标识符。 Notify 对象可以从其 [**INetCfgComponentNotifyBinding：： NotifyBindingPath**](/previous-versions/windows/hardware/network/ff547731(v=vs.85))或 [**INetCfgComponentPropertyUi：： ApplyProperties**](/previous-versions/windows/hardware/network/ff547741(v=vs.85))方法中调用 **INetCfgClassSetup：： Install**。

    若要完成虚拟适配器的安装，操作系统需要虚拟适配器的 INF 文件。 若要确保可以找到此 INF 文件，在安装 multipexer 时，必须将该文件复制到操作系统。 有关详细信息，请参阅 [复制 inf](../install/copying-inf-files.md)。 本主题说明了使用共同安装程序或安装应用程序的 **CopyINF** 指令或对 **SetupCopyOEMInf** 函数的调用，可以将 INF 文件复制到目标系统的 inf 目录。 但是，如果使用 **SetupCopyOEMInf** 复制多路复用器 (原始 inf) 的 inf 文件，则还必须使用 **SetupCopyOEMInf** 复制虚拟适配器的 inf 文件，因为操作系统仅处理 **COPYINF** 指令（如果原始 inf 尚不在 inf 目录中）。

-   可以实现多路复用的通知对象，以便在子系统删除多路复用器时，通知对象将删除所有虚拟适配器。 若要删除虚拟适配器，notify 对象将调用网络配置的 [**INetCfgClassSetup：:D einstall**](/previous-versions/windows/hardware/network/ff547710(v=vs.85)) 方法。 在此调用中，通知对象将指针传递到虚拟适配器的 **INetCfgComponent** 接口。 Notify 对象可以从其 **INetCfgComponentNotifyBinding：： NotifyBindingPath** 或 **INetCfgComponentPropertyUi：： ApplyProperties** 方法调用 **INetCfgClassSetup：:D einstall**。

-   可以实现组件的通知对象，以便当子系统升级组件时，通知对象将更改组件的绑定路径的顺序。 若要更改此顺序，通知对象的 [**INetCfgComponentSetup：： Upgrade**](/previous-versions/windows/hardware/network/ff547783(v=vs.85)) 方法调用 [**INetCfgComponentBindings：： MoveBefore**](/previous-versions/windows/hardware/network/ff547722(v=vs.85)) 或 [**INetCfgComponentBindings：： MoveAfter**](/previous-versions/windows/hardware/network/ff547721(v=vs.85)) 方法。

 

