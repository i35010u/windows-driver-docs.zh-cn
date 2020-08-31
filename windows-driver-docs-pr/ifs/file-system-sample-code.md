---
title: 文件系统示例代码
description: 文件系统示例代码
ms.assetid: a64d83c6-d4cd-432d-bc1a-a3ff4656527c
keywords:
- 驱动程序 WDK 文件系统
- 文件系统驱动程序 WDK
ms.date: 02/10/2020
ms.localizationpriority: medium
ms.openlocfilehash: d0e94a9249cc4f30599c0567a956adef0b200ab2
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063652"
---
# <a name="file-system-sample-code"></a>文件系统示例代码

几乎在所有情况下，都不需要为 Windows 开发完整的文件系统驱动程序。 如果决定开发新的文件系统驱动程序，则可以使用[ *fastfat*示例](../samples/file-system-driver-samples.md)作为模型。 若要了解如何安装文件系统驱动程序，请参阅 [创建文件系统驱动程序的 INF 文件](creating-an-inf-file-for-a-file-system-driver.md)。

WDK 并不提供用于文件系统开发的概念文档。

Windows 上与文件系统相关的大多数开发涉及到创建文件系统筛选器 (或 "微微筛选器" ) 驱动程序，该驱动程序与系统提供的 [筛选器管理](filter-manager-concepts.md)器进行交互。