---
title: PnPUtil
description: PnPUtil
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cdcaad62f9037ef49972cfa128b79e354ee20f54
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841024"
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

> [!NOTE]
> Windows Vista 和更高版本的 Windows 上支持 PnPUtil。 PnPUtil 不适用于 Windows XP，但你可以使用 [驱动程序安装框架 (DIFx) ](../install/difx-guidelines.md) 工具来创建和自定义驱动程序包的安装。
