---
title: 在 Visual Studio 中配置异常和事件
description: 您可以配置 Windows 调试器以预先确定的方式响应指定的异常和事件。 对于每个异常，可以设置中断状态和处理状态。
ms.date: 05/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: d3bc8acbc85794fade18de224a0c0d15f8118cf8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820965"
---
# <a name="configuring-exceptions-and-events-in-visual-studio"></a>在 Visual Studio 中配置异常和事件

> [!IMPORTANT]
> 此功能在 Windows 10 版本1507及更高版本的 WDK 中不可用。
>


您可以配置 Windows 调试器以预先确定的方式响应指定的异常和事件。 对于每个异常，可以设置中断状态和处理状态。 对于每个事件，可以设置中断状态。

本主题中所示的过程要求将 Windows 驱动程序工具包集成到 Visual Studio 中。 若要获取集成环境，请首先安装 Microsoft Visual Studio，然后安装 Windows 驱动程序工具包 (WDK) 。 有关详细信息，请参阅 [Windows 驱动程序开发](../index.yml)。

可以通过在调试器的 "即时" 窗口中输入以下命令来配置中断状态或处理状态。 如果尚未打开调试器的 "即时" 窗口，请从 " **调试** " 菜单中选择 " **&gt; 立即 Windows**"。

-   [**sxe**](sx--sxd--sxe--sxi--sxn--sxr--sx---set-exceptions-.md)
-   [**sxd**](sx--sxd--sxe--sxi--sxn--sxr--sx---set-exceptions-.md)
-   [**sxn**](sx--sxd--sxe--sxi--sxn--sxr--sx---set-exceptions-.md)
-   [**sxi**](sx--sxd--sxe--sxi--sxn--sxr--sx---set-exceptions-.md)

有关异常和事件的详细讨论，请参阅 [控制异常和事件](controlling-exceptions-and-events.md)。

 

