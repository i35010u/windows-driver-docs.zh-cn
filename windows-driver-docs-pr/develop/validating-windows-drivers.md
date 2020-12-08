---
ms.assetid: D4B7FC2A-259F-4B72-A52B-03CBF712D5C5
title: 验证通用 Windows 驱动程序
description: 可以使用 ApiValidator.exe 工具验证驱动程序调用的 API 是否对通用 Windows 驱动程序有效。
ms.date: 04/28/2020
ms.localizationpriority: medium
ms.openlocfilehash: 4884b563166d4128960744e5e00ca1bb89d0b0d8
ms.sourcegitcommit: f86e44d595be2c9e4efe3c196f6c0a9c71f4231e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/01/2020
ms.locfileid: "96470528"
---
# <a name="validating-windows-drivers"></a>验证 Windows 驱动程序

使用 InfVerif、驱动程序验证器驱动程序隔离检查和 ApiValidator 工具来测试 Windows 驱动程序是否符合 [Windows 驱动程序入门](getting-started-with-windows-drivers.md)中所述的要求。

## <a name="infverif"></a>InfVerif

[InfVerif](../devtest/infverif.md) 是一种工具，用于验证 INF 语法，并检查 INF 是否符合要求和限制。

结合使用 InfVerif 与 `/w` 和 `/v` 可以验证 Windows 驱动程序是否：

* 符合 [DCH 设计原则](dch-principles-best-practices.md)的声明性 (D) 原则
* 遵循 [Windows 驱动程序入门](getting-started-with-windows-drivers.md)中的[驱动程序包隔离](driver-isolation.md)要求

如需了解更多详情，请参阅[通过命令行运行 InfVerif](../devtest/running-infverif-from-the-command-line.md)。

### <a name="targeting-current-and-earlier-versions-of-windows"></a>面向当前版本的 Windows 和早期版本的 Windows

InfVerif 的每次运行测试单个规则集，例如 `/w`（Windows 驱动程序兼容性）或 `/k`（硬件开发人员中心提交）。  如果你的 INF 包含较新版本的 Windows 中引入的语法，并且你还想要将以前的 Windows 版本作为目标，请使用 [INF 修饰](../install/inf-manufacturer-section.md)来标记特定版本的 INF 项，然后多次运行 InfVerif，例如：

```inf
infverif /k <INF file>
infverif /w NTAMD64.10.0.0.<build number where w is a requirement> <INF file>
```

如果没有错误，则 INF 满足 Windows 驱动程序的[驱动程序包隔离](driver-isolation.md)要求。

例如，从 Windows 10 版本 1809 开始，[INF AddEventProvider 指令](../install/inf-addeventprovider-directive.md)可供使用。 若要在一个面向 Windows 10 版本 1809 之前的 OS 版本的 INF 中使用此指令，请修饰使用旧 INF 语法（用于注册 ETW 事件提供程序）的安装部分和使用已更新语法的安装部分。

有关演示如何使用 OS 修饰的示例代码，请参阅[适用于一个或多个目标操作系统的示例 INF 模型部分](../install/sample-inf-models-sections-for-one-or-more-target-operating-system.md)。

## <a name="driver-verifier-driver-isolation-checks"></a>驱动程序验证器驱动程序隔离检查

为了获得Windows 驱动程序的资格，驱动程序必须满足[驱动程序包隔离](driver-isolation.md)要求。 自 Windows 10 预览版 19568 开始，[驱动程序验证器](../devtest/driver-verifier.md) (DV) 会监视已隔离的驱动程序包所禁止的注册器读取和写入。

可在内核调试程序中发生违规行为时查看这些行为，也可配置 DV 来停止系统，并在发生违规行为时生成包含详细信息的内存转储。 可通过第一种方法开始驱动程序开发，然后在驱动程序快要完成时，切换到第二种方法。

若要在违规行为发生时进行查看，请先连接内核调试程序，然后使用以下命令。 重启操作启用 DV 设置后，可在内核调试程序输出中监视违规行为。

若要在单个驱动程序中启用驱动程序隔离：

```command
verifier /rc 33 36 /driver myDriver.sys
```

若要检查多个驱动程序，请使用空格隔离每个驱动程序名称：

```command
verifier /rc 33 36 /driver myDriver1.sys myDriver2.sys
```

若要配置 DV，使它在发生违规行为时进行 bug 检查，请使用以下语法：

```
verifier /onecheck /rc 33 36 /driver myDriver1.sys
```

需要重启才能启用验证设置。 若要通过命令行执行此操作，请指定：

```command
shutdown /r /t 0
```

下面是几个错误消息示例：

例如：ZwCreateKey 提供完全绝对路径：

`DRIVER_ISOLATION_VIOLATION: <driver name>: Registry operations should not use absolute paths. Detected creation of unisolated registry key \Registry\Machine\SYSTEM`

例如：ZwCreateKey 提供与句柄相对的路径，而此句柄并非来自已获批的 API 的：

`DRIVER_ISOLATION_VIOLATION: <driver name>: Registry operations should only use key handles returned from WDF or WDM APIs. Detected creation of unisolated registry key \REGISTRY\MACHINE\SYSTEM\SomeKeyThatShouldNotExist`

请考虑启用带有 DV 驱动程序隔离检查的[设备基础功能测试](../devtest/run-devfund-tests-via-the-command-line.md)，帮助及早捕获驱动程序隔离违规行为。

## <a name="apivalidator"></a>ApiValidator

ApiValidator 工具用于验证二进制文件调用的 API 是否对 Windows 驱动程序是有效的。 如果二进制文件调用的 API 在 Windows 驱动程序的有效 API 集之外，此工具就会返回错误。 此工具是 Windows 10 版 WDK 的一部分。

ApiValidator 用于验证驱动程序是否支持 [API 分层](api-layering.md)，这是 Windows 驱动程序的要求之一。 有关完整的要求列表，请参阅 [Windows 驱动程序入门](getting-started-with-windows-drivers.md)。

### <a name="running-apivalidator-in-visual-studio"></a>在 Visual Studio 中运行 ApiValidator

如果驱动程序项目的“目标平台”属性设置为“Windows 驱动程序”，Visual Studio 就会自动运行 ApiValidator 作为生成后步骤。

若要查看 ApiValidator 显示的所有消息，请依次转到“工具”->“选项”->“项目和解决方案”->“生成并运行”，并将“MSBuild 项目生成输出详细程度”设置为“详细”。 从命令行生成时，请将开关 **/v:detailed** 或 **/v:diag** 添加到生成命令以提高详细级别。

对于 umdf2_fx2 驱动程序示例，API 验证错误如下所示：

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

### <a name="fixing-validation-errors"></a>修复验证错误

1.  如果已将旧的桌面 UMDF 驱动程序项目切换为 Windows 驱动程序，请验证在生成二进制文件时是否添加了正确的库。 选择并按住（或右键单击）项目，然后选择属性。 依次转到“链接器”->“输入”。 **其他依赖项** 应包含：

    ```cpp
    %AdditionalDependencies);$(SDK_LIB_PATH)\OneCoreUAP.lib
    ```

    若要查看针对 OneCore SKU 的其他链接器选项，请参阅[针对 OneCore 生成](building-for-onecore.md)。

2.  一次删除或替换一个不允许的 API 调用，并重新运行此工具，直到没有错误。

3.  在某些情况下，可以使用仅用于桌面的 DDI 参考页列出的备用 DDI 替换这些调用。 如果没有适合的替换项，可能必须编写解决方法代码。  如果需要，可以从 WDK 中的驱动程序模板开始编写新的 Windows 驱动程序。

如果看到如下所示的错误，请参阅[针对 OneCore 生成](building-for-onecore.md)中的指南。

```cpp
ApiValidation: Error: FlexLinkTest.exe has a dependency on 'wtsapi32.dll!WTSEnumerateSessionsW' but is missing: IsApiSetImplemented("ext-ms-win-session-wtsapi32-l1-1-0")
ApiValidation: Error: FlexLinkTest.exe has a dependency on 'wtsapi32.dll!WTSFreeMemory' but is missing: IsApiSetImplemented("ext-ms-win-session-wtsapi32-l1-1-0")
ApiValidation: NOT all binaries are Universal
```

### <a name="running-apivalidator-from-the-command-prompt"></a>从命令提示符运行 ApiValidator

也可以从命令提示符运行 Apivalidator.exe。 在 WDK 安装中，转到 C:\Program Files (x86)\Windows Kits\10\bin\<arch> 和 C:\Program Files (x86)\Windows Kits\10\build\universalDDIs\<arch>。

重要说明：
* ApiValidator 需要以下文件：ApiValidator.exe、Aitstatic.exe、Microsoft.Kits.Drivers.ApiValidator.dll 和 UniversalDDIs.xml。
* UniversalDDIs.xml 必须与要验证的二进制文件体系结构相匹配（例如，对于 x64 驱动程序，使用 x64 UniversalDDI.xml）
* ApiValidator 一次只测试一个体系结构
* 有关其他信息，请参阅下面的“已知 ApiValidator 问题”

使用以下语法：

`Apivalidator.exe -DriverPackagePath: <driver folder path> -SupportedApiXmlFiles: (path to XML files containing supported APIs for Windows drivers)`

例如，若要验证 WDK 中的“活动”示例调用的 API，应首先在 Visual Studio 中生成示例。 然后，打开命令提示符，并转到包含此工具的目录（例如，`C:\Program Files (x86\Windows Kits\10\bin\x64`）。 输入以下命令：

`apivalidator.exe -DriverPackagePath:"C:\Program Files (x86)\Windows Kits\10\src\usb\umdf2\_fx2\Debug" -SupportedApiXmlFiles:"c:\Program Files (x86)\Windows Kits\10\build\universalDDIs\x64\UniversalDDIs.xml"`

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

### <a name="troubleshooting-apivalidator"></a>排除 ApiValidator 故障


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

### <a name="known-apivalidator-issues"></a>已知 ApiValidator 问题

* ApiValidator 不能在 ARM64 上运行，因为 AitStatic 不能在 ARM64 上运行。
* ARM64 二进制文件可以在 x64 计算机上测试，但不能在 x86 计算机上测试。
* ApiValidator 可以在 x86 上运行，以测试 x86 二进制文件和 ARM 二进制文件。
* ApiValidator 可以在 x64 上运行，以测试 x86、x64、ARM 和 ARM64 二进制文件。



