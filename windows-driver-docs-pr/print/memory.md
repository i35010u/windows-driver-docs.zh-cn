---
title: 内存（打印）
description: 打印设备中安装的内存的值项
ms.assetid: 9e1ad59f-9a97-49d7-b749-14380067cf64
ms.date: 07/07/2020
ms.localizationpriority: medium
ms.openlocfilehash: 45d7702b716f4a7a188d6170e181aecf40d90310
ms.sourcegitcommit: ff2f72fe98f6ba559c1c01b17d25c773df7337c1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/07/2020
ms.locfileid: "86060800"
---
# <a name="memory-print"></a>内存（打印）

架构路径： \\Printer.Configu。记忆

节点类型：属性

说明：设备中安装的内存的值项

内存属性包含两个子值： **Size**和**PS**。

## <a name="size"></a>大小

架构路径： \\Printer.Configu。内存：大小

节点类型：值

数据类型：双向 \_ INT

说明：设备中安装的物理内存量（以千字节（KB）为单位）。

## <a name="ps"></a>PS

架构路径： \\Printer.Configu。内存： PS

节点类型：值

数据类型：双向 \_ INT

说明：设备中 Postscript 解释器可用的内存量（kb）。 此量应小于安装的物理内存量。
