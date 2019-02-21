---
title: 绘图器驱动程序微型驱动程序
description: 绘图器驱动程序微型驱动程序
ms.assetid: f7223a0a-df02-4a4f-a3d6-7910aed926eb
keywords:
- 绘图器驱动程序 WDK 打印，微型驱动程序
- MSPlot WDK 打印，微型驱动程序
- 微型驱动程序 WDK MSPlot
- PCD 文件 WDK MSPlot
- .pcd 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c38dbc5d532a603fc524c6ca7b8313c3813c88f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526610"
---
# <a name="plotter-driver-minidrivers"></a>绘图器驱动程序微型驱动程序





Microsoft 绘图器驱动程序的特定于模型的微型驱动程序是创建描述设备的特征的文本文件的供应商提供二进制.pcd 文件。

### <a href="" id="ddk-pcd-files-gg"></a>PCD 文件

若要生成。*pcd*文件中，您必须首先创建文本文件使用[PCD 源文件格式](pcd-source-file-format.md)。 您必须运行 plotgpc.exe，包括使用 Windows Driver Kit (WDK)。 此程序将文本文件转换成二进制.pcd 文件。 使用以下命令语法：

**plotgpc***source-file-path* .txt *target-file-path* .pcd

对于源和目标文件，则必须显式指定文件扩展名;不支持默认值。

示例文本文件可以用作输入 plotgpc.exe 纳入[示例绘图器驱动程序文件](sample-plotter-driver-files.md)。

 

 




