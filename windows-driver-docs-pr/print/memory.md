---
title: '内存 (打印) '
description: 打印设备中安装的内存的值项
ms.date: 07/07/2020
ms.localizationpriority: medium
ms.openlocfilehash: d2d78d0c6257750a736f6304a5125286655d5a3b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807881"
---
# <a name="memory-print"></a>内存 (打印) 

架构路径： \\Printer.Configu。记忆

节点类型：属性

说明：设备中安装的内存的值项

内存属性包含两个子值： **Size** 和 **PS**。

## <a name="size"></a>大小

架构路径： \\Printer.Configu。内存：大小

节点类型：值

数据类型：双向 \_ INT

说明：设备中安装的物理内存量（kb (KB) ）。

## <a name="ps"></a>PS

架构路径： \\Printer.Configu。内存： PS

节点类型：值

数据类型：双向 \_ INT

说明：设备中 Postscript 解释器可用的内存量（kb (KB) ）。 此量应小于安装的物理内存量。
