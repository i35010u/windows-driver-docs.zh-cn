---
title: 文件系统驱动程序设计指南
description: 文件系统驱动程序设计指南
ms.assetid: 62DE75F7-0211-4173-AF45-84B2DDFDC95C
ms.date: 10/16/2019
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: 7c01ccdb92c2c86959b5369b85e51dbbd64b7a49
ms.sourcegitcommit: 2a1c24db881ed843498001493c3ce202c9aa03f1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/16/2019
ms.locfileid: "74128471"
---
# <a name="file-systems-driver-design-guide"></a>文件系统驱动程序设计指南

WDK 的这一部分提供与文件系统和筛选器驱动程序（微筛选器）相关的概念信息。 有关说明驱动程序可以实现或调用的接口的参考页，请参阅[文件系统编程参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/_ifsk/)。

## <a name="file-systems"></a>文件系统

Windows 中的文件系统作为在存储系统上运行的文件系统驱动程序来实现。 Windows 中系统提供的每个文件系统旨在提供可靠的数据存储和不同的功能，目的是满足用户的要求。

Windows 中提供的标准文件系统包括 NTFS、ExFAT、UDF 和 FAT32。 [File System Functionality Comparison](https://docs.microsoft.com/windows/desktop/FileIO/filesystem-functionality-comparison)（文件系统功能比较）中比较了这些文件系统中每个文件系统的功能。 此外，Windows Server 2012 及更高版本中提供的[复原文件系统](https://docs.microsoft.com/windows-server/storage/refs/refs-overview) (ReFS) 提供了可缩放的大型卷支持以及检测和更正磁盘上的数据损坏的功能。

创建 Windows 中提供的文件系统驱动程序之外的新文件系统驱动程序很可能不必要，并且新文件系统驱动程序的要求/规范不可预测。 为此，此设计指南不涉及文件系统开发。 即使如此，[示例代码](#file-system-sample-code)也可用作编写新文件系统的模型。

## <a name="file-system-filter-driver-development"></a>文件系统筛选器驱动程序开发

文件系统筛选器驱动程序可以截获发往某个文件系统或其他文件系统筛选器驱动程序的请求。 在请求到达其预期目标之前截获它，筛选器驱动程序就可以扩展或替换请求的原始目标提供的功能。 筛选器驱动程序的示例包括：防病毒筛选器、备份代理和加密产品。

可以通过 Windows 中系统提供的[筛选器管理器](filter-manager-and-minifilter-driver-architecture.md)使用文件系统筛选服务。 筛选器管理器提供一个框架来开发筛选器驱动程序，这样就不需管理文件 I/O 所带来的所有复杂情况。 筛选器管理器简化了第三方筛选器驱动程序的开发，解决了旧版筛选器驱动程序模型的许多问题，例如能够通过分配的等级控制加载顺序。 针对筛选器管理器模型开发的筛选器驱动程序称为微筛选器。 每个微筛选器驱动程序都分配了一个等级，该等级是唯一标识符，决定了该微筛选器相当于 I/O 堆栈中其他微筛选器的加载位置。 等级由 Microsoft 分配和管理。

## <a name="file-system-sample-code"></a>文件系统示例代码

现已提供许多 Windows 驱动程序示例，包括用于文件系统开发和文件系统筛选器驱动程序开发的示例。 有关完整列表，请参阅 [Windows 驱动程序示例](https://docs.microsoft.com/windows-hardware/drivers/samples/)。

## <a name="file-system-filter-driver-certification"></a>文件系统筛选器驱动程序认证

有关文件系统和文件系统筛选器驱动程序的认证信息，请参阅 [Windows Hardware Lab Kit (HLK)](https://go.microsoft.com/fwlink/p/?LinkId=733613)。 有关文件系统和文件系统筛选器驱动程序的测试，请参阅 HCK 的 [Filter.Driver](https://docs.microsoft.com/previous-versions/windows/hardware/hck/jj124779(v=vs.85)) 类别。

## <a name="file-system-filter-driver-developer-resources"></a>文件系统筛选器驱动程序开发人员资源

除了上面提到的示例代码之外，还提供了以下附加资源：

- 若要请求 Microsoft 为你的微筛选器分配等级，请发送一封电子邮件，在其中提出相应要求。 请按[微筛选器等级请求](minifilter-altitude-request.md)中的说明提交请求。

- 若要获取使用重新分析点的筛选器驱动程序的 ID，请按[重新分析点请求](reparse-point-tag-request.md)中的步骤操作。

- [OSR](https://go.microsoft.com/fwlink/p/?linkid=50692) 提供各种用于文件系统微筛选器开发的资源，包括研讨会和社区论坛，例如 NTFDS 论坛。
