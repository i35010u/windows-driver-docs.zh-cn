---
title: 关于文件系统筛选器驱动程序
description: 关于文件系统筛选器驱动程序
ms.assetid: 4bff8ad6-624a-429d-b9ec-3f96c3c7c99d
keywords:
- 筛选器驱动程序 WDK 文件系统，关于文件系统筛选器驱动程序
- 文件系统筛选器驱动程序 WDK，关于文件系统筛选器驱动程序
- 什么是文件系统筛选器驱动程序
- 文件系统筛选器驱动程序不是设备驱动程序
ms.date: 02/10/2020
ms.localizationpriority: medium
ms.openlocfilehash: 5e7a7ec42d175f08d35ee9fa412884b231efcae8
ms.sourcegitcommit: 8c898615009705db7633649a51bef27a25d72b26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/07/2020
ms.locfileid: "78910518"
---
# <a name="about-file-system-filter-drivers"></a>关于文件系统筛选器驱动程序

## <a name="file-system-filter-drivers-on-windows"></a>Windows 上的文件系统筛选器驱动程序

*文件系统筛选器驱动程序*是一个可选的驱动程序，它将值添加到或修改文件系统的行为。 文件系统筛选器驱动程序是一个内核模式组件，作为 Windows executive 的一部分运行。

文件系统筛选器驱动程序可以对一个或多个文件系统或文件系统卷的 i/o 操作进行筛选。 根据驱动程序的性质，*筛选器*可以表示*日志*、*观察*、*修改*甚至*阻止*。 文件系统筛选器驱动程序的典型应用程序包括防病毒实用程序、加密程序和分层存储管理系统。

Windows 中有两种文件系统筛选器模型：

- 微筛选器[模型](https://docs.microsoft.com/windows-hardware/drivers/ifs/filter-manager-concepts)，其中微筛选器使用系统提供的筛选器管理器支持，从而简化了筛选器开发

- [旧文件系统筛选器模型](https://docs.microsoft.com/windows-hardware/drivers/ifs/about-file-system-legacy-filter-drivers)

> [!NOTE]
> 为了获得最佳的可靠性和性能，请使用带有筛选器管理器支持的[文件系统微筛选器驱动程序]((https://docs.microsoft.com/windows-hardware/drivers/ifs/filter-manager-concepts))，而不是使用旧的文件系统 若要将旧驱动程序移植到微筛选器驱动程序，请参阅[迁移旧筛选器驱动程序的准则](guidelines-for-porting-legacy-filter-drivers.md)。

## <a name="file-system-filter-drivers-are-not-device-drivers"></a>文件系统筛选器驱动程序不是设备驱动程序

*设备驱动程序*是控制特定硬件 i/o 设备的软件组件。 例如，DVD 存储驱动程序控制 DVD 驱动器。

与此相反，*文件系统筛选器驱动程序*与一个或多个文件系统配合使用来管理文件 i/o 操作。 这些操作包括：

- 创建、打开、关闭和枚举文件和目录

- 获取和设置文件、目录和卷信息

- 读取和写入文件数据

此外，文件系统筛选器驱动程序必须支持特定于文件系统的功能，如缓存、锁定、稀疏文件、磁盘配额、压缩、安全、可恢复性、重新分析点和卷装入点。

有关文件系统筛选器驱动程序和设备驱动程序之间的相似性和差异的详细信息，请参阅以下内容：

- [文件系统筛选器驱动程序与设备驱动程序的相似之处](how-file-system-filter-drivers-are-similar-to-device-drivers.md)

- [文件系统筛选器驱动程序与设备驱动程序有何不同](how-file-system-filter-drivers-are-different-from-device-drivers.md)