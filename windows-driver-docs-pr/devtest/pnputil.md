---
title: PnPUtil
description: PnPUtil
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b06923dc4d28dc3e9f22edabf650a8ff4c0de266
ms.sourcegitcommit: 98a2748f98d0eaf5ca6af6568b1a3fc6f2c9b63a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/29/2021
ms.locfileid: "99057525"
---
# <a name="pnputil"></a>PnPUtil

PnPUtil ( # A0) 是一个命令行工具，可让管理员对 [驱动程序包](../install/driver-packages.md)执行操作。  示例包括：

- 将驱动程序包添加到 [驱动程序存储区](../install/driver-store.md)。

- 在计算机上安装驱动程序包。

- 从驱动程序存储区中删除驱动程序包。

- 枚举当前位于驱动程序存储区中的驱动程序包。 仅列出非内置包的驱动程序包。 *内置* 驱动程序包是 Windows 或其 service pack 的默认安装中包含的程序包。

## <a name="where-can-i-download-pnputil"></a>在哪里可以下载 PnPUtil？

PnPUtil 包含在 Windows 的每个版本中，从) 目录中的 Windows Vista (开始 `%windir%\system32` 。 没有单独的 PnPUtil 下载包。

- 打开 " **命令提示符** " 窗口 (**以管理员身份运行**) 。
- 键入 `pnputil /?` 以查看命令选项。 有关详细信息，请参阅 [**PnPUtil 命令语法**](pnputil-command-syntax.md) 。
