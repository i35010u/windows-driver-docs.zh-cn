---
title: 文件系统示例代码
description: 文件系统示例代码
ms.assetid: a64d83c6-d4cd-432d-bc1a-a3ff4656527c
keywords:
- 驱动程序 WDK 文件系统
- 文件系统驱动程序 WDK
ms.date: 02/10/2020
ms.localizationpriority: medium
ms.openlocfilehash: f87a87824ae52df1099286ecad430feed482ce81
ms.sourcegitcommit: 8c898615009705db7633649a51bef27a25d72b26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/07/2020
ms.locfileid: "78910530"
---
# <a name="file-system-sample-code"></a>文件系统示例代码

几乎在所有情况下，都不需要为 Windows 开发完整的文件系统驱动程序。 如果决定开发新的文件系统驱动程序，则可以使用[ *fastfat*示例](https://docs.microsoft.com/windows-hardware/drivers/samples/file-system-driver-samples)作为模型。 若要了解如何安装文件系统驱动程序，请参阅[创建文件系统驱动程序的 INF 文件](creating-an-inf-file-for-a-file-system-driver.md)。

WDK 并不提供用于文件系统开发的概念文档。

Windows 上与文件系统相关的大多数开发涉及到创建与系统提供的[筛选器管理](filter-manager-concepts.md)器交互的文件系统筛选器（或 "微筛选器"）驱动程序。
