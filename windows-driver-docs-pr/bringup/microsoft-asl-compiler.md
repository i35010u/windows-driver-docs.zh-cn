---
title: Microsoft ASL 编译器
description: Microsoft ASL 编译器版本5.0 支持 ACPI 5.0 规范中的功能。
ms.date: 12/17/2020
ms.localizationpriority: medium
ms.openlocfilehash: 54fd399644998d6a8866976432bc00401f7049fe
ms.sourcegitcommit: 10fecd036370f5eccb538004c5bec1fdd18c3275
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/12/2021
ms.locfileid: "98124113"
---
# <a name="microsoft-asl-compiler"></a>Microsoft ASL 编译器

Microsoft ACPI 源语言 (版本 5.0 ASL) 编译器支持高级配置和电源接口规范中的功能，修订 5.0 ([ACPI 5.0 规范](https://uefi.org/specifications)) 。 ASL 编译器随 Windows 驱动程序工具包 (WDK) 一起分发。

[**下载 Windows 驱动程序工具包 (WDK)**](../download-the-wdk.md)

ASL 编译器 (asl.exe) 位于已安装的 WDK 的 Tools\\arm\\ACPIVerify、Tools\\arm64\\ACPIVerify、Tools\\x86\\ACPIVerify 和 Tools\\x64\\ACPIVerify 目录中，例如 C:\Program Files (x86)\Windows Kits\10\Tools\x86\ACPIVerify。

## <a name="command-line-options"></a>命令行选项

ASL 编译器支持多个命令行选项。 若要列出版本信息和可用的命令行选项，请 `asl /?` 在命令提示符窗口中运行命令 ""。

### <a name="asl-compiler-usage"></a>ASL 编译器用法

ASL 编译器支持以下命令行选项：

```console
asl /?
asl [/nologo] /d <BinFile>
asl [/nologo] /u [/Fa=<ASMFile>] [/Fl=<LSTFile>] [/Fn=<NSDFile>] <AMLFile>
asl [/nologo] /tab=<TabSig> [/c] [/Fa=<ASMfile>] [/Fl=<LSTFile>] [/Fn=<NSDFile>]
asl [/nologo] [/Fo=<AMLFile>] [/Fa=<ASMFile>] [/Fl=<LSTFile>] [/Fn=<NSDFile>] <ASLFile>
```

| 选项 | 描述 |
|--|--|
| ? | 打印此帮助消息。 |
| nologo | 禁止显示徽标横幅。 |
| Fo = &lt; AMLFile&gt; | 重写 DefinitionBlock 中的 AML 文件名。 |
| Fa = &lt; ASMFile&gt; | 生成。名称为 ASMFile 的 ASM &lt; 文件 &gt; 。 |
| Fn = &lt; NSDFile&gt; | 生成名为 NSDFile 的命名空间转储 &lt; 文件 &gt; 。 |
| d | 以文本格式转储二进制文件。 |
| u | 将 AML 文件 Unassemble 到。ASL 文件 (默认) 或。.LST 文件。 |
| tab = &lt; TabSig&gt; | Unassemble ASL 表。ASL 文件 (默认) 或。.LST 文件。 将非 ASL 表转储到。TXT 文件。 如果 &lt; TabSig &gt; 是 " \* "，则所有表都转储到 ACPI.TXT。 &lt;TabSig &gt; 也可以是表的物理地址。 |
| c | 从表中创建二进制文件。 |

## <a name="using-the-microsoft-asl-compilers-acpi-table-load-feature"></a>使用 Microsoft ASL 编译器的 ACPI-表加载功能

在系统开发过程中，有一种方法可以模拟各种 ACPI BIOS 构造，并在开发系统中对其进行测试。 Windows 操作系统允许从 Windows 注册表而不是从 PC 的 BIOS ROM 加载某些 ACPI 表。 使用此功能需要管理员权限，并且还要求在系统上启用测试签名。 对于支持 UEFI 安全启动的系统，无法启用测试签名，并且不能使用编译器的表加载功能，除非禁用了 UEFI 安全启动或在系统上安装了 Windows 调试策略。

若要使用表加载功能，要重载的 ACPI 表必须满足以下要求：

- 要重载的表在系统的 BIOS ROM 中必须已经存在。 例如，DSDT 可以重载;但是，如果计算机没有 SSDT，则不能强制从该注册表替代机制加载 SSDT。

- 此表必须包含 Windows ACPI 解释器 (Acpi.sys 驱动程序) 通常使用的 AML 代码。

- 将加载版本号最高的表。 加载到注册表中用于测试的表的版本号必须高于 BIOS ROM 中的相同表版本号。

- 要加载的表必须位于编译 (AML) 格式，并加载到正确位置的注册表中，并且指定了正确的参数。 本文中所述的机制旨在处理加载表和配置注册表的各个方面。

> [!WARNING]
> 本主题中所述的过程可能使您的 Windows 系统处于无法启动状态。 确保你有权访问具有 NTFS 文件系统支持的另一操作系统， (即，在尝试此处列出的过程之前，同一计算机上的 "安全生成" ) 。 此过程仅针对系统开发人员和测试人员提供，不应用于任何对开发或生产用途至关重要的计算机。

### <a name="acpi-table-load-usage"></a>ACPI-表加载使用情况

要出于测试目的将 ACPI 表加载到注册表中，请按如下所示调用 ASL 编译器：

```console
asl.exe /loadtable [-v] [-d] <AMLFile>
```

其中，AMLFile 是已编译的 AML 文件的名称，其中包含要加载到注册表中的表。

| 选项 | 描述 |
|--|--|
| -v | 详细模式。 启用实用工具的额外调试输出。 |
| -d | 删除。 从注册表中删除以前加载的 AML 文件，并删除所有关联的注册表项。 |

## <a name="additional-resources"></a>其他资源

- [ACPICA 文档](https://acpica.org/documentation/)

- [ACPI 规范](https://uefi.org/specifications/)

- [ACPI 调试](../debugger/acpi-debugging.md)

- [Acpi.sysWindows ACPI 驱动程序](../kernel/acpi-driver.md)

- [电源管理和 ACPI](/previous-versions/windows/hardware/design/dn614610(v=vs.85))