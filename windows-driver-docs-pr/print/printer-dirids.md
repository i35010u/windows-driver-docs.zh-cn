---
title: 打印机 Dirids
description: 打印机 Dirids
ms.assetid: 104af180-c739-4733-b21b-448cfe15ab71
keywords:
- INF 文件 WDK 打印，dirids
- dirids WDK
- 目录标识符 WDK 打印机
- printer dirids WDK
- 标识符 WDK 打印机
ms.date: 06/12/2020
ms.localizationpriority: medium
ms.openlocfilehash: 4ffc08cdf7f6adcd40052e178b6b93561b72e4d6
ms.sourcegitcommit: 8a3cb2a87ce9751059bca8145a55b8cc39c34de9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/13/2020
ms.locfileid: "84756177"
---
# <a name="printer-dirids"></a>打印机 Dirids

指定 INF 文件中的目标目录时，应使用目录标识符（ `dirids` ）。 有关详细信息，请参阅[Using Dirids](https://docs.microsoft.com/windows-hardware/drivers/install/using-dirids)。

下表列出了打印机特定 `dirids` 的和每个的用途。

| Dirid | 目标 | 目录内容 |
|--|--|--|
| 66000 | 表示[GetPrinterDriverDirectory](https://docs.microsoft.com/windows/win32/printdocs/getprinterdriverdirectory)函数返回的目录路径。 | 驱动程序文件和[依赖文件](printer-inf-file-entries.md#ddk-dependent-files-gg)相关文件 |
| 66001 | 表示[GetPrintProcessorDirectory](https://docs.microsoft.com/windows/win32/printdocs/getprintprocessordirectory)函数返回的目录路径。 | [打印处理器](https://docs.microsoft.com/windows-hardware/drivers/#wdkgloss-print-processor)文件。 |
| 66002 | 表示要复制到本地系统 \System32 的其他文件的目录路径。 请参阅此表后面的段落。 | [打印监视器](https://docs.microsoft.com/windows-hardware/drivers/#wdkgloss-print-monitor)文件。 |
| 66003 | 表示[GetColorDirectory](https://docs.microsoft.com/previous-versions/windows/desktop/wcs/getcolordirectory)函数返回的目录路径。 | ICM 颜色配置文件。 |
| 66004 | 表示将打印机类型特定的 ASP 文件复制到的目录路径。 | ASP 文件和关联的文件。 |

`dirid`如果本地系统上安装了本机体系结构的打印机驱动程序，例如在 x86 系统上本地安装 x86 驱动程序，则分配给66002的目录中的文件将复制到 System32 子目录。 如果将驱动程序安装到远程系统，则会忽略此目录中的文件。

当打印机类安装程序调用后台处理程序的[AddPrinterDriverEx](https://docs.microsoft.com/windows/win32/printdocs/addprinterdriverex)函数时，将安装打印机驱动程序。 此函数要求所有驱动程序文件都位于**GetPrinterDriverDirectory**函数所返回的目录中。
