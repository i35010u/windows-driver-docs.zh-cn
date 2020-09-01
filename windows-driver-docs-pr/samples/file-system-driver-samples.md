---
title: 文件系统驱动程序示例
description: 此目录中的驱动程序示例提供了为设备编写自定义文件系统驱动程序的起点。
ms.assetid: 9F2F995E-EA20-4877-B96C-5FF082CE886D
ms.date: 11/15/2019
ms.localizationpriority: medium
ms.openlocfilehash: 1062ffd2677864add9e43aec2b4fa92f62bf2f34
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187273"
---
# <a name="file-system-driver-samples"></a>文件系统驱动程序示例

此目录中的驱动程序示例提供了为设备编写自定义文件系统驱动程序的起点。

| 示例 | 说明 |
| --- | --- |
| [CDFS 文件系统驱动程序](/samples/microsoft/windows-driver-samples/cdfs-file-system-driver) | Cd-rom 文件系统驱动程序 (cdfs) 示例是可移动媒体的文件系统驱动程序。 |
| [fastfat 文件系统驱动程序](/samples/microsoft/windows-driver-samples/fastfat-file-system-driver) | 基于 Windows 收件箱 FastFAT 文件系统的文件系统驱动程序，用作新文件系统的模型。 |
| [AvScan 文件系统微筛选器驱动程序](/samples/microsoft/windows-driver-samples/avscan-file-system-minifilter-driver) | 此筛选器是一个用于检查文件中数据的事务识别文件扫描程序。 防病毒软件可能以这种方式运行。 |
| [CancelSafe 文件系统微筛选器驱动程序](/samples/microsoft/windows-driver-samples/cancelsafe-file-system-minifilter-driver) | 演示如何使用取消安全队列的微筛选器。 |
| [CDO 文件系统微筛选器驱动程序](/samples/microsoft/windows-driver-samples/cdo-file-system-minifilter-driver) | 使用控制设备对象 (CDO) 与微筛选器结合使用的示例。 |
| [更改文件系统微筛选器驱动程序](/samples/microsoft/windows-driver-samples/change-file-system-minifilter-driver) | 监视文件更改的实时事务筛选器。 |
| [Ctx 文件系统微筛选器驱动器](/samples/microsoft/windows-driver-samples/ctx-file-system-minifilter-drive) | 演示如何在微筛选器中将上下文附加到实例、文件、流和流句柄。 |
| [删除文件系统微筛选器驱动程序](/samples/microsoft/windows-driver-samples/delete-file-system-minifilter-driver) | 演示如何检测文件或流的删除。 |
[元数据管理器文件系统微筛选器驱动程序](/samples/microsoft/windows-driver-samples/metadata-manager-file-system-minifilter-driver) | 作为一个示例，说明如何使用文件来存储与 minifilters 相对应的元数据。 此示例的实现描述了可能需要阻止对文件进行修改的情况，或者可能需要微筛选器暂时关闭文件。 |
| [Minispy 文件系统微筛选器驱动程序](/samples/microsoft/windows-driver-samples/minispy-file-system-minifilter-driver) | 用于监视和记录系统中发生的任何 i/o 和事务活动的工具。 |
| [NameChanger 文件系统微筛选器驱动程序](/samples/microsoft/windows-driver-samples/namechanger-file-system-minifilter-driver) | 使用映射将目录从卷命名空间的一个部分 Grafts 到另一部分。 微筛选器通过充当名称提供程序来维护这种错觉，将条目注入到目录枚举和转发目录更改通知。 |
| [NullFilter 文件系统微筛选器驱动程序](/samples/microsoft/windows-driver-samples/nullfilter-file-system-minifilter-driver) | 仅演示使用筛选器管理器注册的微筛选器。 |
| [传递文件系统微筛选器驱动程序](/samples/microsoft/windows-driver-samples/passthrough-file-system-minifilter-driver) | 演示如何为不同类型的 i/o 请求指定回调函数。 |
| [扫描仪文件系统微筛选器驱动程序](/samples/microsoft/windows-driver-samples/scanner-file-system-minifilter-driver) | 文件数据扫描程序示例。 通常，防病毒筛选器属于这种类型。 |
| [SimRep 文件系统微筛选器驱动程序](/samples/microsoft/windows-driver-samples/simrep-file-system-minifilter-driver) | 演示文件系统筛选器如何模拟文件系统（如重新分析点行为），以将打开的文件重定向到备用路径。 |
[SwapBuffer 文件系统微筛选器驱动程序](/samples/microsoft/windows-driver-samples/swapbuffer-file-system-minifilter-driver) | 演示如何在数据的读取和写入之间切换缓冲区。 此方法对于加密筛选器特别有用。 |