---
ms.assetid: D4B7FC2A-259F-4B72-A52B-03CBF712D5C5
title: 验证通用 Windows 驱动程序
description: 可以使用 ApiValidator.exe 工具验证驱动程序调用的 API 是否对通用 Windows 驱动程序有效。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 045d6911386f407d87c7f22910e017e91cb74216
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518351"
---
# <a name="validating-universal-windows-drivers"></a>验证通用 Windows 驱动程序

可以使用 ApiValidator.exe 工具验证二进制文件调用的 API 是否对通用 Windows 驱动程序有效。 如果二进制文件调用的 API 不是有效的通用 Windows 驱动程序 API，该工具将返回错误。 此工具是适用于 Windows 10 的 Windows 驱动程序工具包 (WDK) 的一部分。

## <a name="span-idrunningapivalidatorinvisualstudiospanspan-idrunningapivalidatorinvisualstudiospanspan-idrunningapivalidatorinvisualstudiospanrunning-apivalidator-in-visual-studio"></a><span id="Running_ApiValidator_in_Visual_Studio"></span><span id="running_apivalidator_in_visual_studio"></span><span id="RUNNING_APIVALIDATOR_IN_VISUAL_STUDIO"></span>在 Visual Studio 中运行 ApiValidator


如果驱动程序项目的“目标平台”属性设置为“通用”，Visual Studio 将作为生成后步骤自动运行 ApiValidator。

若要查看 ApiValidator 显示的所有消息，请导航到“工具”&gt;“选项”&gt;“项目和解决方案”&gt;“生成并运行”，并将“MSBuild 项目生成输出详细级别”设置为“详细”。 从命令行生成时，请将开关 **/v:detailed** 或 **/v:diag** 添加到生成命令以提高详细级别。

对于 umdf2\_fx2 驱动程序示例，API 验证错误如下所示：

```cpp
Warning  1   warning : API DecodePointer in kernel32.dll is not supported. osrusbfx2um.dll calls this API.   C:\Program Files (x86)\Windows Kits\10\src\usb\umdf2_fx2\driver\ApiValidator.exe    osrusbfx2um
Warning 2   warning : API DisableThreadLibraryCalls in kernel32.dll is not supported. osrusbfx2um.dll calls this API.   C:\Program Files (x86)\Windows Kits\10\src\usb\umdf2_fx2\driver\ApiValidator.exe    osrusbfx2um
Warning 3   warning : API EncodePointer in kernel32.dll is not supported. osrusbfx2um.dll calls this API.   C:\Program Files (x86)\Windows Kits\10\src\usb\umdf2_fx2\driver\ApiValidator.exe    osrusbfx2um
Warning 4   warning : API GetCurrentProcessId in kernel32.dll is not supported. osrusbfx2um.dll calls this API. C:\Program Files (x86)\Windows Kits\10\src\usb\umdf2_fx2\driver\ApiValidator.exe    osrusbfx2um
Warning 5   warning : API GetCurrentThreadId in kernel32.dll is not supported. osrusbfx2um.dll calls this API.  C:\Program Files (x86)\Windows Kits\10\src\usb\umdf2_fx2\driver\ApiValidator.exe    osrusbfx2um
Warning 6   warning : API GetSystemTimeAsFileTime in kernel32.dll is not supported. osrusbfx2um.dll calls this API. C:\Program Files (x86)\Windows Kits\10\src\usb\umdf2_fx2\driver\ApiValidator.exe    osrusbfx2um
Warning 7   warning : API IsDebuggerPresent in kernel32.dll is not supported. osrusbfx2um.dll calls this API.   C:\Program Files (x86)\Windows Kits\10\src\usb\umdf2_fx2\driver\ApiValidator.exe    osrusbfx2um
Warning 8   warning : API IsProcessorFeaturePresent in kernel32.dll is not supported. osrusbfx2um.dll calls this API.   C:\Program Files (x86)\Windows Kits\10\src\usb\umdf2_fx2\driver\ApiValidator.exe    osrusbfx2um
Warning 9   warning : API QueryPerformanceCounter in kernel32.dll is not supported. osrusbfx2um.dll calls this API. C:\Program Files (x86)\Windows Kits\10\src\usb\umdf2_fx2\driver\ApiValidator.exe    osrusbfx2um
Error   10  error MSB3721: The command ""C:\Program Files (x86)\Windows Kits\10\bin\x64\ApiValidator.exe" -DriverPackagePath:"C:\Program Files (x86)\Windows Kits\10\src\usb\umdf2_fx2\Debug\\" -SupportedApiXmlFiles:"C:\Program Files (x86)\Windows Kits\10\build\universalDDIs\x86\UniversalDDIs.xml" -ApiExtractorExePath:"C:\Program Files (x86)\Windows Kits\10\bin\x64"" exited with code -1.    C:\Program Files (x86)\Windows Kits\10\build\WindowsDriver.common.targets   1531    5   osrusbfx2um
```

## <a name="fixing-validation-errors"></a>修复验证错误

1.  如果已将旧的桌面 UMDF 驱动程序项目切换为“通用”，请确认在生成二进制文件时包括正确的库。 右键单击该项目，然后选择“属性”。 导航到“链接器”-&gt;“输入”。 **其他依赖项**应包含：

    ```cpp
    %AdditionalDependencies);$(SDK_LIB_PATH)\OneCoreUAP.lib
    ```

    若要查看针对 OneCore SKU 的其他链接器选项，请参阅[针对 OneCore 生成](building-for-onecore.md)。

2.  一次删除或替换一个非通用 API 调用并重新运行工具，直到没有错误。

3.  在某些情况下，可以使用仅用于桌面的 DDI 参考页列出的备用 DDI 替换这些调用。 如果找不到适合的替换项，请[提交反馈](https://go.microsoft.com/fwlink/p/?linkid=529549)。  如果没有适合的替换项，可能必须编写解决方法代码。  如果需要，请从 WDK 中的驱动程序模板开始编写新的通用 Windows 驱动程序。

如果看到如下所示的错误，请参阅[针对 OneCore 生成](building-for-onecore.md)中的指南。

```cpp
ApiValidation: Error: FlexLinkTest.exe has a dependency on 'wtsapi32.dll!WTSEnumerateSessionsW' but is missing: IsApiSetImplemented("ext-ms-win-session-wtsapi32-l1-1-0")
ApiValidation: Error: FlexLinkTest.exe has a dependency on 'wtsapi32.dll!WTSFreeMemory' but is missing: IsApiSetImplemented("ext-ms-win-session-wtsapi32-l1-1-0")
ApiValidation: NOT all binaries are Universal
```

## <a name="running-apivalidator-from-the-command-prompt"></a>从命令提示符运行 ApiValidator

也可以从命令提示符运行 Apivalidator.exe。 在 WDK 安装中，导航到 C:\\Program Files (x86)\\Windows Kits\\10\\bin\\*&lt;arch&gt;*。

使用以下语法：

**Apivalidator.exe** **-DriverPackagePath：***&lt;驱动程序文件夹路径&gt;* **-SupportedApiXmlFiles：***&lt;包含通用驱动程序支持的 API 的 XML 文件的路径&gt;*

例如，若要验证 WDK 中的“活动”示例调用的 API，应首先在 Visual Studio 中生成示例。 然后，打开命令提示符并导航到包含工具的目录，例如，C:\\Program Files (x86)\\Windows Kits\\10\\bin\\x64。 输入以下命令：

**apivalidator.exe -DriverPackagePath:"C:\\Program Files (x86)\\Windows Kits\\10\\src\\usb\\umdf2\_fx2\\Debug\\\\" -SupportedApiXmlFiles:"c:\\Program Files (x86)\\Windows Kits\\10\\build\\universalDDIs\\x64\\UniversalDDIs.xml"**

此命令将生成以下输出：

```cpp
ApiValidator.exe: Warning: API DecodePointer in kernel32.dll is not supported. osrusbfx2um.dll calls this API.
ApiValidator.exe: Warning: API DisableThreadLibraryCalls in kernel32.dll is not supported. osrusbfx2um.dll calls this API.
ApiValidator.exe: Warning: API EncodePointer in kernel32.dll is not supported. osrusbfx2um.dll calls this API.
ApiValidator.exe: Warning: API GetCurrentProcessId in kernel32.dll is not supported. osrusbfx2um.dll calls this API.
ApiValidator.exe: Warning: API GetCurrentThreadId in kernel32.dll is not supported. osrusbfx2um.dll calls this API.
ApiValidator.exe: Warning: API GetSystemTimeAsFileTime in kernel32.dll is not supported. osrusbfx2um.dll calls this API.
ApiValidator.exe: Warning: API IsDebuggerPresent in kernel32.dll is not supported. osrusbfx2um.dll calls this API.
ApiValidator.exe: Warning: API IsProcessorFeaturePresent in kernel32.dll is not supported. osrusbfx2um.dll calls this API.
ApiValidator.exe: Warning: API QueryPerformanceCounter in kernel32.dll is not supported. osrusbfx2um.dll calls this API.

ApiValidator.exe Driver located at C:\Program Files (x86)\Windows Kits\10\src\usb\umdf2_fx2\Debug is NOT a Universal Driver
```

枚举通用 Windows 驱动程序的有效 API 的 XML 位于 C:\\Program Files (x86)\\Windows Kits\\10\\build\\universalDDIs\\*&lt;arch&gt;*。

## <a name="span-idtroubleshootingspanspan-idtroubleshootingspanspan-idtroubleshootingspantroubleshooting"></a><span id="Troubleshooting"></span><span id="troubleshooting"></span><span id="TROUBLESHOOTING"></span>故障排除


如果 ApiValidator.exe 输出格式不正确错误（如下所示）：

```cpp
Error      1              error : AitStatic output file has incorrect format or analysis run on incorrect file types.     C:\Program Files (x86)\Windows Kits\10\src\usb\umdf2_fx2\driver\ApiValidator.exe            osrusbfx2um
```

请使用此解决方法：

1.  打开“项目”属性，导航到“常规”，将“输出目录”重命名为以下内容：

    ```cpp
    $(SolutionDir)$(Platform)\$(ConfigurationName)\
    ```

2.  重新生成解决方案。

## <a name="known-issues"></a>已知问题

* ApiValidator 不能在 ARM64 上运行，因为 AitStatic 不能在 ARM64 上运行。
* ARM64 二进制文件可以在 x64 计算机上测试，但不能在 x86 计算机上测试。
* ApiValidator 可以在 x86 上运行，以测试 x86 二进制文件和 ARM 二进制文件。
* ApiValidator 可以在 x64 上运行，以测试 x86、x64、ARM 和 ARM64 二进制文件。


