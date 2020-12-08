---
title: 安装文件系统筛选器驱动程序
description: 安装文件系统筛选器驱动程序
keywords:
- 筛选器驱动程序 WDK 文件系统，安装
- 文件系统筛选器驱动程序 WDK，安装
- INF 文件系统
- INF 文件系统筛选器驱动程序安装的文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be03f0bbd590b39a4b19c492d320d8eecbba6c50
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834569"
---
# <a name="installing-a-file-system-filter-driver"></a>安装文件系统筛选器驱动程序


## <span id="ddk_installing_a_file_system_filter_driver_if"></span><span id="DDK_INSTALLING_A_FILE_SYSTEM_FILTER_DRIVER_IF"></span>


对于 Microsoft Windows XP 和更高版本的操作系统，应使用 INF 文件和安装应用程序安装文件系统筛选器驱动程序。  (在 Windows 2000 和更早版本的操作系统上，筛选器驱动程序通常由服务控制管理器安装。 ) 

将来，基于 INF 的安装应符合文件系统筛选器驱动程序的 Windows 硬件认证包要求。 请注意，"基于 INF 的安装" 表示只需使用 INF 文件复制文件并将信息存储在注册表中。 你不需要仅使用 INF 文件来安装整个产品，并且你将不需要为你的驱动程序提供 ["右键单击安装"](using-an-inf-file-to-install-a-file-system-filter-driver.md) 选项。

本节包括：

[为文件系统筛选器驱动程序创建 INF 文件](creating-an-inf-file-for-a-file-system-filter-driver.md)

[文件系统筛选器驱动程序的加载顺序组](load-order-groups-for-file-system-filter-drivers.md)

[文件系统筛选器驱动程序类和类 Guid](file-system-filter-driver-classes-and-class-guids.md)

[使用 INF 文件安装文件系统筛选器驱动程序](using-an-inf-file-to-install-a-file-system-filter-driver.md)

[使用 INF 文件卸载文件系统筛选器驱动程序](using-an-inf-file-to-uninstall-a-file-system-filter-driver.md)

 

 




