---
title: 文件系统筛选器驱动程序不是设备驱动程序
description: 文件系统筛选器驱动程序不是设备驱动程序
ms.assetid: 4a1b2470-0062-4241-952d-ea9351b1a2f9
keywords:
- 筛选器驱动程序 WDK 文件系统，与设备驱动程序
- 文件系统筛选器驱动程序 WDK，与设备驱动程序
- 设备驱动程序 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a2c42aa75aa10d6ccd743c512ab54219e4a69e9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523133"
---
# <a name="file-system-filter-drivers-are-not-device-drivers"></a>文件系统筛选器驱动程序不是设备驱动程序


## <span id="ddk_a_file_system_filter_driver_is_not_a_device_driver_if"></span><span id="DDK_A_FILE_SYSTEM_FILTER_DRIVER_IS_NOT_A_DEVICE_DRIVER_IF"></span>


一个*设备驱动程序*是一个软件组件，用于控制特定硬件 I/O 设备。 例如，DVD 存储驱动程序控制的 DVD 驱动器。

与此相反，文件系统筛选器驱动程序工作原理与一个或多个文件系统来管理文件 I/O 操作结合使用。 这些操作包括创建、 打开、 关闭和枚举文件和目录;获取和设置的文件、 目录和卷信息;和读取和写入文件数据。 此外，文件系统筛选器驱动程序必须支持文件特定于系统的功能，例如缓存、 锁定、 稀疏文件、 磁盘配额、 压缩、 安全性、 可恢复性，重新分析点和卷装入点。

相似之处和文件系统筛选器驱动程序和设备驱动程序之间的差异的详细信息，请参阅：

[文件系统筛选器驱动程序的方式类似于设备驱动程序](how-file-system-filter-drivers-are-similar-to-device-drivers.md)

[有何不同的设备驱动程序从文件系统筛选器驱动程序](how-file-system-filter-drivers-are-different-from-device-drivers.md)

 

 




