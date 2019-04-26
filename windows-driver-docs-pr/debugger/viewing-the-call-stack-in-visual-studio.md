---
title: 在 Visual Studio 中查看调用堆栈
description: 过程介绍如何在 Visual Studio 中查看调用堆栈
ms.assetid: 060A2441-C1A7-4485-82E5-2C024E6A3FBE
ms.date: 05/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 96e9de51ed45073a29f8ba2dd4f09b2ccb687d40
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325903"
---
# <a name="viewing-the-call-stack-in-visual-studio"></a>在 Visual Studio 中查看调用堆栈

> [!IMPORTANT]
> 此功能不在 Windows 10，版本 1507年和更高版本的 WDK 中可用。
>

本主题中所示的步骤要求具有集成到 Visual Studio Windows 驱动程序工具包。 要获取的集成的环境，请首先安装 Microsoft Visual Studio 中，然后再安装 Windows Driver Kit (WDK)。 有关详细信息，请参阅[Windows 驱动程序开发](https://msdn.microsoft.com/library/windows/hardware/ff557573)。

## <a name="span-idusingthecallstackwindowspanspan-idusingthecallstackwindowspanspan-idusingthecallstackwindowspanusing-the-call-stack-window"></a><span id="Using_the_Call_Stack_Window"></span><span id="using_the_call_stack_window"></span><span id="USING_THE_CALL_STACK_WINDOW"></span>使用调用堆栈窗口


若要打开**调用堆栈**窗口在 Visual Studio 中，从**调试**菜单中，选择**Windows&gt;调用堆栈**。 若要设置本地上下文中的堆栈跟踪显示某个特定行，双击的行的第一列。

## <a name="span-idviewingthecallstackbyenteringcommandsspanspan-idviewingthecallstackbyenteringcommandsspanspan-idviewingthecallstackbyenteringcommandsspanviewing-the-call-stack-by-entering-commands"></a><span id="Viewing_the_Call_Stack_by_Entering_Commands"></span><span id="viewing_the_call_stack_by_entering_commands"></span><span id="VIEWING_THE_CALL_STACK_BY_ENTERING_COMMANDS"></span>通过输入命令查看调用堆栈


在调试器即时窗口中，您可以查看调用堆栈通过输入之一[ **k （显示堆栈回溯）** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)命令。 如果尚未打开，请在调试器即时窗口**调试**菜单中，选择**Windows&gt;即时**。

 

 





