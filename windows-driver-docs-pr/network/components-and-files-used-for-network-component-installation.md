---
title: 用于网络组件安装的组件和文件
description: 用于网络组件安装的组件和文件
ms.assetid: be056ff1-0b92-4e81-a506-7750012aad4e
keywords:
- 安装网络组件 WDK、 组件和使用的文件
- 网络组件安装 WDK、 组件和使用的文件
- 组件 WDK 网络安装
- 类安装程序 WDK 网络
- 共同安装程序 WDK 网络
- 网络迁移 DLL WDK
- 文本模式下安装 WDK 网络
- 驱动程序图像文件 WDK 网络
- 驱动程序库文件 WDK 网络
- 迁移 DLL WDK 网络
- 供应商提供的安装文件 WDK 网络
- 文件 WDK 网络组件安装
ms.date: 01/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: 2b3c4163ad8b7bb88193f737b08bd499225b1a37
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344239"
---
# <a name="components-and-files-used-for-network-component-installation"></a>用于网络组件安装的组件和文件

以下组件和文件用于安装的网络驱动程序：

-   一个或多个信息 (INF) 文件

-   安装程序所需的类和微型端口驱动程序的可选共同安装程序

-   协议和筛选器驱动程序的 INetCfg

-   可选的通知对象

除了一个或多个以上的组件，供应商还选择提供以下文件：

-   一个或多个设备驱动程序 (.sys) 图像文件和驱动程序库 (.dll) 文件

-   驱动程序目录文件

-   文本模式下安装信息文件 (txtsetup.oem)

## <a name="inf-files"></a>INF 文件

每个网络组件必须具有网络类安装程序用于安装该组件的信息 (INF) 文件。 网络 INF 文件基于通用 INF 文件格式。 有关 INF 文件格式的详细信息，请参阅[INF 文件的部分和指令](https://msdn.microsoft.com/library/windows/hardware/ff547433)。

有关创建网络组件的 INF 文件的详细信息，请参阅[创建网络 INF 文件](creating-network-inf-files.md)。

## <a name="inetcfg"></a>INetCfg

目前，通过调入安装 NDIS 协议和筛选器驱动程序`INetCfg`系列[网络配置接口](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff559080(v%3dvs.85))。 例如，若要安装或删除网络组件，驱动程序编写器调用到[INetCfgClassSetup](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547709%28v%3dvs.85%29)接口。 

驱动程序编写人员可以通过调用到此接口以编程方式或者他们可以使用[netcfg.exe](https://docs.microsoft.com/windows-server/administration/windows-commands/netcfg)，它调用`INetCfg`代表这些设备。

有关协议驱动程序安装的详细信息，请参阅[NDIS 协议驱动程序安装](ndis-protocol-driver-installation.md)。

有关筛选器驱动程序安装的详细信息，请参阅[NDIS 筛选器驱动程序安装](ndis-filter-driver-installation.md)。

## <a name="notify-object"></a>通知对象

软件组件，如网络协议、 客户端或服务，可以具有*通知对象*。 通知对象可以显示用户界面，通知绑定事件，以便该组件可以执行绑定进程的某些控制和有条件地安装或删除软件组件的组件。 有关详细信息通知对象，请参阅[通知网络组件的对象](notify-objects-for-network-components.md)。

网络适配器不能具有通知对象。 它可以具有共同安装程序。 有关共同安装程序的详细信息，请参阅[编写共同安装程序](https://msdn.microsoft.com/library/windows/hardware/ff554011)。

## <a name="vendor-supplied-files"></a>供应商提供的文件

供应商提供了一个或多个设备，通常包含的驱动程序 (.sys) 图像文件和驱动程序库 (.dll) 文件的驱动程序。 供应商还可以提供可选驱动程序*编录文件*。 供应商提交其驱动程序包向 Windows 硬件质量实验室 (WHQL) 测试和签名获取数字签名。 WHQL 返回包目录 (.cat) 文件。 供应商必须列出该设备的 INF 文件中的目录文件。

可选的文本模式下安装信息文件 (txtsetup.oem) 也可能由供应商提供。 如果网络设备需要来启动计算机，该驱动程序或设备驱动程序必须包括在操作系统工具包或此类设备的供应商必须提供 txtsetup.oem 文件。 Txtsetup.oem 文件包含系统安装程序组件用于在文本模式下安装期间安装该设备的信息。

 

 





