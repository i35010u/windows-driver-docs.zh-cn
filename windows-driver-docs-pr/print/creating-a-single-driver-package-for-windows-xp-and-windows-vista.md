---
title: 创建适用于 Windows XP 和 Windows Vista 的单个驱动程序包
description: 创建适用于 Windows XP 和 Windows Vista 的单个驱动程序包
ms.assetid: 5e350152-edd7-4afb-bcba-dd0217d0d17a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3fdff81e035e29f5dd0a74ddae95e746a1e66040
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91734513"
---
# <a name="creating-a-single-driver-package-for-windows-xp-and-windows-vista"></a>创建适用于 Windows XP 和 Windows Vista 的单个驱动程序包


Microsoft [Connect](/collaborate/connect-redirect) 网站提供了两组核心驱动程序更新：

-   对于早于 Windows Vista 的 Windows 操作系统 (包括 Windows Server 2003、Windows XP 和 Windows 2000) ，一组可再发行更新允许硬件制造商合并支持这些操作系统所需的特定文件。

-   对于 Windows Vista 和更高版本，单独的包允许硬件制造商提供最新的核心驱动程序包。

若要在同一驱动程序包中同时支持 Windows Vista) 和 Windows Vista 及更高版本操作系统中的 Windows XP (和其他 Windows 操作系统，硬件制造商必须使用相应的可再发行组件包，并相应地构造其 INF。

### <a name="no-redistributable-package"></a>无可再发行包

如果你的驱动程序适用于核心驱动程序组件的 Windows XP 和 Windows Vista 版本 (也就是说，如果不需要重新发布核心驱动程序) ，请执行以下步骤：

1.  继续在 Windows Vista 上使用 Windows XP 驱动程序。 不需要进行任何更改。

2.  对于 Windows Vista Premium 徽标认证，为 windows XP (和 windows vista 之前的其他 Windows 操作系统) 和 Windows Vista 及更高版本的操作系统）提供单独的 INF 安装部分，并为 Windows Vista 程序包识别 INF 安装部分。

### <a name="redistributable-package-for-windows-operating-systems-earlier-than-windows-vista"></a><a href="" id="redistributable-package-for-windows-operating-systems-earlier-than-win"></a> 早于 Windows Vista 的 Windows 操作系统的可再发行组件包

如果你的驱动程序适用于 windows Vista 初始版本，但你需要在 Windows XP 和更早的操作系统上使用 Windows Vista 版本的核心驱动程序组件 (也就是说，如果需要) 之前 windows Vista 之前的 Windows 操作系统的重新分发功能，请执行以下步骤：

1.  为 windows XP (和 windows) Vista 之前的其他 Windows 操作系统（对于 Windows vista (和更高) 版本）创建单独的 INF 安装部分。

2.  使用 INF **CoreDriverDependencies** 和 **COREDRIVERSECTIONS** 指令强制 Inf 文件的 Windows Vista 部分使用收件箱核心驱动程序包。

3.  确定 windows Vista 之前的 Windows 操作系统的重新分发包中的文件，这些文件需要支持这些操作系统版本。

4.  为驱动程序包中的下层支持包含所需的二进制文件，并且仅复制它们以便在早于 Windows Vista 的 Windows 操作系统上安装。

### <a name="windows-vista-redistributable-package"></a>Windows Vista 可再发行组件包

如果你的驱动程序需要核心驱动程序包的更新版本才能在 windows Vista 初始版本和 Windows XP 上正常运行 (也就是说，如果需要重新分发到 Windows Vista) ，请执行以下步骤：

1.  为 windows XP (和 windows) Vista 之前的其他 Windows 操作系统（对于 Windows Vista 和更高版本）创建单独的 INF 安装部分。

2.  将整个 Windows Vista 核心驱动程序包添加到驱动程序包的子目录中。

3.  使用 [**INF CopyINF 指令**](../install/inf-copyinf-directive.md) 将更新的核心驱动程序预加载到驱动程序存储区中。

4.  使用**InboxVersionRequired** = * &lt; 已更新核心驱动程序 &gt; *指令的 INF InboxVersionRequired 版本，以确保仅使用较新版本的核心驱动程序包。

5.  使用 INF **CoreDriverDependencies** 和 **CoreDriverSections** 指令指明 Windows Vista 驱动程序需要更新的核心驱动程序。

6.  在 windows Vista 之前的 Windows 操作系统的安装部分中，将所需的文件直接复制到包含的核心驱动程序包中，就像它们是驱动程序的一部分一样。

