---
title: 文件系统驱动程序设计指南
description: 文件系统驱动程序设计指南
ms.assetid: 62DE75F7-0211-4173-AF45-84B2DDFDC95C
ms.date: 09/10/2020
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: c4d912e0e4568a756e56f755b3d6776d7213698f
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90104640"
---
# <a name="file-systems-driver-design-guide"></a>文件系统驱动程序设计指南

WDK 的这一部分提供与文件系统和筛选器驱动程序相关的概念信息。 有关说明驱动程序可以实现或调用的接口的参考页，请参阅[文件系统编程参考](/windows-hardware/drivers/ddi/_ifsk/)。

## <a name="file-systems"></a>文件系统

Windows 中的文件系统作为在存储系统上运行的文件系统驱动程序来实现。

Windows 中系统提供的每个文件系统旨在提供可靠的数据存储和不同的功能，目的是满足用户的要求。 Windows 中提供的标准文件系统包括 NTFS、ExFAT、UDF 和 FAT32。 [File System Functionality Comparison](/windows/desktop/FileIO/filesystem-functionality-comparison)（文件系统功能比较）中比较了这些文件系统中每个文件系统的功能。 此外，Windows Server 2012 及更高版本中提供的[复原文件系统](/windows-server/storage/refs/refs-overview) (ReFS) 提供了可缩放的大型卷支持以及检测和更正磁盘上的数据损坏的功能。

通常不需要开发新的文件系统驱动程序，也不能预测新文件系统驱动程序的要求/规格。 为此，此设计指南不涉及文件系统开发。 如果确实需要开发 Windows 中提供的驱动程序之外的新的文件系统驱动程序，可参考作为模型提供的示例代码。

## <a name="file-system-filter-drivers"></a>文件系统筛选器驱动程序

文件系统筛选器驱动程序可以截获发往某个文件系统或其他文件系统筛选器驱动程序的请求。 在请求到达其预期目标之前截获它，筛选器驱动程序就可以扩展或替换请求的原始目标提供的功能。 筛选器驱动程序的示例包括：

- 防病毒筛选器
- 备份代理
- 加密产品

筛选器驱动程序开发人员使用系统提供的[筛选器管理器](./filter-manager-concepts.md)，它提供一个框架来开发筛选器驱动程序，这样就无需管理文件 I/O 造成的所有复杂情况。 筛选器管理器简化了第三方筛选器驱动程序的开发，解决了旧版筛选器驱动程序模型的许多问题，例如能够通过分配的等级控制加载顺序。

## <a name="file-system-and-filter-sample-code"></a>文件系统和筛选器示例代码

现已提供许多 Windows 驱动程序示例，包括用于文件系统开发和文件系统筛选器驱动程序开发的示例。 有关完整列表，请参阅 [Windows 驱动程序示例](../samples/index.md)。

## <a name="file-system-filter-driver-certification"></a>文件系统筛选器驱动程序认证

有关文件系统和文件系统筛选器驱动程序的认证信息，请参阅 [Windows Hardware Lab Kit (HLK)](https://go.microsoft.com/fwlink/p/?LinkId=733613)。 有关文件系统和文件系统筛选器驱动程序的测试，请参阅 HCK 的 [Filter.Driver](/previous-versions/windows/hardware/hck/jj124779(v=vs.85)) 类别。

## <a name="additional-resources"></a>其他资源

除了本文档和上述示例代码，还有 [OSR](https://go.microsoft.com/fwlink/p/?linkid=50692) 提供各种用于文件系统筛选器开发的资源，包括研讨会和社区论坛（例如 NTFDS 论坛）。