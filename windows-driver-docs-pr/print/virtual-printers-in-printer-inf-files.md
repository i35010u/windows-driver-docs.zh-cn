---
title: 打印机 INF 文件中的虚拟打印机
description: 打印机 INF 文件中的虚拟打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f3e9a02946bc30e184ce92d3c884f80ebada317
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785821"
---
# <a name="virtual-printers-in-printer-inf-files"></a>打印机 INF 文件中的虚拟打印机


虚拟打印机是打印目标，例如传真服务器或电子文档，它不是物理打印机。 因为虚拟打印机没有硬件 ID，所以必须使用 null 硬件 ID 在打印机 INF 文件中表示它。

若要在 INF 文件中插入 null 硬件 ID，请在 "安装" 部分名称和兼容 ID 之间的 INF 的 "模型" 部分中添加另一个逗号。 下面的示例演示如何为指定的传真打印机创建 null 硬件 ID。

```cpp
"Objectworld Fax Printer"=OWFAX,,Objectworld_Fax_Printer
```

有关 INF 文件中的虚拟打印机的详细信息，请参阅 [PRINTER Inf File 条目](printer-inf-file-entries.md)中的 **DriverCategory** 。

 

 




