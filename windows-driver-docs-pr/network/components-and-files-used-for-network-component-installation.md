---
title: 用于网络组件安装的组件和文件
description: 用于网络组件安装的组件和文件
keywords:
- 安装网络组件 WDK，使用的组件和文件
- 网络组件安装 WDK，使用的组件和文件
- 组件 WDK 网络安装
- 类安装程序 WDK 网络
- 共同安装程序 WDK 网络
- 网络迁移 DLL WDK
- 文本模式设置 WDK 网络
- 驱动程序图像文件 WDK 网络
- 驱动程序库文件 WDK 网络
- 迁移 DLL WDK 网络
- 供应商提供的安装文件 WDK 网络
- 文件 WDK 网络组件安装
ms.date: 01/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: b4e76b47c39613661d24bdecc05a25216603a033
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823035"
---
# <a name="components-and-files-used-for-network-component-installation"></a>用于网络组件安装的组件和文件

以下组件和文件用于安装网络驱动程序：

-    (INF) 文件的一个或多个信息

-   必需的类安装程序和微型端口驱动程序的可选共同安装程序

-   协议和筛选器驱动程序的 INetCfg

-   可选通知对象

除了上述一个或多个组件，供应商还可以选择提供以下文件：

-   一个或多个设备驱动程序映像 ( .sys) 文件和驱动程序库 ( .dll) 文件

-   驱动程序目录文件

-   文本模式安装信息文件 (txtsetup.oem) 

## <a name="inf-files"></a>INF 文件

每个网络组件必须具有网络类安装程序用于安装组件的 (INF) 文件的信息。 网络 INF 文件基于常见 INF 文件格式。 有关 INF 文件格式的详细信息，请参阅 [Inf 文件部分和指令](../install/index.md)。

有关为网络组件创建 INF 文件的详细信息，请参阅 [创建网络 INF 文件](creating-network-inf-files.md)。

## <a name="inetcfg"></a>INetCfg

目前，NDIS 协议和筛选器驱动程序通过调用 `INetCfg` [网络配置接口](/previous-versions/windows/hardware/network/ff559080(v=vs.85))系列来安装。 例如，若要安装或删除网络组件，驱动程序编写器将调用 [INetCfgClassSetup](/previous-versions/windows/hardware/network/ff547709(v=vs.85)) 接口。 

驱动程序编写器可以以编程方式调入此接口，也可以使用 [netcfg.exe](/windows-server/administration/windows-commands/netcfg)，它 `INetCfg` 代表它们调用。

有关协议驱动程序安装的详细信息，请参阅 [NDIS 协议驱动程序安装](ndis-protocol-driver-installation.md)。

有关筛选器驱动程序安装的详细信息，请参阅 [NDIS 筛选器驱动程序安装](ndis-filter-driver-installation.md)。

## <a name="notify-object"></a>通知对象

软件组件（如网络协议、客户端或服务）可以具有 " *通知" 对象*。 "通知" 对象可以显示用户界面，通知绑定事件的组件，以便组件可以对绑定过程执行一些控制，并有条件地安装或删除软件组件。 有关通知对象的详细信息，请参阅 [为网络组件通知对象](notify-objects-for-network-components.md)。

网络适配器不能有 "通知" 对象。 它可以具有共同安装程序。 有关共同安装程序的详细信息，请参阅 [编写共同安装程序](../install/writing-a-co-installer.md)。

## <a name="vendor-supplied-files"></a>供应商提供的文件

供应商为设备提供一个或多个驱动程序，该驱动程序通常由 ( .sys) 文件的驱动程序映像和驱动程序库 ( .dll) 文件组成。 供应商还可以提供可选的驱动程序 *目录文件*。 供应商通过将其驱动程序包提交给 Windows 硬件质量实验室 (WHQL) 进行测试和签名，来获取数字签名。 WHQL 返回 ( 的目录) 文件的包。 供应商必须在 INF 文件中列出设备的目录文件。

可选的文本模式安装信息文件 (txtsetup.oem) 也可能由供应商提供。 如果需要网络设备来启动计算机，则设备的驱动程序或驱动程序必须包含在操作系统工具包中，否则此类设备的供应商必须提供 txtsetup.oem 文件。 Txtsetup.oem 文件包含系统安装组件在文本模式安装过程中安装设备所使用的信息。

 

