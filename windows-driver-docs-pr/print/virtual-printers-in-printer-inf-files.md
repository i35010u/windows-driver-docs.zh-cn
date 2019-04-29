---
title: 打印机 INF 文件中的虚拟打印机
description: 打印机 INF 文件中的虚拟打印机
ms.assetid: a7308b0f-61b8-4b4d-a116-ce940787882b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28140db763668d9bc01fb9cedb1f004f9739590a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363716"
---
# <a name="virtual-printers-in-printer-inf-files"></a>打印机 INF 文件中的虚拟打印机


虚拟打印机是当打印目标，例如传真服务器或不物理打印机的电子文档。 由于虚拟打印机无法硬件 ID，它必须用来表示打印机 INF 文件中为 null 的硬件 id。

若要在 INF 文件中插入 null 硬件 ID，可安装部分名称和兼容 id。 之间 INF 的模型部分添加第二个以逗号 下面的示例演示如何创建空的硬件 ID 所指示的传真打印机。

```cpp
"Objectworld Fax Printer"=OWFAX,,Objectworld_Fax_Printer
```

INF 文件中的虚拟打印机的详细信息，请参阅**DriverCategory**中[打印机 INF 文件条目](printer-inf-file-entries.md)。

 

 




