---
title: 在 Visual Studio 中输入调试器命令
description: 这些过程介绍了如何在 Visual Studio 中输入调试器命令。
ms.assetid: 0590D849-3885-46D9-A6A1-55F3086B95FF
ms.date: 08/23/2018
ms.localizationpriority: medium
ms.openlocfilehash: 298a8fa6a4dd015cb4cd0529e7051e0fc904ab0d
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216664"
---
# <a name="entering-debugger-commands-in-visual-studio"></a>在 Visual Studio 中输入调试器命令

> [!IMPORTANT]
> 此功能在 Windows 10 版本1507及更高版本的 WDK 中不可用。
> 作为 Visual Studio 的替代方法，请使用 WinDbg Preview 中的命令窗口。 有关详细信息，请参阅 [WinDbg 预览-查看菜单](windbg-view-preview.md) 和 [调试器命令](debugger-commands.md)。
>

本主题中所示的过程要求将 Windows 驱动程序工具包集成到 Visual Studio 中。 若要获取集成环境，请首先安装 Microsoft Visual Studio，然后安装 Windows 驱动程序工具包 (WDK) 。 有关详细信息，请参阅 [Windows 驱动程序开发](../index.yml)。

在 Visual Studio 中，可以在调试器的 "即时" 窗口中输入调试器命令。 若要打开调试器的 "即时" 窗口，请从 " **调试** " 菜单中选择 " ** &gt; 立即**"。