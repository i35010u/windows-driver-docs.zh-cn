---
title: 安装文件系统驱动程序
description: 安装文件系统驱动程序
ms.assetid: 1297b565-ac85-4248-927a-ab91b6cb3ab0
keywords:
- 驱动程序 WDK 文件系统，安装
- 文件系统驱动程序 WDK，安装
- INF 文件 WDK 文件系统
- INF 文件 WDK 文件系统，有关文件系统驱动程序安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a055607d6e59246990408ab44806b15fd0af4606
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370127"
---
# <a name="installing-a-file-system-driver"></a>安装文件系统驱动程序


## <span id="ddk_installing_a_file_system_filter_driver_if"></span><span id="DDK_INSTALLING_A_FILE_SYSTEM_FILTER_DRIVER_IF"></span>


对于 Microsoft Windows XP 和更高版本操作系统，应使用 INF 文件和安装应用程序来安装文件系统驱动程序。 （在 Microsoft Windows 2000 和更早的操作系统，文件系统驱动程序通常安装的服务控制管理器。）

将来，基于 INF 的安装应满足 Windows 硬件认证工具包要求文件系统驱动程序。 请注意，"基于 INF 的安装"仅意味着需要使用 INF 文件以将文件复制并存储在注册表中的信息。 您不需要在使用仅的 INF 文件，请安装整个产品和你不将需要提供["右键单击安装"](using-an-inf-file-to-install-a-file-system-filter-driver.md)您的驱动程序的选项。

本部分包括：

[创建文件系统驱动程序 INF 文件](creating-an-inf-file-for-a-file-system-driver.md)

中的以下节[文件系统筛选器驱动程序](file-system-filter-drivers.md)部分有关安装和卸载文件系统筛选器驱动程序也是适用于文件系统驱动程序。

[使用 INF 文件来安装文件系统筛选器驱动程序](using-an-inf-file-to-install-a-file-system-filter-driver.md)

[使用 INF 文件卸载文件系统筛选器驱动程序](using-an-inf-file-to-uninstall-a-file-system-filter-driver.md)

 

 




