---
title: 在 Visual Studio 中设置符号和可执行映像路径
description: 此过程介绍如何在 Visual Studio 中设置符号和可执行图像路径
ms.date: 05/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4b144e9cbfbdc8038261341dacd09d8e7f810134
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821571"
---
# <a name="setting-symbol-and-executable-image-paths-in-visual-studio"></a>在 Visual Studio 中设置符号和可执行映像路径

> [!IMPORTANT]
> 此功能在 Windows 10 版本1507及更高版本的 WDK 中不可用。
>


本主题中所示的过程要求将 Windows 驱动程序工具包集成到 Visual Studio 中。 若要获取集成环境，请首先安装 Microsoft Visual Studio，然后安装 Windows 驱动程序工具包 (WDK) 。 有关详细信息，请参阅 [使用 Visual Studio 进行调试](debugging-using-visual-studio.md)。

## <a name="span-idsetting_the_symbol_path_by_using_a_property_pagespanspan-idsetting_the_symbol_path_by_using_a_property_pagespanspan-idsetting_the_symbol_path_by_using_a_property_pagespansetting-the-symbol-path-by-using-a-property-page"></a><span id="Setting_the_Symbol_Path_by_Using_a_Property_Page"></span><span id="setting_the_symbol_path_by_using_a_property_page"></span><span id="SETTING_THE_SYMBOL_PATH_BY_USING_A_PROPERTY_PAGE"></span>使用属性页设置符号路径


1.  在主计算机上的 Visual Studio 中，从 "**工具**" 菜单中选择 "**选项**"。
2.  在 " **选项** " 属性框中，导航到 " **调试 &gt; 符号**"。
3.  如果要从 Microsoft 符号服务器获取符号，请检查 **Microsoft 符号** 服务器。
4.  如果要从主计算机上的文件夹中获取符号，请检查 **环境变量： \_ NT \_ 符号 \_ 路径**。 然后设置 \_ NT \_ 符号 \_ 路径 [环境变量](general-environment-variables.md)。

## <a name="span-idsetting_the_symbol_path_by_entering_a_commandspanspan-idsetting_the_symbol_path_by_entering_a_commandspanspan-idsetting_the_symbol_path_by_entering_a_commandspansetting-the-symbol-path-by-entering-a-command"></a><span id="Setting_the_Symbol_Path_by_Entering_a_Command"></span><span id="setting_the_symbol_path_by_entering_a_command"></span><span id="SETTING_THE_SYMBOL_PATH_BY_ENTERING_A_COMMAND"></span>通过输入命令设置符号路径


在 Visual Studio 的 "调试器即时" 窗口中，输入 [**. sympath (设置符号路径)**](-sympath--set-symbol-path-.md) 命令。

## <a name="span-idsetting_the_executable_image_path_by_entering_a_commandspanspan-idsetting_the_executable_image_path_by_entering_a_commandspanspan-idsetting_the_executable_image_path_by_entering_a_commandspansetting-the-executable-image-path-by-entering-a-command"></a><span id="Setting_the_Executable_Image_Path_by_Entering_a_Command"></span><span id="setting_the_executable_image_path_by_entering_a_command"></span><span id="SETTING_THE_EXECUTABLE_IMAGE_PATH_BY_ENTERING_A_COMMAND"></span>通过输入命令设置可执行映像路径


在 Visual Studio 的 "调试器即时" 窗口中，输入 [**. exepath (设置可执行文件路径)**](-exepath--set-executable-path-.md) 命令。

 

 





