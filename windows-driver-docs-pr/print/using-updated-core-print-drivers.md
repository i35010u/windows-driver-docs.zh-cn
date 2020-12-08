---
title: 使用更新的核心打印驱动程序
description: 使用更新的核心打印驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70a84197fb565753461af972607df09e5f4aaa80
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785957"
---
# <a name="using-updated-core-print-drivers"></a>使用更新的核心打印驱动程序


大多数制造商提供的打印驱动程序仅实现与设备相关的功能，它们依赖于系统提供的核心驱动程序组件来管理一般打印机功能。 UniDrv、PostScript 和 XPSDrv 是许多制造商提供的驱动程序所依赖的核心驱动程序组件示例，用于帮助进行打印机控制和配置。

通常情况下，打印机制造商不会在其打印驱动程序包中包含 Microsoft 的核心打印驱动程序。 相反，它们的驱动程序包中的 INF 文件仅调用 Microsoft 的打印机 INF 文件 Ntprint.inf，该文件将安装相应的核心打印驱动程序。

不过，Microsoft 会定期发布其核心打印驱动程序的更新版本，并且某些制造商可能会提供需要仅在更新版本中可用的功能的驱动程序包。 本部分介绍用所需的核心打印驱动程序版本安装的步骤。

### <a name="packages"></a>包

在 Windows Vista 和 Windows Server 2008 中，操作系统将所有打印驱动程序包都视为唯一对象。 操作系统将每个驱动程序包中的文件存储在 Windows 驱动程序存储区中的单独文件夹中。 Windows 打印机安装程序配置驱动程序包，使其独立于其他驱动程序包运行，并且每个驱动程序包都由操作系统单独管理。

Windows 将每个驱动程序包存储为一个完整的单位，并在单点和打印期间，整个驱动程序包将从打印服务器下载到客户端并安装。 可识别程序包的驱动程序与驱动程序包作为独立对象的管理兼容。 包感知打印驱动程序具有其 INF 文件中的 [条目](printer-inf-file-entries.md) ，以便启用点和打印操作，即使它们的包对包外的文件具有打印驱动程序依赖项也是如此。

### <a name="updates-in-windows-vista"></a>Windows Vista 中的更新

为了支持独立驱动程序包，并仍允许硬件制造商利用核心驱动程序组件，Windows Vista (和更高版本) 允许包感知驱动程序注册核心驱动程序包的依赖项。 Microsoft 只为 Windows Vista 中的打印机提供一个核心驱动程序包。 该程序包由驱动程序信息文件 Ntprint.inf 描述。 几乎所有制造商提供的打印机驱动程序（包括包感知驱动程序）都依赖于此核心驱动程序包。

Microsoft 会定期发布此核心驱动程序包的更新版本。 例如，Windows Vista 的 Service Pack 1 包括核心驱动程序包的更新版本。 某些制造商可能会发现他们需要利用这些更新，并且它们的驱动程序无法再依赖于初始 Windows Vista 版本中包含的核心驱动程序包版本。

本部分介绍如何构造与已更新的核心驱动程序文件有依赖关系的包感知驱动程序，以及如何确保在安装制造商提供的包感知驱动程序时安装更新的核心驱动程序包。

本文讨论了以下主题：

[使用更新的核心驱动程序构造包感知驱动程序](constructing-a-package-aware-driver-with-updated-core-drivers.md)

[更新非包感知驱动程序的核心驱动程序文件](updating-core-drivers-files-for-non-package-aware-drivers.md)

[创建适用于 Windows XP 和 Windows Vista 的单个驱动程序包](creating-a-single-driver-package-for-windows-xp-and-windows-vista.md)

 

 




