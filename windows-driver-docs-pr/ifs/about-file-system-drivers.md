---
title: 关于文件系统驱动程序
description: 关于文件系统驱动程序
ms.assetid: a64d83c6-d4cd-432d-bc1a-a3ff4656527c
keywords:
- 驱动程序 WDK 文件系统
- 文件系统驱动程序 WDK
ms.date: 10/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: 46e5ab1dec5eb2a29edfa69a21438d24f8e19b2f
ms.sourcegitcommit: 2a1c24db881ed843498001493c3ce202c9aa03f1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/16/2019
ms.locfileid: "74135167"
---
# <a name="about-file-system-drivers"></a>关于文件系统驱动程序

几乎在所有情况下，都不需要开发完整的文件系统驱动程序。 如果决定开发新的文件系统驱动程序，请执行以下操作：

- [ *Fastfat*示例](https://docs.microsoft.com/windows-hardware/drivers/samples/file-system-driver-samples)可用于作为模型。

- 若要了解如何创建和安装文件系统驱动程序，请参阅[创建文件系统驱动程序的 INF 文件](creating-an0inf-file-for-a-file-system-driver.md)。

WDK 并不提供用于文件系统开发的概念文档。

Windows 上与文件系统相关的大多数开发都涉及到创建[文件系统微筛选器驱动程序](file-system-minifilter-drivers.md)。
