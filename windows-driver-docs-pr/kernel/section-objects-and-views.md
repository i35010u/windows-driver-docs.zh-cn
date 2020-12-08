---
title: 节对象和视图
description: 节对象和视图
keywords:
- 内存管理 WDK 内核，节对象
- 内存管理 WDK 内核，共享内存
- 共享内存 WDK 内核
- 节对象 WDK 内核
- 内存段 WDK 内核
- 共享内存地址空间
- 查看 WDK 内存部分
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 545f2bca53afbe917fc2dde685a0e1188803fe12
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836908"
---
# <a name="section-objects-and-views"></a>节对象和视图





*Section 对象* 表示可以共享的内存部分。 进程可以使用 section 对象来共享部分内存地址空间 (内存部分与其他进程) 。 节对象还提供了一种机制，通过该机制，进程可以将文件映射到其内存地址空间。

每个内存部分都有一个或多个相应的 *视图*。 部分的视图是该部分的一部分，该部分实际上对某个进程可见。 为节创建视图的行为称为 " *映射* " 部分的视图。 处理节内容的每个进程都有其自己的视图;一个进程还可以有多个视图 () 的相同或不同的部分。

本节包含下列主题：

[基于文件和基于页文件的节](file-backed-and-page-file-backed-sections.md)

[管理内存节](managing-memory-sections.md)

[节对象和视图的安全问题](security-issues-for-section-objects-and-views.md)

 

 




