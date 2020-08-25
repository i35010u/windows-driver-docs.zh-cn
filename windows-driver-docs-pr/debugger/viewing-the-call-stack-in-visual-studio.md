---
title: 在 Visual Studio 中查看调用堆栈
description: 此过程介绍如何在 Visual Studio 中查看调用堆栈
ms.assetid: 060A2441-C1A7-4485-82E5-2C024E6A3FBE
ms.date: 05/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9c8c5185c45b516c09b64140ea46db347d819932
ms.sourcegitcommit: 17c1bbc5ea0bef3bbc87794b030a073f905dc942
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88802751"
---
# <a name="viewing-the-call-stack-in-visual-studio"></a>在 Visual Studio 中查看调用堆栈

> [!IMPORTANT]
> 此功能在 Windows 10 版本1507及更高版本的 WDK 中不可用。
>

本主题中所示的过程要求将 Windows 驱动程序工具包集成到 Visual Studio 中。 若要获取集成环境，请首先安装 Microsoft Visual Studio，然后安装 Windows 驱动程序工具包 (WDK) 。 有关详细信息，请参阅 [Windows 驱动程序开发](https://docs.microsoft.com/windows-hardware/drivers/)。

## <a name="span-idusing_the_call_stack_windowspanspan-idusing_the_call_stack_windowspanspan-idusing_the_call_stack_windowspanusing-the-call-stack-window"></a><span id="Using_the_Call_Stack_Window"></span><span id="using_the_call_stack_window"></span><span id="USING_THE_CALL_STACK_WINDOW"></span>使用 "调用堆栈" 窗口


若要在 Visual Studio 中打开 " **调用堆栈** " 窗口，请从 " **调试** " 菜单中选择 " **Windows &gt; 调用堆栈**"。 若要将本地上下文设置为堆栈跟踪显示中的特定行，请选择并按住 (或双击) 行的第一列。

## <a name="span-idviewing_the_call_stack_by_entering_commandsspanspan-idviewing_the_call_stack_by_entering_commandsspanspan-idviewing_the_call_stack_by_entering_commandsspanviewing-the-call-stack-by-entering-commands"></a><span id="Viewing_the_Call_Stack_by_Entering_Commands"></span><span id="viewing_the_call_stack_by_entering_commands"></span><span id="VIEWING_THE_CALL_STACK_BY_ENTERING_COMMANDS"></span>通过输入命令查看调用堆栈


在调试器的 "即时" 窗口中，可以通过输入其中一个 [**k (显示堆栈 Backtrace) **](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md) 命令来查看调用堆栈。 如果尚未打开调试器的 "即时" 窗口，请从 " **调试** " 菜单中选择 " ** &gt; 立即 Windows**"。

 

 





