---
title: Microsoft ASL 编译器
description: Microsoft ASL 编译器版本 5.0 ACPI 5.0 规范中支持的功能。
ms.assetid: E6EC168F-DB4B-461A-874A-F5278E8F9200
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 307ced356e9347b38cd320038465ba5ebff79e6c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337538"
---
# <a name="microsoft-asl-compiler"></a>Microsoft ASL 编译器


5.0 版本的 Microsoft ACPI 源语言 (ASL) 编译器支持高级配置和电源接口规范，修订版本 5.0 中的功能 ([ACPI 5.0 规范](https://www.uefi.org/specifications))。 ASL 编译器都会使用 Windows Driver Kit (WDK)。 查找工具中 Asl.exe 可执行文件\\arm\\ACPIVerify、 工具\\arm64\\ACPIVerify、 工具\\x86\\ACPIVerify 或工具\\x64\\ACPIVerify 安装 WDK 目录。

## <a name="command-line-options"></a>命令行选项


Microsoft ASL 编译器支持多个命令行选项。 若要列出可用命令行选项，请运行命令"`asl /?`"命令提示符窗口中。

### <a name="usage"></a>用法

ASL 编译器支持下列命令行选项：

```console
asl /?
asl [/nologo] /d <BinFile>
asl [/nologo] /u [/Fa=<ASMFile>] [/Fl=<LSTFile>] [/Fn=<NSDFile>] <AMLFile>
asl [/nologo] /tab=<TabSig> [/c] [/Fa=<ASMfile>] [/Fl=<LSTFile>] [/Fn=<NSDFile>]
asl [/nologo] [/Fo=<AMLFile>] [/Fa=<ASMFile>] [/Fl=<LSTFile>] [/Fn=<NSDFile>] <ASLFile>
```

| Option             | 描述                                                                   |
|--------------------|-------------------------------------------------------------------------------|
| ?                  | 打印此帮助消息。                                                      |
| nologo             | 禁止显示徽标横幅。                                                     |
| Fo=&lt;AMLFile&gt; | 重写中 DefinitionBlock 的 AML 文件名称。                            |
| Fa=&lt;ASMFile&gt; | 生成。ASM 文件同名&lt;ASMFile&gt;。                           |
| Fn=&lt;NSDFile&gt; | 生成具有名称的命名空间转储文件&lt;NSDFile&gt;。                 |
| d                  | 转储以文本形式的二进制文件。                                            |
| u                  | 反汇编的 AML 文件。ASL 文件 （默认值） 或。LST 文件。               |
| tab=&lt;TabSig&gt; | 反汇编 ASL 表。ASL 文件 （默认值） 或。LST 文件。 转储到非 ASL 表。TXT 文件。 如果&lt;TabSig&gt;是\*，所有表都转储到 ACPI。TXT。 &lt;TabSig&gt;也可以是表的物理地址。 |
| c                  | 从表中创建的二进制文件。                                              |

 
## <a name="using-the-microsoft-asl-compilers-acpi-table-load-feature"></a>使用 Microsoft ASL 编译器的 ACPI 表加载功能

系统在开发期间，最好有一种方法来模拟各种 ACPI BIOS 构造和开发系统上对其进行测试。 Windows 操作系统允许某些 ACPI 表要从 Windows 注册表，而不是从 PC 的 BIOS rom。 加载 使用此功能需要管理员权限，还需要在系统上启用测试签名。 对于支持 UEFI 安全引导的系统，不能启用测试签名，并且除非禁用 UEFI 安全引导或系统上安装 Windows 调试策略不能使用编译器的表加载功能。

若要使用表加载功能，要重载的 ACPI 表必须满足以下要求：

-   要重载的表必须已经存在于系统的 BIOS rom。 例如，可以重载 DSDT;但是，如果计算机不具有 SSDT，不能强制 SSDT 加载从该注册表替代机制。
-   表必须包含通常由 Windows ACPI 解释器 （Acpi.sys 驱动程序） 的 AML 代码。
-   将加载具有最高版本号的表。 加载到用于测试的注册表中的表必须具有更高版本的版本号高于在同一个表，在 BIOS ROM 中。
-   要加载的表必须是已编译 (AML) 格式和加载到注册表中正确的位置，使用指定的正确参数。 此处所述的机制可以处理加载表和注册表配置的所有方面。

> [!WARNING]
> 本主题中所述的过程可能会使 Windows 系统处于不可启动状态。 确保尝试此处所述的过程之前，在同一台计算机上有对另一个操作系统支持 NTFS 文件系统 （即，"安全生成"） 的访问权限。 此过程为 system 开发人员和测试人员仅提供，不应进行开发或生产重要的任何计算机上使用。


### <a name="usage"></a>用法

若要将 ACPI 表加载到注册表中为测试目的，ASL 编译器调用，如下所示：

```console
asl.exe /loadtable [-v] [-d] <AMLFile>
```

其中 AMLFile 是编译 AML 文件包含你想要加载到注册表的表的名称。

| Option  | 描述                                                                                              |
|---------|----------------------------------------------------------------------------------------------------------|
| -v      | 详细模式。 打开从实用程序的额外的调试输出。                                          |
| -d      | “删除”。 从注册表中，删除先前加载的 AML 文件并删除所有相关的注册表项。|


## <a name="additional-resources"></a>其他资源

-   [ACPICA 文档](https://acpica.org/documentation/)
-   [ACPI 网站](https://www.uefi.org/specifications/)
-   [ACPI 调试](https://msdn.microsoft.com/library/windows/hardware/ff537808)
-   [Acpi.sys:Windows ACPI 驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff540493)
-   [电源管理和 ACPI](https://msdn.microsoft.com/library/windows/hardware/dn614610)

