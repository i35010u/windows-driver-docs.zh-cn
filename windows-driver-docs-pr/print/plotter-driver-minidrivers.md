---
title: 绘图仪驱动程序微型驱动程序
description: 绘图仪驱动程序微型驱动程序
keywords:
- 绘图仪驱动程序 WDK 打印，微型驱动程序
- MSPlot WDK 打印，微型驱动程序
- 微型驱动程序 WDK MSPlot
- PCD 文件 WDK MSPlot
- pcd 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 206bb540f4164718e8609b8e54072a6b8eedcfc8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807595"
---
# <a name="plotter-driver-minidrivers"></a>绘图仪驱动程序微型驱动程序





Microsoft 绘图仪驱动程序的特定于模型的微型驱动程序是由供应商提供的 pcd 文件，这些文件是从描述设备特征的文本文件创建的。

### <a name="pcd-files"></a><a href="" id="ddk-pcd-files-gg"></a>PCD 文件

生成。*pcd* 文件，必须首先使用 [pcd 源文件格式](pcd-source-file-format.md)创建文本文件。 然后，你必须运行 plotgpc.exe，Windows 驱动程序工具包 (WDK) 附带。 此程序会将文本文件转换为 pcd 文件。 使用以下命令语法：

**plotgpc**-file-file *-* _path._ pcd

对于源文件和目标文件，必须显式指定文件扩展名;不支持默认值。

一个示例文本文件，可将其用作 plotgpc.exe 的输入内容包含在 [绘图仪驱动程序文件](sample-plotter-driver-files.md)中。

 

 




