---
title: 使用 Windows 调试器调试托管代码
description: 可以使用 windows 调试器 (WinDbg、CDB 和 NTSD) 调试包含托管代码的目标应用程序。
ms.assetid: eb4cc883-71ac-4a57-8654-07c3120310c0
keywords: 调试，调试，Windbg，托管代码调试，.NET 公共语言运行时，公共语言运行时，CLR，JIT 编译器，实时编译代码
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 022e2daa59166a43ad78a4786ba4d8dd6c20b4ce
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213481"
---
# <a name="debugging-managed-code-using-the-windows-debugger"></a>使用 Windows 调试器调试托管代码

可以使用 Windows 调试器 (WinDbg、CDB 和 NTSD) 调试包含托管代码的目标应用程序。 若要调试托管代码，必须加载 [SOS 调试扩展 ( # A0) ](/dotnet/framework/tools/sos-dll-sos-debugging-extension) 和 ( # A1) 的数据访问组件。

Windows 调试器独立于 Visual Studio 调试器。 有关 Windows 调试器和 Visual Studio 调试器之间的区别的信息，请参阅 [Windows 调试](index.md)。

## <a name="introduction-to-managed-code"></a>托管代码简介

托管代码与 Microsoft .NET 公共语言运行时 (CLR) 一起执行。 在托管代码应用程序中，编译器生成的二进制代码为 Microsoft 中间语言 (MSIL) ，后者独立于平台。

运行托管代码时，运行时将生成特定于平台的本机代码。 从 MSIL 生成本机代码的过程称为 "实时 * (JIT) 编译*"。 JIT 编译器编译了特定方法的 MSIL 后，该方法的本机代码将保留在内存中。 以后调用此方法时，本地代码执行，并且 JIT 编译器不必涉及。

您可以使用多个软件创建者制造的多个编译器生成托管代码。 具体而言，Microsoft Visual Studio 可以从多种不同的语言（包括 c #、Visual Basic、JScript 和 c + + 以及托管扩展）生成托管代码。

每次更新 .NET Framework 时，不会更新 CLR。 例如，版本2.0、3.0 和 3.5 .NET Framework 都使用 CLR 版本2.0。 下表显示了每个版本的 .NET Framework 所使用的 CLR 的版本和文件名。

| .NET Framework 版本 | CLR 版本 | CLR 文件名 |
|------------------------|-------------|--------------|
| 1.1                    | 1.1         | mscorwks.dll |
| 2.0                    | 2.0         | mscorwks.dll |
| 3.0                    | 2.0         | mscorwks.dll |
| 3.5                    | 2.0         | mscorwks.dll |
| 4.0                    | 4.0         | clr.dll      |
| 4.5                    | 4.0         | clr.dll      |

## <a name="debugging-managed-code"></a>调试托管代码

若要调试托管代码，调试器必须加载这两个组件。

- 数据访问组件 (DAC)  ( # A0) 
- [SOS 调试扩展 ( # A0) ](/dotnet/framework/tools/sos-dll-sos-debugging-extension)

**注意**   对于所有版本的 .NET Framework，将 mscordacwks.dll DAC 的文件名，并 sos.dll SOS 调试扩展的文件名。

### <a name="getting-the-sos-debugging-extension-sosdll"></a>正在获取 SOS 调试扩展 ( # A0) 

在 Windows 调试工具的当前版本中，SOS 调试扩展 ( # A0) 文件不包括在内。

对于 .NET Framework 版本2.0 及更高版本，.NET Framework 安装中包含 sos.dll。

用于版本1。.NET Framework 的*x* ，.NET Framework 安装中未包含 sos.dll。 获取 .NET Framework 1 sos.dll。*x*下载适用于 Windows 的 Windows 7 调试工具的32位版本。

适用于 windows 7 的 windows 7 调试工具包含在 Windows 7 的 Windows SDK 中，这两个位置可用：

- [适用于 Windows 7 和 .NET Framework 4.0 的 Windows SDK](https://www.microsoft.com/download/details.aspx?id=8279)
- [适用于 Windows 7 和 .NET Framework 4.0 (ISO) 的 Windows SDK ](https://www.microsoft.com/download/details.aspx?id=8442)

如果你运行的是 x64 版本的 Windows，则使用 [ISO](https://www.microsoft.com/download/details.aspx?id=8442)，以便可以指定你想要使用32位版本的 SDK。 Sos.dll 仅包含在适用于 Windows 的 Windows 7 调试工具32位版本中。

### <a name="loading-mscordacwksdll-and-sosdll-live-debugging"></a>加载 mscordacwks.dll 和 sos.dll (实时调试) 

假设调试器和正在调试的应用程序在同一台计算机上运行。 然后，应用程序使用的 .NET Framework 安装在计算机上，并可供调试器使用。

调试器必须加载与托管代码应用程序正在使用的 CLR 版本相同的 DAC 版本。  (32 位或64位) 的位数也必须匹配。 DAC ( # A0) 附带了 .NET Framework。 若要加载正确的 DAC 版本，请将调试器附加到托管代码应用程序，然后输入此命令。

**。 cordll-i-u-l**

输出应类似于此。

```dbgcmd
CLRDLL: Loaded DLL C:\Windows\Microsoft.NET\Framework64\v4.0.30319\mscordacwks.dll
CLR DLL status: Loaded DLL C:\Windows\Microsoft.NET\Framework64\v4.0.30319\mscordacwks.dll
```

若要验证 mscordacwks.dll 的版本是否与应用程序所使用的 CLR 的版本相匹配，请输入以下命令之一以显示有关加载的 CLR 模块的信息。

适用于版本4.0 的 CLR) 的**lmv mclr** (

CLR) 版本1.0 或2.0 的**lmv mscorwks.dll** (

输出应类似于此。

```dbgcmd
start             end                 module name
000007ff`26710000 000007ff`2706e000   clr        (deferred)             
    Image path: C:\Windows\Microsoft.NET\Framework64\v4.0.30319\clr.dll
...
```

在前面的示例中，请注意，CLR 的版本 ( # A0) 与 DAC ( # A1) ： v 4.0.30319 的版本相匹配。 另请注意，这两个组件为64位。

使用 [**cordll**](-cordll--control-clr-debugging-.md) 加载 DAC 时，SOS 调试扩展 ( # A0) 可能会自动加载。 如果 sos.dll 不会自动加载，则可以使用其中一个命令将其加载。

loadby) 的 CLR 版本4.0 的**sos clr** (

**loadby sos mscorwks.dll** (，适用于 CLR) 的版本1.0 或2。0

作为使用[**loadby**](-load---loadby--load-extension-dll-.md)的替代方法，可以使用 **。** 例如，若要加载64位 CLR 版本4.0，你可以输入类似于下面的命令。

**。 load C： \\ Windows \\ Microsoft.NET \\ Framework64 \\ v 4.0.30319 \\sos.dll**

在上面的输出中，请注意，SOS 调试扩展的版本 ( # A0) 与 CLR 和 DAC： v 4.0.30319 的版本相匹配。 另请注意，所有这三个组件都是64位。

### <a name="loading-mscordacwksdll-and-sosdll-dump-file"></a>加载 mscordacwks.dll 和 sos.dll (转储文件) 

假设你使用调试器来打开 (在另一台计算机上创建的托管代码应用程序) 的转储文件。

调试器必须加载与托管代码应用程序在另一台计算机上使用的 CLR 版本相同的 DAC 版本。  (32 位或64位) 的位数也必须匹配。

DAC ( # A0) 附带了 .NET Framework，但假设你没有在运行调试器的计算机上安装正确的 .NET Framework 版本。 有三个选项。

- 从符号服务器加载 DAC。 例如，你可以在符号路径中包含 Microsoft 的公共符号服务器。
- 在运行调试器的计算机上安装 .NET Framework 的正确版本。
- 从在另一台计算机上创建转储文件 (的用户处获取 mscordacwks.dll 的正确版本) 然后将其手动复制到运行调试器的计算机。

这里介绍了如何使用 Microsoft 的公共符号服务器。

输入这些命令。

**. sympath + srv \\ *** (将符号服务器添加到符号路径。 ) 

**！符号干扰**

**。 cordll-i-u-l**

输出将与此类似。

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

在上面的输出中，可以看到调试器首先在本地计算机上的 C： Windows Microsoft.NET 和符号缓存中查找 mscordacwks.dll 和 sos.dll， \\ \\ (c： \\ ProgramData \\ dbg \\ 符号) 。 如果调试器在本地计算机上找不到正确版本的文件，则会从公共符号服务器检索这些文件。

若要验证 mscordacwks.dll 的版本是否与应用程序所使用的 CLR 的版本相匹配，请输入以下命令之一以显示有关加载的 CLR 模块的信息。

**lmv-**) 的 CLR 版本 4.0 (

**lmv-**) CLR 的版本1.0 或 2.0 (

输出应类似于此。

```dbgcmd
start             end                 module name
000007ff`26710000 000007ff`2706e000   clr        (deferred)             
    Image path: C:\Windows\Microsoft.NET\Framework64\v4.0.30319\clr.dll
...
```

在前面的示例中，请注意，CLR 的版本 ( # A0) 与 DAC ( # A1) ： v 4.0.30319 的产品版本相匹配。 另请注意，这两个组件为64位。

### <a name="using-the-sos-debugging-extension"></a>使用 SOS 调试扩展

若要验证是否已正确加载 SOS 调试扩展，请输入 [**链式**](-chain--list-debugger-extensions-.md) 命令。

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

若要测试 SOS 调试扩展，请输入 **！ SOS. help**。 然后尝试使用 SOS 调试扩展提供的命令之一。 例如，你可以尝试 **！ sos。DumpDomain** 或 **！ sos。Threads** 命令。

### <a name="notes"></a>说明

有时，托管代码应用程序会加载多个版本的 CLR。 在这种情况下，必须指定要加载的 DAC 版本。 有关详细信息，请参阅 [**cordll**](-cordll--control-clr-debugging-.md)。