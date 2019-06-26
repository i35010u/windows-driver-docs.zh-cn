---
title: Inf2Cat
description: Inf2Cat (Inf2Cat.exe) 是一个命令行工具，确定驱动程序包的 INF 文件是否可以为指定的 Windows 版本列表进行数字签名。
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
ms.openlocfilehash: 5f4ee273c8692c5fa71912079d2de8c71b8d5f5f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366817"
---
# <a name="inf2cat"></a>Inf2Cat

Inf2Cat (Inf2Cat.exe) 是一个命令行工具，确定是否[驱动程序包的](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)INF 文件可以是指定的 Windows 版本列表进行数字签名。 如果这样，Inf2Cat 生成无符号[编录文件](https://docs.microsoft.com/windows-hardware/drivers/install/catalog-files)，应用于指定的 Windows 版本。

```command
    Inf2Cat /driver:
    PackagePath
     /os:
    WindowsVersionList [/nocat] [/verbose] [/?] [other switches]
```

> [!TIP]
> 如果您看到`DriverVer set to a date in the future`时构建您的驱动程序，更改驱动程序程序包项目设置以便 Inf2Cat 设置`/uselocaltime`。 为此，请使用  “配置属性”->“Inf2Cat”->“常规”->“使用本地时间”。 现在，[Stampinf](stampinf-command-options.md) 和 Inf2Cat 都使用本地时间。

Inf2Cat 工具位于 Program Files\\Windows 工具包\\8.0\\bin\\x86 或 Program Files (x86)\\Windows 工具包\\8.0\\bin\\x86WDK 的文件夹。

## <a name="switches-and-arguments"></a>开关和参数

**/driver:** <em>PackagePath</em>  
指定包含驱动程序包的 INF 文件的目录的路径。 如果指定的目录中包含多个驱动程序包的 INF 文件，Inf2Cat 将创建每个驱动程序包的目录文件。

> [!NOTE]
> 可以使用 **/drv:** 切换来代替 **/driver:** 切换。

**/nocat**  
配置 Inf2Cat 以便确认[驱动程序包](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)符合指定的 Windows 的签名要求的版本中，但不是能生成目录文件。

**/os:** <em>WindowsVersionList</em>  
配置 Inf2Cat 以便确认[驱动程序包](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)INF 文件是否符合指定的 Windows 版本的签名要求*WindowsVersionList*。 *WindowsVersionList*是以逗号分隔的列表，包括一个或多个以下的版本标识符。

|Windows 版本|版本标识符|
|--- |--- |
|Windows 10 x86 19 H 1 版本|10_19H1_X86|
|Windows 10 x64 19 H 1 版本|10_19H1_X64|
|Windows 10 ARM64 19 H 1 版本|10_19H1_ARM64|
|Windows 10 x86 RS5 Edition|10_RS5_X86|
|Windows 10 x64 RS5 Edition|10_RS5_X64|
|Windows 10 ARM64 RS5 版|10_RS5_ARM64|
|Windows Server RS5 x64 Edition|ServerRS5_X64|
|Windows Server RS5 ARM64 Edition|ServerRS5_ARM64|
|Windows 10 x86 版 RS4 Edition|10_RS4_X86|
|Windows 10 x64 版 RS4 Edition|10_RS4_X64|
|Windows 10 ARM64 RS4 版|10_RS4_ARM64|
|Windows 10 x86 RS3 Edition|10_RS3_X86|
|Windows 10 x64 RS3 Edition|10_RS3_X64|
|Windows 10 ARM64 RS3 版|10_RS3_ARM64|
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
|Windows 8.1 ARM 版本|6_3_ARM|
|Windows Server 2012 R2|Server6_3_X64|
|Windows 8 x64 Edition|8_X64|
|Windows 8 x86 Edition|8_X86|
|Windows 8 ARM 版|8_ARM|
|Windows Server 2012|Server8_X64|
|Windows Server 2008 R2 x64 Edition|Server2008R2_X64|
|Windows Server 2008 R2 Itanium Edition|Server2008R2_IA64|
|Windows 7 x64 Edition|7_X64|
|Windows 7 x86 Edition|7_X86|
|Windows Server 2008 x64 Edition|Server2008_X64|
|Windows Server 2008 Itanium Edition|Server2008_IA64|
|Windows Server 2008 x86 Edition|Server2008_X86|
|Windows Vista x64 Edition|Vista_X64|
|Windows Vista x86 Edition|Vista_X86|
|Windows XP x64 Edition|XP_X64|
|Windows XP x86 Edition|XP_X86|
|Windows Server 2003 x64 Edition|Server2003_X64|
|Windows Server 2003 Itanium Edition|Server2003_IA64|
|Windows Server 2003 x86 Edition|Server2003_X86|

> [!NOTE]
> 从 Windows Server 2008 R2 开始，Windows server 操作系统将不再支持基于 x86 的平台。

Inf2Cat 忽略大小写的版本标识符字符串的字母字符。 例如，vista\_x64 和 Vista\_X64 是 Windows Vista x64 Edition 这两个有效标识符。

**/uselocaltime**  
运行驱动程序的时间戳验证测试时使用本地时区。 默认情况下使用 UTC。

**/nocat**  
将阻止这些目录的创建。

**/verbose**  
配置 Inf2Cat，在命令窗口中显示详细的信息。

**/?**  
配置 Inf2Cat 要在命令窗口中显示帮助信息。

**/drm**  
*不推荐使用的命令行参数。*  
若要添加 drm 签名特性的.inf 文件中添加 drm 签名特性。

**/pe**  
*不推荐使用的命令行参数。*  
若要添加 petrust 签名特性的.inf 文件中添加 petrust 签名属性。

**/pageHashes**  
在文件中包含页面哈希。  可选择性地后跟文件列表。

## <a name="comments"></a>备注

Inf2Cat 工具替换了已包括在 Windows Vista 之前的 wdk 版本 Signability 工具。

若要使用 Inf2Cat，您必须在系统上的 Administrators 组的成员。

Inf2Cat 工具检查[驱动程序包的](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)INF 文件的结构错误，并验证驱动程序包可以是数字签名。 仅当所有 INF 文件中引用的文件都存在且正确的位置是在源代码文件，可以进行签名的驱动程序包。 如果不能进行签名的 INF 文件或者它包含的结构错误，驱动程序包可能未正确安装，或可能会错误地显示驱动程序签名在安装过程中的警告对话框。

生成 Inf2Cat[编录文件](https://docs.microsoft.com/windows-hardware/drivers/install/catalog-files)才是驱动程序包的 INF 文件中指定的目录文件和目录文件适用于一个或多个指定的 Windows 版本。 如果[ **INF 版本部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-version-section)的 INF 文件将仅提供**CatalogFile =** <em>filename.cat</em>指令，该目录文件适用于整个驱动程序包。 若要支持[跨平台安装](https://docs.microsoft.com/windows-hardware/drivers/install/creating-inf-files-for-multiple-platforms-and-operating-systems)的 INF 文件应包含**CatalogFile。** <em>PlatformExtension</em> **=** <em>唯一 filename.cat</em>指令。

有关对驱动程序包进行签名的详细信息，请参阅[驱动程序签名](https://docs.microsoft.com/windows-hardware/drivers/install/driver-signing)并[设备和驱动程序安装基本主题](https://docs.microsoft.com/windows-hardware/drivers/install/device-and-driver-installation-fundamental-topics)。

## <a name="examples"></a>示例

在以下示例中，c:\\MyDriver 包含[驱动程序包](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)其 INF 文件是 MyInfFile.inf 和 INF 文件中的 INF 版本部分包括仅以下**CatalogFile**指令：

```command
[Version]
. . .
CatalogFile=MyCatalogFile.cat
. . .
```

对于此示例中，以下 Inf2Cat 命令将验证是否可以为 Windows 2000 和 x86 版本的 Windows Vista、 Windows Server 2003 和 Windows XP 签名的驱动程序包。 如果包可以为这些版本进行签名，Inf2Cat 创建未签名的编录文件 MyCatalogFile.cat。

```command
Inf2Cat /driver:C:\MyDriver /os:2000,XP_X86,Server2003_X86,Vista_X86
```

在以下示例中，c:\\MyDriver 包含[驱动程序包](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)其 INF 文件是 MyInfFile.inf 和 INF**版本**INF 文件中的部分包括仅以下两个**CatalogFile**指令与平台扩展：

```command
[Version]
. . .
CatalogFile.ntx86=MyCatalogFileX86.cat
CatalogFile.ntamd64=MyCatalogFileX64.cat
. . .
```

对于此示例中，以下 Inf2Cat 命令将验证是否可以为 Windows 2000 和 x86 签名的驱动程序包版本的 Windows Vista、 Windows Server 2003 和 Windows XP。 此外，该命令将验证是否可以针对 x64 签名的驱动程序包的 Windows Vista、 Windows Server 2003 和 Windows XP 版本。 如果可以进行包签名的所有这些版本，Inf2Cat 将创建未签名的编录文件 MyCatalogFileX86.cat 和 MyCatalogFileX64.cat。

```command
Inf2Cat /driver:C:\MyDriver /os:2000,XP_X86,XP_X64,Server2003_X86,Server2003_X64,Vista_X86,Vista_X64
```

有关如何使用 Inf2Cat 创建编录文件的详细信息，请参阅[为 PnP 驱动程序包创建编录文件](https://docs.microsoft.com/windows-hardware/drivers/install/creating-a-catalog-file-for-a-pnp-driver-package)。
