---
title: Inf2Cat
description: 'Inf2Cat ( # A0) 是一个命令行工具，用于确定是否可以为指定的 Windows 版本列表对驱动程序包的 INF 文件进行数字签名。'
ms.assetid: 5d85058e-4051-4321-a4c1-b1a71d232b7f
keywords:
- Inf2Cat 驱动程序开发工具
topic_type:
- apiref
api_name:
- Inf2Cat
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a21c66a41b19952829dde2ee87bb94ddb62436ca
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89383509"
---
# <a name="inf2cat"></a>Inf2Cat

Inf2Cat ( # A0) 是一个命令行工具，用于确定是否可以为指定的 Windows 版本列表对 [驱动程序包的](../install/driver-packages.md) INF 文件进行数字签名。 如果是这样，Inf2Cat 将生成适用于指定 Windows 版本的未签名的 [目录文件](../install/catalog-files.md) 。

```command
    Inf2Cat /driver:
    PackagePath
     /os:
    WindowsVersionList [/nocat] [/verbose] [/?] [other switches]
```

> [!TIP]
> 如果你在 `DriverVer set to a date in the future` 构建驱动程序时看到，请更改驱动程序包项目设置，以便 Inf2Cat 设置 `/uselocaltime` 。 为此，请使用“配置属性”->“Inf2Cat”->“常规”->“使用本地时间”。 现在，[Stampinf](stampinf-command-options.md) 和 Inf2Cat 都使用本地时间。

Inf2Cat 工具位于 Program Files \\ Windows 工具包 \\ 8.0 \\ Bin \\ x86 或 program files (x86) \\ windows 工具包 \\ 8.0 \\ bin \\ x86 文件夹中。

## <a name="switches-and-arguments"></a>开关和参数

**/driver：**<em>PackagePath</em>  
指定包含驱动程序包 INF 文件的目录的路径。 如果指定的目录包含多个驱动程序包的 INF 文件，Inf2Cat 将为每个驱动程序包创建编录文件。

> [!NOTE]
> 可以使用 **/drv：** 开关代替 **/driver：** 开关。

**/nocat**  
将 Inf2Cat 配置为验证 [驱动程序包](../install/driver-packages.md) 是否符合指定 Windows 版本的签名要求，但不生成目录文件。

**/os：**<em>WindowsVersionList</em>  
将 Inf2Cat 配置为验证 [驱动程序包的](../install/driver-packages.md) INF 文件是否符合 *WindowsVersionList*指定的 Windows 版本的签名要求。 *WindowsVersionList* 是一个以逗号分隔的列表，其中包含一个或多个以下版本标识符。

|Windows 版本|版本标识符|
|--- |--- |
|Windows 10 x86 19H1 Edition|10_19H1_X86|
|Windows 10 x64 19H1 Edition|10_19H1_X64|
|Windows 10 ARM64 19H1 Edition|10_19H1_ARM64|
|Windows 10 x86 RS5 Edition|10_RS5_X86|
|Windows 10 x64 RS5 Edition|10_RS5_X64|
|Windows 10 ARM64 RS5 Edition|10_RS5_ARM64|
|Windows Server RS5 x64 Edition|ServerRS5_X64|
|Windows Server RS5 ARM64 Edition|ServerRS5_ARM64|
|Windows 10 x86 RS4 Edition|10_RS4_X86|
|Windows 10 x64 RS4 Edition|10_RS4_X64|
|Windows 10 ARM64 RS4 Edition|10_RS4_ARM64|
|Windows 10 x86 RS3 Edition|10_RS3_X86|
|Windows 10 x64 RS3 Edition|10_RS3_X64|
|Windows 10 ARM64 RS3 Edition|10_RS3_ARM64|
|Windows 10 x86 RS2 Edition|10_RS2_X86|
|Windows 10 x64 RS2 Edition|10_RS2_X64|
|Windows 10 x86 RS1 Edition|10_AU_X86|
|Windows 10 x64 RS1 Edition|10_AU_X64|
|Windows Server 2016 x64 Edition|SERVER2016_X64|
|Windows 10 x86 Edition|10_X86|
|Windows 10 x64 Edition|10_X64|
|Windows Server 2016|Server10_X64|
|ARM 上的 Windows Server 2016|Server10_ARM64|
|Windows 8.1 x86 Edition|6_3_X86|
|Windows 8.1 x64 Edition|6_3_X64|
|Windows 8.1 ARM Edition|6_3_ARM|
|Windows Server 2012 R2|Server6_3_X64|
|Windows 8 x64 版本|8_X64|
|Windows 8 x86 版|8_X86|
|Windows 8 ARM 版本|8_ARM|
|Windows Server 2012|Server8_X64|
|Windows Server 2008 R2 x64 Edition|Server2008R2_X64|
|Windows Server 2008 R2 Itanium 版|Server2008R2_IA64|
|Windows 7 x64 版本|7_X64|
|Windows 7 x86 版|7_X86|
|Windows Server 2008 x64 Edition|Server2008_X64|
|Windows Server 2008 Itanium 版|Server2008_IA64|
|Windows Server 2008 x86 版|Server2008_X86|
|Windows Vista x64 版本|Vista_X64|
|Windows Vista x86 版|Vista_X86|
|Windows XP x64 版本|XP_X64|
|Windows XP x86 版|XP_X86|
|Windows Server 2003 x64 Edition|Server2003_X64|
|Windows Server 2003 Itanium 版|Server2003_IA64|
|Windows Server 2003 x86 版|Server2003_X86|

> [!NOTE]
> 从 Windows Server 2008 R2 开始，Windows server 操作系统将不再支持基于 x86 的平台。

Inf2Cat 忽略版本标识符字符串的字母字符的大小写。 例如，vista \_ x64 和 vista \_ x64 都是适用于 Windows Vista x64 版本的有效标识符。

**/uselocaltime**  
在运行驱动程序时间戳验证测试时使用本地时区。 默认情况下，使用 UTC。

**/nocat**  
禁止 () 创建目录。

**/verbose**  
配置 Inf2Cat 以在命令窗口中显示详细信息。

**/?**  
配置 Inf2Cat 以在命令窗口中显示帮助信息。

**/drm**  
*不推荐使用的命令行参数。*  
将 drm 签名特性添加到 .inf 文件中以添加 drm 签名属性。

**/pe**  
*不推荐使用的命令行参数。*  
将 petrust 签名特性添加到 .inf 文件中，以添加 petrust 签名特性。

**/pageHashes**  
在文件中包含页面哈希。  可选择性地后跟文件列表。

## <a name="comments"></a>注释

Inf2Cat 工具已替换 Windows Vista 之前的 WDK 版本中包含的 Signability 工具。

若要使用 Inf2Cat，你必须是系统上 Administrators 组的成员。

Inf2Cat 工具将检查 [驱动程序包](../install/driver-packages.md) 的 .inf 文件中的结构错误，并验证驱动程序包是否可以进行数字签名。 只有在 INF 文件中引用的所有文件都存在并且源文件位于正确的位置时，才能对驱动程序包进行签名。 如果无法对 INF 文件进行签名，或者如果它包含结构性错误，则驱动程序包可能未正确安装，或者在安装过程中可能会错误地显示 "驱动程序签名警告" 对话框。

只有在驱动程序包的 INF 文件中指定了目录文件，并且目录文件适用于一个或多个指定的 Windows 版本时，Inf2Cat 才会生成 [目录](../install/catalog-files.md) 文件。 如果 INF 文件的 [**Inf 版本部分**](../install/inf-version-section.md) 仅提供 **CatalogFile =**<em>filename.cat</em> 指令，则该目录文件适用于整个驱动程序包。 为了支持[跨平台安装](../install/creating-inf-files-for-multiple-platforms-and-operating-systems.md)，INF 文件应包含**CatalogFile。**<em>PlatformExtension</em> **=**<em>unique-filename.cat</em>指令。

有关签署驱动程序包的详细信息，请参阅 [驱动程序签名](../install/driver-signing.md) 和 [设备和驱动程序安装基本主题](https://docs.microsoft.com/windows-hardware/drivers/install/device-and-driver-installation-fundamental-topics)。

## <a name="examples"></a>示例

在下面的示例中，c： \\ MyDriver 包含一个其 inf 文件为 MyInfFile 的 [驱动程序包](../install/driver-packages.md) ，inf 文件中的 inf 版本部分仅包含以下 **CatalogFile** 指令：

```command
[Version]
. . .
CatalogFile=MyCatalogFile.cat
. . .
```

在此示例中，以下 Inf2Cat 命令将验证是否可以为 Windows 2000 和 x86 版本的 Windows Vista、Windows Server 2003 和 Windows XP 签署驱动程序包。 如果可以对这些版本对包进行签名，Inf2Cat 会创建未签名的目录文件 MyCatalogFile.cat。

```command
Inf2Cat /driver:C:\MyDriver /os:2000,XP_X86,Server2003_X86,Vista_X86
```

在下面的示例中，c： \\ MyDriver 包含一个其 inf 文件为 MyInfFile 的 [驱动程序包](../install/driver-packages.md) ，inf 文件中的 inf **版本** 部分仅包含以下两个带有平台扩展的 **CatalogFile** 指令：

```command
[Version]
. . .
CatalogFile.ntx86=MyCatalogFileX86.cat
CatalogFile.ntamd64=MyCatalogFileX64.cat
. . .
```

在此示例中，以下 Inf2Cat 命令将验证是否可以为 Windows 2000 和 x86 版本的 Windows Vista、Windows Server 2003 和 Windows XP 签署驱动程序包。 此外，该命令还将验证是否可以为 Windows Vista、Windows Server 2003 和 Windows XP x64 版本签署驱动程序包。 如果可以对所有这些版本的包进行签名，Inf2Cat 会创建 MyCatalogFileX86.cat 和 MyCatalogFileX64.cat 的未签名的目录文件。

```command
Inf2Cat /driver:C:\MyDriver /os:2000,XP_X86,XP_X64,Server2003_X86,Server2003_X64,Vista_X86,Vista_X64
```

有关如何使用 Inf2Cat 创建编录文件的详细信息，请参阅为 [PnP 驱动程序包创建编录文件](../install/creating-a-catalog-file-for-a-pnp-driver-package.md)。