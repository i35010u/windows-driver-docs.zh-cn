---
title: Windows Vista 中对打印机窗体的更改
description: Windows Vista 中对打印机窗体的更改
keywords:
- 打印机窗体 WDK
- forms WDK 打印机
- 特殊形式 WDK 打印机
- 特殊纸张大小 WDK 打印机
- 纸张大小 WDK 窗体
- 自定义表单 WDK 打印机
- FORM_INFO_2 数据结构 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c78434fb1d3da407e82c43f3880f2ae186fd2157
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797731"
---
# <a name="changes-to-printer-forms-in-windows-vista"></a>Windows Vista 中对打印机窗体的更改


在 Windows Vista 之前，窗体使用窗体的名称和大小在内部进行标识。 但是，当打印服务器和客户端计算机使用已本地化为不同语言的打印机驱动程序时，此方法并不一定有效。 在 Windows Vista 中，打印后台处理程序已经过改进，因此打印机驱动程序可以支持已本地化为不同语言的客户端计算机和打印服务器。

Windows Vista 添加了窗体 \_ info \_ 2 数据结构，它是表单 \_ info 1 数据结构的超集，其中包含的信息是 \_ 使打印机驱动程序可以在具有不同语言的系统上工作所需的信息的其他成员。

Windows Vista 还升级了 Unidrv 打印机驱动程序，以使用窗体 \_ INFO \_ 2 数据结构，并通过使用 GPD 文件中的数据来填充其他成员。 \_ \_ \_ \_ 如果用户需要新结构提供的其他信息，则可以将使用表单 info 1 结构的单一打印机驱动程序升级为使用表单 info 2 结构。

本部分介绍如何更新 Unidrv 打印机驱动程序的 GPD 文件或单一打印机驱动程序中的代码，以使用表单 \_ INFO \_ 2 数据结构提供的新成员。

本部分介绍适用于 Windows Vista 的打印机窗体的以下改进：

[窗体 \_ 信息 \_ 2 数据结构](form-info-2-data-structure.md)

[改进的窗体匹配算法](improved-form-matching-algorithm.md)

[改进的窗体-纸盘匹配算法](improved-form-to-tray-matching-algorithm.md)

有关使用打印机窗体的详细信息，请参阅 Microsoft Windows SDK 文档。

 

 




