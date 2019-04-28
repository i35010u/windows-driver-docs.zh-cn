---
title: Windows Vista 中对打印机窗体的更改
description: Windows Vista 中对打印机窗体的更改
ms.assetid: 6e970cbd-1c7f-4c48-8d05-a29f922a3f33
keywords:
- 打印机纸张规格 WDK
- 窗体 WDK 打印机
- 特殊的窗体 WDK 打印机
- 特殊纸张大小 WDK 打印机
- 纸张大小 WDK 窗体
- 自定义窗体 WDK 打印机
- FORM_INFO_2 数据结构 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e3d921e812651fddb5e6f5c98c1a1f73a90f6c3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347217"
---
# <a name="changes-to-printer-forms-in-windows-vista"></a>Windows Vista 中对打印机窗体的更改


在 Windows Vista 之前窗体发现在内部使用的名称和窗体大小。 此方法，但是，没有始终奏效时打印服务器和客户端计算机使用的打印机驱动程序的已本地化为不同的语言。 在 Windows Vista 中，打印后台处理程序进行了改进，因此打印机驱动程序可以支持客户端计算机和打印服务器的已本地化为不同的语言。

Windows Vista 添加了窗体\_INFO\_2 个数据结构，它是窗体的超集\_信息\_1 个数据结构，其中包含你需要启用打印机驱动程序的信息的其他成员跨具有不同的语言的系统工作。

Unidrv 打印机驱动程序也已升级适用于 Windows Vista 使用窗体\_信息\_2 个数据结构，然后从 GPD 文件使用的数据填充中的其他成员。 你可以升级使用窗体的整体式打印机驱动程序\_INFO\_1 结构使用窗体\_信息\_2 结构，如果需要新的结构提供的附加信息。

本部分介绍了如何更新 GPD 文件 Unidrv 打印机驱动程序或代码的整体化打印机驱动程序以使用新成员中的窗体\_信息\_2 数据结构提供。

本部分介绍适用于 Windows Vista 在打印机窗体中的以下改进：

[窗体\_信息\_2 个数据结构](form-info-2-data-structure.md)

[改进了匹配算法的窗体](improved-form-matching-algorithm.md)

[改进的送纸器格式匹配算法](improved-form-to-tray-matching-algorithm.md)

有关使用打印机纸张规格的详细信息，请参阅 Microsoft Windows SDK 文档。

 

 




