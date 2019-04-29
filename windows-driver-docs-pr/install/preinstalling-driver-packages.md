---
title: 预安装驱动程序包
description: 预安装驱动程序包
ms.assetid: aba794ac-ab24-486a-9f5a-7e8435056bb7
keywords:
- 安装应用程序 WDK，预安装的驱动程序包
- 设备安装应用程序 WDK，预安装的驱动程序包
- 预安装驱动程序 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2bab22ad61f4e685d8ed73d7fe3fc6ef6380add9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325753"
---
# <a name="preinstalling-driver-packages"></a>预安装驱动程序包





若要预安装的驱动程序文件，你*设备安装应用程序*应遵循以下步骤：

1.  在目标系统上，创建驱动程序文件的目录。 如果设备安装应用程序安装应用程序，驱动程序文件应存储在应用程序目录的子目录。

2.  中的所有文件都复制[驱动程序包](driver-packages.md)从分发介质到在步骤 (1) 中创建的目录。 驱动程序包包括驱动程序或驱动程序、 INF 文件、 目录文件和其他安装文件。

3.  调用[SetupCopyOEMInf](https://go.microsoft.com/fwlink/p/?linkid=98735)步骤 (1) 中创建的目录中指定的 INF 文件。 指定为 SPOST_PATH *OEMSourceMediaType*参数并指定**NULL**有关*OEMSourceMediaLocation*参数。 [SetupCopyOEMInf](https://go.microsoft.com/fwlink/p/?linkid=194252)将复制到驱动程序包的 INF 文件 *%systemroot%\\Inf*目录在目标系统上并指示 Windows 在其列表中存储的 INF 文件的源位置预处理过的 INF 文件。 [SetupCopyOEMInf](https://go.microsoft.com/fwlink/p/?linkid=194252)还处理目录文件，因此 PnP 管理器将它识别设备 INF 文件中列出了下一次安装驱动程序。

PnP 管理器时用户插入设备，可以识别该设备，将查找由复制的 INF 文件[SetupCopyOEMInf](https://go.microsoft.com/fwlink/p/?linkid=194252)，并将安装在步骤 (2) 中复制的驱动程序。 (有关复制 INF 文件的详细信息，请参阅[复制 Inf](copying-inf-files.md)。)

 

 





