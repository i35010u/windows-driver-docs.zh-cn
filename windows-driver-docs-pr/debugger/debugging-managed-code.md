---
title: 使用 Windows 调试器调试托管代码
description: 可以使用 windows 调试器 （WinDbg、 CDB 和 NTSD） 调试包含托管的代码的目标应用程序。
ms.assetid: eb4cc883-71ac-4a57-8654-07c3120310c0
keywords: 调试时，调试 Windbg、 托管的代码调试、.NET 公共语言运行时、 公共语言运行时，CLR，JIT 编译器，实时编译的代码
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8edea69504ef1085bb2df54934350426a28e1a01
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350607"
---
# <a name="debugging-managed-code-using-the-windows-debugger"></a>使用 Windows 调试器调试托管代码


可以使用 Windows 调试器 （WinDbg、 CDB 和 NTSD） 调试包含托管的代码的目标应用程序。 若要调试托管的代码，必须加载[SOS 调试扩展 (sos.dll)](https://go.microsoft.com/fwlink/p/?linkid=223345)和数据访问组件 (mscordacwks.dll)。

Windows 调试器是独立于 Visual Studio 调试器。 有关 Windows 调试器和 Visual Studio 调试器之间的区别的信息，请参阅[Windows 调试](index.md)。

## <a name="span-idintroduction-to-managed-codespanspan-idintroductiontomanagedcodespanintroduction-to-managed-code"></a><span id="introduction-to-managed-code"></span><span id="INTRODUCTION_TO_MANAGED_CODE"></span>托管代码的简介


与 Microsoft.NET 公共语言运行时 (CLR) 一起执行托管的代码。 在托管代码应用程序中，编译器生成的二进制代码是在 Microsoft 中间语言 (MSIL)，即独立于平台的。

当运行托管的代码时，运行时生成特定于平台的本机代码。 从 MSIL 中生成本机代码的过程称为*实时 (JIT) 编译*。 JIT 编译器编译特定方法的 MSIL 后，该方法的本机代码保留在内存中。 此方法更高版本时调用，本机代码执行和 JIT 编译器不需要参与。

可以使用多种软件生成者而制造的多个编译器来生成托管的代码。 具体而言，Microsoft Visual Studio 可以生成多种不同语言，包括从托管的代码C#，Visual Basic、 JScript 中，和C++与托管扩展。

每次更新.NET Framework CLR 不会更新。 例如，版本 2.0、 3.0 和 3.5 的.NET Framework 的 clr 的所有使用版本 2.0。 下表显示的版本和使用的每个版本的.NET Framework 的 clr 的文件名。

| .NET framework 版本 | CLR 版本 | CLR 文件名 |
|------------------------|-------------|--------------|
| 1.1                    | 1.1         | mscorwks.dll |
| 2.0                    | 2.0         | mscorwks.dll |
| 3.0                    | 2.0         | mscorwks.dll |
| 3.5                    | 2.0         | mscorwks.dll |
| 4.0                    | 4.0         | clr.dll      |
| 4.5                    | 4.0         | clr.dll      |

 

## <a name="span-iddebugging-managedcodespanspan-iddebuggingmanagedcodespandebugging-managed-code"></a><span id="debugging-managed_code"></span><span id="DEBUGGING_MANAGED_CODE"></span>调试托管的代码


若要调试托管的代码，调试器必须加载这两个组件。

-   数据访问组件 (DAC) (mscordacwks.dll)
-   [SOS 调试扩展 (sos.dll)](https://go.microsoft.com/fwlink/p/?linkid=223345)

**请注意**  对于所有版本的.NET Framework 中，该 DAC 的文件名是 mscordacwks.dll，，SOS 调试扩展的文件名为 sos.dll。

 

### <a name="span-idgetting-the-sos-debugging-extensionspanspan-idgettingthesosdebuggingextensionspangetting-the-sos-debugging-extension-sosdll"></a><span id="getting-the-sos-debugging-extension"></span><span id="GETTING_THE_SOS_DEBUGGING_EXTENSION"></span>获取 SOS 调试扩展 (sos.dll)

SOS 调试扩展 (sos.dll) 文件中的 Windows 调试工具的当前版本不包括。

对于.NET Framework 2.0 及更高版本中，sos.dll 包括在.NET Framework 安装。

版本 1。*x*的.NET Framework 中，sos.dll 未包含在.NET Framework 安装。 若要获得.NET Framework 1 sos.dll。*x*，下载 32 位版本的 Windows 7 调试工具的 Windows。

Windows 7 调试工具的 Windows 包括在 Windows SDK 适用于 Windows 7 的位于以下两个位置：

-   [Windows SDK for Windows 7 和.NET Framework 4.0](https://go.microsoft.com/fwlink/p?LinkId=320327)
-   [Windows SDK for Windows 7 和.NET Framework 4.0 (ISO)](https://go.microsoft.com/fwlink/p?LinkId=320328)

如果运行的 x64 版本的 Windows，使用[ISO](https://go.microsoft.com/fwlink/p?LinkID=320328)站点，以便您可以指定所需的 sdk 的 32 位版本。 Sos.dll 仅包括在 Windows 7 调试工具的 Windows 的 32 位版本。

### <a name="span-idloadingmscordacwksdllandsosdlllivedebuggingspanspan-idloadingmscordacwksdllandsosdlllivedebuggingspanspan-idloadingmscordacwksdllandsosdlllivedebuggingspanloading-mscordacwksdll-and-sosdll-live-debugging"></a><span id="Loading_mscordacwks.dll_and_sos.dll__live_debugging_"></span><span id="loading_mscordacwks.dll_and_sos.dll__live_debugging_"></span><span id="LOADING_MSCORDACWKS.DLL_AND_SOS.DLL__LIVE_DEBUGGING_"></span>正在加载 mscordacwks.dll 和 sos.dll （实时调试）

假定在同一台计算机上运行调试器和正在调试的应用程序。 然后应用程序使用.NET Framework 的计算机上安装并可供调试器。

调试器必须加载的 CLR 的托管代码应用程序使用的版本相同的 dac 的版本。 也必须匹配的位数 （32 位或 64 位）。 DAC (mscordacwks.dll) 提供了.NET Framework。 若要加载正确版本的 DAC，请将调试器附加到托管代码应用程序，并输入以下命令。

**.cordll -ve -u -l**

输出应类似于此。

```dbgcmd
CLRDLL: Loaded DLL C:\Windows\Microsoft.NET\Framework64\v4.0.30319\mscordacwks.dll
CLR DLL status: Loaded DLL C:\Windows\Microsoft.NET\Framework64\v4.0.30319\mscordacwks.dll
```

若要验证 mscordacwks.dll 版本与应用程序使用的 clr 的版本相匹配，请输入以下命令以显示有关已加载的 CLR 模块信息之一。

**lmv mclr** （适用于 CLR 版本 4.0）

**lmv mscorwks** （适用于版本 1.0 或 2.0 CLR）

输出应类似于此。

```dbgcmd
start             end                 module name
000007ff`26710000 000007ff`2706e000   clr        (deferred)             
    Image path: C:\Windows\Microsoft.NET\Framework64\v4.0.30319\clr.dll
...
```

在前面的示例，请注意，CLR (clr.dll) 的版本与 DAC (mscordacwks.dll) 的版本相匹配： v4.0.30319。 另请注意这两个组件都是 64 位。

当你使用[ **.cordll** ](-cordll--control-clr-debugging-.md)加载 DAC，SOS 调试扩展 (sos.dll) 可能会获取自动加载。 如果不会自动加载 sos.dll，可以使用以下命令之一以加载它。

**.loadby sos clr** （适用于 CLR 版本 4.0）

**.loadby sos mscorwks** （适用于版本 1.0 或 2.0 CLR）

为使用的替代方法[ **.loadby**](-load---loadby--load-extension-dll-.md)，可以使用 **.load**。 例如，若要加载的 64 位 CLR 版本 4.0，可以输入类似于以下的命令。

**.load c:\\Windows\\Microsoft.NET\\Framework64\\v4.0.30319\\sos.dll**

在上面的输出，请注意，SOS 调试扩展 (sos.dll) 的版本匹配的 CLR 和 DAC 的版本： v4.0.30319。 另请注意所有三个组件都是 64 位。

### <a name="span-idloadingmscordacwksdllandsosdlldumpfilespanspan-idloadingmscordacwksdllandsosdlldumpfilespanspan-idloadingmscordacwksdllandsosdlldumpfilespanloading-mscordacwksdll-and-sosdll-dump-file"></a><span id="Loading_mscordacwks.dll_and_sos.dll__dump_file_"></span><span id="loading_mscordacwks.dll_and_sos.dll__dump_file_"></span><span id="LOADING_MSCORDACWKS.DLL_AND_SOS.DLL__DUMP_FILE_"></span>正在加载 mscordacwks.dll 和 sos.dll （转储文件）

假设您使用调试器打开转储文件 （托管代码应用程序） 的另一台计算机上创建。

调试器必须加载的 CLR 的托管代码应用程序正在使用另一台计算机上的版本相同的 dac 的版本。 也必须匹配的位数 （32 位或 64 位）。

DAC (mscordacwks.dll) 附带了.NET Framework 中，但让我们假定您没有运行调试器的计算机上安装了.NET Framework 的正确版本。 有三个选项。

-   从符号服务器加载 DAC。 例如，您可以在你的符号路径包括 Microsoft 公共符号服务器。
-   运行调试器的计算机上安装.NET Framework 的正确版本。
-   从创建转储文件 （在另一台计算机） 的人员获取 mscordacwks.dll 的正确版本，并手动将其复制到正在运行调试器的计算机。

下面将演示使用 Microsoft 公共符号服务器。

输入以下命令。

**.sympath + srv\\*** （添加到符号路径的符号服务器）。

**！ 干扰性的符号**

**.cordll -ve -u -l**

输出将类似于此。

```dbgcmd
CLRDLL: Unable to get version info for 'C:\Windows\Microsoft.NET
   \Framework64\v4.0.30319\mscordacwks.dll', Win32 error 0n87

SYMSRV:  C:\ProgramData\dbg\sym\mscordacwks_AMD64_AMD64_4.0.30319.18010.dll
   \5038768C95e000\mscordacwks_AMD64_AMD64_4.0.30319.18010.dll not found

SYMSRV:  mscordacwks_AMD64_AMD64_4.0.30319.18010.dll from 
   https://msdl.microsoft.com/download/symbols: 570542 bytes - copied         
...
SYMSRV:  C:\ProgramData\dbg\sym\SOS_AMD64_AMD64_4.0.30319.18010.dll
   \5038768C95e000\SOS_AMD64_AMD64_4.0.30319.18010.dll not found

SYMSRV:  SOS_AMD64_AMD64_4.0.30319.18010.dll from 
   https://msdl.microsoft.com/download/symbols: 297048 bytes - copied         
...
Automatically loaded SOS Extension
...
```

在上面的输出中可以看到调试器首先寻找 mscordacwks.dll 和 c： 驱动器中在本地计算机上的 sos.dll\\Windows\\Microsoft.NET 和符号缓存中 (c:\\ProgramData\\dbg\\符号)。 当调试器找不到本地计算机上的文件的正确版本时，它可以从公共符号服务器检索它们。

若要验证 mscordacwks.dll 版本与应用程序正在使用的 clr 的版本相匹配，请输入以下命令以显示有关已加载的 CLR 模块信息之一。

**lmv mclr** （适用于 CLR 版本 4.0）

**lmv mscorwks** （适用于版本 1.0 或 2.0 CLR）

输出应类似于此。

```dbgcmd
start             end                 module name
000007ff`26710000 000007ff`2706e000   clr        (deferred)             
    Image path: C:\Windows\Microsoft.NET\Framework64\v4.0.30319\clr.dll
...
```

在前面的示例，请注意，CLR (clr.dll) 的版本与 DAC (mscordacwks.dll) 的版本相匹配： v4.0.30319。 另请注意这两个组件都是 64 位。

### <a name="span-idusingthesosdebuggingextensionspanspan-idusingthesosdebuggingextensionspanspan-idusingthesosdebuggingextensionspanusing-the-sos-debugging-extension"></a><span id="Using_the_SOS_Debugging_Extension_"></span><span id="using_the_sos_debugging_extension_"></span><span id="USING_THE_SOS_DEBUGGING_EXTENSION_"></span>使用 SOS 调试扩展

若要验证的 SOS 调试扩展无法正确加载，请输入[ **.chain** ](-chain--list-debugger-extensions-.md)命令。

```dbgcmd
0:000> .chain
Extension DLL search Path:
...
Extension DLL chain:
    C:\ProgramData\dbg\sym\SOS_AMD64_AMD64_4.0.30319.18010.dll\...
        ...
    dbghelp: image 6.13.0014.1665, API 6.2.6, built Wed Dec 12 03:02:43 2012
...
```

若要测试 SOS 调试扩展，请输入 **！ sos.help**。 请尝试通过将 SOS 调试扩展提供的命令之一。 例如，可以尝试 **！ sos。DumpDomain**或 **！ sos。线程**命令。

### <a name="span-idnotesspanspan-idnotesspanspan-idnotesspannotes"></a><span id="Notes"></span><span id="notes"></span><span id="NOTES"></span>说明

有时托管代码应用程序加载的 clr 的多个版本。 在这种情况下，必须指定要加载的 DAC 的版本。 有关详细信息，请参阅[ **.cordll**](-cordll--control-clr-debugging-.md)。

 

 





