---
title: 预安装驱动程序包
description: 预安装驱动程序包
keywords:
- 安装应用程序 WDK，预安装驱动程序包
- 设备安装应用程序 WDK，预安装驱动程序包
- 预安装的驱动程序 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b56a117b31e10c61c69e7d9dd5df9aff65448482
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796055"
---
# <a name="preinstalling-driver-packages"></a>预安装驱动程序包





若要预安装驱动程序文件， *设备安装应用程序* 应遵循以下步骤：

1.  在目标系统上，为驱动程序文件创建一个目录。 如果设备安装应用程序安装了应用程序，则驱动程序文件应存储在应用程序目录的子目录中。

2.  将 [驱动程序包](driver-packages.md) 中的所有文件从分发媒体复制到步骤 (1) 中创建的目录。 驱动程序包包括驱动程序、驱动程序、INF 文件、目录文件以及其他安装文件。

3.  调用 [SetupCopyOEMInf](/windows/win32/api/setupapi/nf-setupapi-setupcopyoeminfa) ，并在步骤 (1) 中创建的目录中指定 INF 文件。 指定 *OEMSourceMediaType* 参数 SPOST_PATH，并将 *OEMSourceMediaLocation* 参数指定为 **NULL** 。 [SetupCopyOEMInf](/windows/win32/api/setupapi/nf-setupapi-setupcopyoeminfa) 将驱动程序包的 INF 文件复制到目标系统上的 *% SystemRoot% \\ INF* 目录中，并指示 Windows 将 inf 文件的源位置存储在它的预处理 inf 文件列表中。 [SetupCopyOEMInf](/windows/win32/api/setupapi/nf-setupapi-setupcopyoeminfa) 还会处理编录文件，因此 PnP 管理器会在下次识别 INF 文件中列出的设备时安装该驱动程序。

当用户插入设备时，PnP 管理器会识别设备，查找 [SetupCopyOEMInf](/windows/win32/api/setupapi/nf-setupapi-setupcopyoeminfa)复制的 INF 文件，并安装在步骤 (2) 中复制的驱动程序。  (有关复制 INF 文件的详细信息，请参阅 [复制 inf](copying-inf-files.md)。 ) 

 

