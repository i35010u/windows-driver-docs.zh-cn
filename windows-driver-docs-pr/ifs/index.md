---
title: 文件系统筛选器简介
description: Windows 中的文件系统作为在存储系统上运行的文件系统驱动程序来实现。
ms.assetid: 62DE75F7-0211-4173-AF45-84B2DDFDC95C
ms.date: 05/31/2019
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: 5ee23a2be327186b712afde367213e45178e5420
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841204"
---
# <a name="file-systems-driver-design-guide"></a>文件系统驱动程序设计指南

WDK 的这一部分提供与文件系统和筛选器驱动程序（微筛选器）相关的概念信息。 有关驱动程序可以实现或调用的编程接口的详细信息，请参阅[文件系统编程参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/_ifsk/)。

Windows 中的文件系统作为在存储系统上运行的文件系统驱动程序来实现。 Windows 中的每个文件系统旨在提供可靠的数据存储和不同的功能，目的是满足用户的要求。 [File System Functionality Comparison](https://docs.microsoft.com/windows/desktop/FileIO/filesystem-functionality-comparison)（文件系统功能比较）中比较了 Windows 中每个标准的文件系统的功能。 Windows Server 2012 的新增功能为 ReFS。 ReFS 是一个提供可缩放大型卷支持的文件系统，可以检测并修正磁盘上的数据损坏情况。

除了那些在 Windows 中提供的文件系统驱动程序，可能不需要创建新的文件系统驱动程序。 文件系统和文件系统筛选器驱动程序可以提供修改现有文件系统的操作所需的任何自定义行为。

## <a name="span-idfile_system_filter_driver_developmentspanspan-idfile_system_filter_driver_developmentspanspan-idfile_system_filter_driver_developmentspanfile-system-filter-driver-development"></a><span id="File_System_Filter_Driver_Development"></span><span id="file_system_filter_driver_development"></span><span id="FILE_SYSTEM_FILTER_DRIVER_DEVELOPMENT"></span>文件系统筛选器驱动程序开发

文件系统筛选器驱动程序可以截获发往某个文件系统或其他文件系统筛选器驱动程序的请求。 在请求到达其预期目标之前截获它，筛选器驱动程序就可以扩展或替换请求的原始目标提供的功能。 文件系统和文件系统筛选器驱动程序的示例包括：防病毒筛选器、备份代理和加密产品。

可以通过 Windows 中的[筛选器管理器](filter-manager-and-minifilter-driver-architecture.md)使用文件系统筛选服务。 筛选器管理器提供一个框架来开发文件系统和文件系统筛选器驱动程序，这样就不需管理文件 I/O 所带来的所有复杂情况。 筛选器管理器简化了第三方筛选器驱动程序的开发，解决了现有的旧版筛选器驱动程序模型的许多问题，例如能够通过分配的等级控制加载顺序。 针对筛选器管理器模型开发的筛选器驱动程序称为微筛选器。 每个微筛选器驱动程序都分配了一个等级，该等级是唯一标识符，决定了该微筛选器相当于 I/O 堆栈中其他微筛选器的加载位置。 等级由 Microsoft 分配和管理。

## <a name="span-idfile_system_filter_driver_certificationspanspan-idfile_system_filter_driver_certificationspanspan-idfile_system_filter_driver_certificationspanfile-system-filter-driver-certification"></a><span id="File_System_Filter_Driver_Certification"></span><span id="file_system_filter_driver_certification"></span><span id="FILE_SYSTEM_FILTER_DRIVER_CERTIFICATION"></span>文件系统筛选器驱动程序认证

有关文件系统和文件系统筛选器驱动程序的认证信息，请参阅 [Windows 硬件认证工具包 (HCK)](https://go.microsoft.com/fwlink/p/?LinkId=733613)。 有关文件系统和文件系统筛选器驱动程序的测试，请参阅 HCK 的 [Filter.Driver](https://docs.microsoft.com/previous-versions/windows/hardware/hck/jj124779(v=vs.85)) 类别。

## <a name="span-idfile_system_filter_driver_developer_resourcesspanspan-idfile_system_filter_driver_developer_resourcesspanspan-idfile_system_filter_driver_developer_resourcesspanfile-system-filter-driver-developer-resources"></a><span id="File_System_Filter_Driver_Developer_Resources"></span><span id="file_system_filter_driver_developer_resources"></span><span id="FILE_SYSTEM_FILTER_DRIVER_DEVELOPER_RESOURCES"></span>文件系统筛选器驱动程序开发人员资源

若要请求 Microsoft 为你的微筛选器分配等级，请发送一封电子邮件，在其中提出相应要求。 请按[微筛选器等级请求](minifilter-altitude-request.md)中的说明提交请求。

若要获取使用重新分析点的筛选器驱动程序的 ID，请按[重新分析点请求](reparse-point-tag-request.md)中的步骤操作。

可以订阅 NTFSD 新闻组，详细了解如何开发文件系统和筛选器驱动程序。 可以在 [NT 文件系统驱动程序新网组](https://go.microsoft.com/fwlink/p/?LinkId=620898)中找到该组。

OSR 的“开发 Windows 文件系统”讲座探讨了如何开发文件系统以及文件系统和文件系统筛选器驱动程序。 请参阅 [IFS 开发人员培训](https://go.microsoft.com/fwlink/p/?linkid=50692)。
