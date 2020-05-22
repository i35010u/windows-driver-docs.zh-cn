---
title: PnPUtil
description: PnPUtil
ms.assetid: 3678fd41-c3ee-4538-b783-6f099ac104a6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9556127d2cc0be3ba5188dcdfdf7ed8655f53d9
ms.sourcegitcommit: 34a06eda78c8d935f3900b86fa0f620027bc6577
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/22/2020
ms.locfileid: "83778347"
---
# <a name="pnputil"></a>PnPUtil

PnPUtil （PnPUtil）是一种命令行工具，可让管理员对[驱动程序包](../install/driver-packages.md)执行操作。  示例包括：

- 将驱动程序包添加到[驱动程序存储区](../install/driver-store.md)。

- 在计算机上安装驱动程序包。

- 从驱动程序存储区中删除驱动程序包。

- 枚举当前位于驱动程序存储区中的驱动程序包。 仅列出非内置包的驱动程序包。 *内置*驱动程序包是 Windows 或其 service pack 的默认安装中包含的程序包。

## <a name="where-can-i-download-pnputil"></a>在哪里可以下载 PnPUtil？

PnPUtil 包含在 Windows 的每个版本中，从 Windows Vista 开始（在 `%windir%\system32` 目录中）。 没有单独的 PnPUtil 下载包。

- 打开 "**命令提示符**" 窗口（**以管理员身份运行**）。
- 键入 `pnputil /?` 以查看命令选项。 有关详细信息，请参阅[**PnPUtil 命令语法**](pnputil-command-syntax.md)。

> [!NOTE]
> Windows Vista 和更高版本的 Windows 上支持 PnPUtil。 PnPUtil 不适用于 Windows XP，但你可以使用[驱动程序安装框架（DIFx）](../install/difx-guidelines.md)工具来创建和自定义驱动程序包的安装。
