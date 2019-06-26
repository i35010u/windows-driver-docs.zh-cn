---
title: 在 Visual Studio 中设置符号和可执行映像路径
description: 该过程包括设置符号和 Visual Studio 中的可执行文件映像路径
ms.assetid: BFFF9BBC-C926-4974-A43E-C3A2DDA74AA4
ms.date: 05/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8c299b26ce55ddc964c3b26c22e7263b39cca9d3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366385"
---
# <a name="setting-symbol-and-executable-image-paths-in-visual-studio"></a>在 Visual Studio 中设置符号和可执行映像路径

> [!IMPORTANT]
> 此功能不在 Windows 10，版本 1507年和更高版本的 WDK 中可用。
>


本主题中所示的步骤要求具有集成到 Visual Studio Windows 驱动程序工具包。 要获取的集成的环境，请首先安装 Microsoft Visual Studio 中，然后再安装 Windows Driver Kit (WDK)。 有关详细信息，请参阅[Windows 驱动程序开发](https://docs.microsoft.com/windows-hardware/drivers/)。

## <a name="span-idsettingthesymbolpathbyusingapropertypagespanspan-idsettingthesymbolpathbyusingapropertypagespanspan-idsettingthesymbolpathbyusingapropertypagespansetting-the-symbol-path-by-using-a-property-page"></a><span id="Setting_the_Symbol_Path_by_Using_a_Property_Page"></span><span id="setting_the_symbol_path_by_using_a_property_page"></span><span id="SETTING_THE_SYMBOL_PATH_BY_USING_A_PROPERTY_PAGE"></span>使用属性页设置符号路径


1.  在主计算机，在 Visual Studio 中，选择**选项**从**工具**菜单。
2.  在中**选项**属性框中，导航到**调试&gt;符号**。
3.  如果你想要从 Microsoft 符号服务器获取的符号，请检查**Microsoft 符号服务器**。
4.  如果你想要从主机计算机上的文件夹中获取的符号，请检查**环境变量：\_NT\_符号\_路径**。 然后设置\_NT\_符号\_路径[环境变量](general-environment-variables.md)。

## <a name="span-idsettingthesymbolpathbyenteringacommandspanspan-idsettingthesymbolpathbyenteringacommandspanspan-idsettingthesymbolpathbyenteringacommandspansetting-the-symbol-path-by-entering-a-command"></a><span id="Setting_the_Symbol_Path_by_Entering_a_Command"></span><span id="setting_the_symbol_path_by_entering_a_command"></span><span id="SETTING_THE_SYMBOL_PATH_BY_ENTERING_A_COMMAND"></span>通过输入命令设置符号路径


在 Visual Studio 中，在调试器即时窗口中，输入[ **.sympath （设置符号路径）** ](-sympath--set-symbol-path-.md)命令。

## <a name="span-idsettingtheexecutableimagepathbyenteringacommandspanspan-idsettingtheexecutableimagepathbyenteringacommandspanspan-idsettingtheexecutableimagepathbyenteringacommandspansetting-the-executable-image-path-by-entering-a-command"></a><span id="Setting_the_Executable_Image_Path_by_Entering_a_Command"></span><span id="setting_the_executable_image_path_by_entering_a_command"></span><span id="SETTING_THE_EXECUTABLE_IMAGE_PATH_BY_ENTERING_A_COMMAND"></span>通过输入命令设置的可执行映像路径


在 Visual Studio 中，在调试器即时窗口中，输入[ **.exepath （设置可执行文件路径）** ](-exepath--set-executable-path-.md)命令。

 

 





