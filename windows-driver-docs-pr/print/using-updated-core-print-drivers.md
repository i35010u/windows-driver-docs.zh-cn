---
title: 使用更新的核心打印驱动程序
description: 使用更新的核心打印驱动程序
ms.assetid: a2a31627-a453-4776-b4f2-13660e4ad7a3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 43b2eb2a60a0f7fbd989a02a1a4393c3fabd3e63
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376455"
---
# <a name="using-updated-core-print-drivers"></a>使用更新的核心打印驱动程序


大多数制造商提供的打印驱动程序实现仅依赖于设备的函数，并且它们依赖于系统提供的核心驱动程序组件来管理通用打印机功能。 UniDrv、 PostScript 和 XPSDrv 打印机控制与配置的帮助许多制造商提供的驱动程序依赖的核心驱动程序组件的示例。

通常情况下，打印机制造商不包括在其打印驱动程序包中 Microsoft 的核心打印驱动程序。 相反，其驱动程序包中的 INF 文件只需调用 Microsoft 的打印机 INF 文件，Ntprint.inf，安装适当的核心打印驱动程序。

但是，Microsoft 定期发布更新的版本的其核心打印驱动程序，并且某些制造商可能提供需要仅在更新版本中可用的功能的驱动程序包。 本部分介绍用于安装所需的核心打印驱动程序版本的步骤。

### <a name="packages"></a>包

在 Windows Vista 和 Windows Server 2008 中，操作系统的打印驱动程序的所有包都视为唯一对象。 操作系统将每个驱动程序包中的文件存储在 Windows 驱动程序存储区中的单独文件夹中。 Windows 打印机安装程序配置的驱动程序包的其他驱动程序包，独立运行，并由操作系统单独管理每个驱动程序包。

Windows 存储作为一个完整的单元，每个驱动程序包，并从打印服务器下载到客户端和安装整个驱动程序包在指向并打印，过程。 识别包的驱动程序适用于管理驱动程序程序包作为独立的对象。 识别包的打印驱动程序具有[条目](printer-inf-file-entries.md)INF 文件要启用点--打印操作，即使其程序包依赖项的打印驱动程序软件包外部的文件中。

### <a name="updates-in-windows-vista"></a>Windows Vista 中的更新

若要支持独立的驱动程序包，并仍允许硬件制造商可以利用核心驱动程序组件，Windows Vista （和更高版本） 允许识别包的驱动程序即可注册核心驱动程序包依赖项。 Microsoft 提供了 Windows Vista 中的打印机的只有一个核心驱动程序包。 该程序包由驱动程序信息文件 Ntprint.inf 描述。 几乎所有制造商提供打印驱动程序，包括识别包的驱动程序，都依赖于此核心驱动程序包。

定期，Microsoft 发布更新版本的此核心驱动程序包。 例如，适用于 Windows Vista Service Pack 1 包括核心驱动程序包的更新的版本。 某些制造商可能会发现他们需要利用这些更新，并且其驱动程序可以不再依赖于在初始 Windows Vista 版本中包含的核心驱动程序包的版本。

本部分介绍如何构造具有更新的核心驱动程序文件依赖项包识别驱动程序以及如何确保安装的制造商提供的包识别驱动程序时，安装了更新的核心驱动程序包。

论述了以下主题：

[构造一个识别包的驱动程序与更新的核心驱动程序](constructing-a-package-aware-driver-with-updated-core-drivers.md)

[不识别包的驱动程序更新核心驱动程序文件](updating-core-drivers-files-for-non-package-aware-drivers.md)

[创建一个驱动程序包的 Windows XP 和 Windows Vista](creating-a-single-driver-package-for-windows-xp-and-windows-vista.md)

 

 




