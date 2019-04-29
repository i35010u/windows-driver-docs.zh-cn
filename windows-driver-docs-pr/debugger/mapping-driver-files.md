---
title: 映射驱动程序文件
description: 映射驱动程序文件
ms.assetid: 9a13a6a9-b585-4be1-b7c8-da65fa3ba6c6
keywords:
- 映射驱动程序文件
- 驱动程序替换映射
- 驱动程序替换映射概述
- 驱动程序替换映射中，文件格式
- 驱动程序替换映射，将启动的驱动程序
- 启动驱动程序替换
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc8b2024711501fc64f02a9b967dd9c24fd74f23
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383297"
---
# <a name="mapping-driver-files"></a>映射驱动程序文件


## <span id="ddk_mapping_driver_files_dbg"></span><span id="DDK_MAPPING_DRIVER_FILES_DBG"></span>


替换为驱动程序文件可能很困难。 通常情况下，必须启动到 Microsoft Windows*安全生成*，替换驱动程序二进制文件，然后再次启动。

但是，Windows XP 和更高版本的 Windows 支持的驱动程序文件替换为更简单的方法。 此方法可用于取代 （包括显示器驱动程序） 的任何内核模式驱动程序、 任何 Windows 子系统的驱动程序或内核模式下的任何其他模块。 为简单起见，这些文件称为*驱动程序*中本主题中，即使您可以使用此方法为内核模式下的任何模块。

每当 WinDbg 或 KD 附加为内核调试程序时，可以使用此方法。 此外可以启动的驱动程序，使用此方法，但会更加困难。 有关如何使用此方法与启动驱动程序的详细信息，请参阅替换引导驱动程序。

若要使用的驱动程序替换映射替换驱动程序文件，请执行以下操作：

1.  创建*驱动程序替换映射文件*。 此文件是文本文件，其中列出了在目标计算机上的驱动程序和主机计算机上的其替换驱动程序。 您可以替换任意数量的驱动程序。 例如，可以创建一个文件中名为 Mymap.ini d:\\映射\_主机计算机，其中包含以下信息的文件目录。

    ```ini
    map
    \Systemroot\system32\drivers\videoprt.sys
    \\myserver\myshare\new_drivers\videoprt.sys
    ```

    此文件的语法的详细信息，请参阅驱动程序替换映射文件格式。

2.  设置内核调试与目标计算机的连接并开始在主机计算机上的内核调试程序 （KD 或 WinDbg）。 （您无需实际中中断到目标计算机。）

3.  加载驱动程序替换映射文件，通过执行以下任一操作：
    -   设置\_NT\_KD\_文件[环境变量](environment-variables.md)开始内核调试程序之前。

        ```console
        D:\Debugging Tools for Windows> set _NT_KD_FILES=d:\Map_Files\mymap.ini
        D:\Debugging Tools for Windows> kd
        ```

    -   使用[ **.kdfiles (设置驱动程序替换 Map)** ](-kdfiles--set-driver-replacement-map-.md)命令后启动内核调试程序。

        ```console
        D:\Debugging Tools for Windows> kd
        kd> .kdfiles d:\Map_Files\mymap.ini
        KD file associations loaded from 'd:\Map_Files\mymap.ini'
        ```

        此外可以使用 **.kdfiles**命令以显示当前的驱动程序替换映射文件或删除驱动程序替换映射。 如果不使用此命令，该映射持续，直到退出调试器。

完成此过程后，驱动程序替换映射将生效。

只要在目标计算机以加载驱动程序，它将查询内核调试程序，以确定是否已映射了此驱动程序。 如果映射该驱动程序，替换文件被发送，内核连接，并覆盖旧的驱动程序文件复制。 然后加载新的驱动程序。

### <a name="span-iddriverreplacementmapfileformatspanspan-iddriverreplacementmapfileformatspandriver-replacement-map-file-format"></a><span id="driver_replacement_map_file_format"></span><span id="DRIVER_REPLACEMENT_MAP_FILE_FORMAT"></span>驱动程序替换映射文件格式

每个驱动程序文件替换为由驱动程序替换映射文件中的三个行。

-   第一行包含单词"映射"。

-   第二行指定目标计算机上旧驱动程序路径和文件名。

-   第三行指定新的驱动程序的完整路径。 此驱动程序可以位于主计算机上或一些其他服务器上。

您可以任意次数重复此模式的信息。

路径和文件名称不区分大小写，且实际的驱动程序文件名称可以不同。 在第三个行指定的文件复制目标计算机是以加载该驱动程序时在第二个行上指定的文件。

Kdfiles 将尝试与服务控制管理器 (SCM) 数据库中存储的文件名匹配。 SCM 数据库中的名称与传递给 MmLoadSystemImage 的名称完全相同。

在 Windows 10 和更高版本的调试工具，驱动程序映射的工作原理动态匹配的驱动程序名称，并确定正确的路径。 不需要指定完整路径和文件扩展名是可选的。 可以使用任何这些项以匹配 NT 文件系统驱动程序。

-   ntfs
-   NTFS
-   ntfs.sys
-   windows\\system32\\drivers\\ntfs.sys

可以使用任何这些项以匹配 NT 内核驱动程序。

-   ntoskrnl
-   NTOSKRNL
-   ntoskrnl.sys
-   windows\\system32\\drivers\\ntoskrnl.sys

映射文件可以包含空白行，并且可以包含以数字符号开头的注释行 (**\#**)。 但是，在文件中显示的"映射"后，接下来的两行必须是旧驱动程序和新的驱动程序。 空白的行和注释行无法分解的三个线条图块。

下面的示例显示了驱动程序替换映射文件。

```text
map
\Systemroot\system32\drivers\videoprt.sys
e:\MyNewDriver\binaries\videoprt.sys
map
\Systemroot\system32\mydriver.sys
\\myserver\myshare\new_drivers\mydriver0031.sys

# Here is a comment
map
\??\c:\windows\system32\beep.sys
\\myserver\myshare\new_drivers\new_beep.sys
```

驱动程序替换映射文件必须是一个文本文件，但可以使用任何文件名和文件扩展名 （.ini、.txt、.map，等）。

### <a name="span-idadditionalnotesspanspan-idadditionalnotesspanadditional-notes"></a><span id="additional_notes"></span><span id="ADDITIONAL_NOTES"></span>其他说明

驱动程序替换时，内核调试器中显示一条消息。

如果您使用[ **CTRL + D** ](ctrl-d--toggle-debug-info-.md) （在 KD) 或 CTRL + ALT + D （在 WinDbg 中），请参阅有关替换请求的详细信息。 此信息可以是如果您不确定是否已列出的名称匹配的 SCM 数据库中的一个很有用。

您可以启用 bcdedit bootdebug 选项，若要查看可用于替换内核，hal 或启动驱动程序的早期启动信息。

```console
bcdedit -bootdebug on
```

有关详细信息，请参阅[BCDEdit 选项参考](https://msdn.microsoft.com/library/windows/hardware/ff542205)。

如果内核调试程序退出后，会发生没有多个驱动程序替代项。 但是，被取代的任何驱动程序恢复为其旧的二进制文件，因为实际上覆盖驱动程序文件。

此驱动程序替换功能自动将绕过 Windows 文件保护 (WFP)。

不需要重新启动目标计算机。 执行了驱动程序替换任何目标计算机将加载的驱动程序，而不考虑是否已重新启动后的时间。 当然，大多数驱动程序加载在启动过程中，因此在实践中应后，重新启动目标计算机已加载映射文件。

如果\_NT\_KD\_定义文件变量、 内核调试程序在启动时读取指定的驱动程序替换映射文件。 如果发出 **.kdfiles**命令，因此指定的文件立即阅读。 此时，调试器将验证该文件具有基本的映射/行/行格式。 但直到替换发生未验证的实际路径和文件名。

映射文件具有读取后，调试器会将其内容存储。 如果此点后更改此文件，所做的更改产生任何影响 (除非你重新颁发 **.kdfiles**命令)。

### <a name="span-idreplacingbootdriversspanspan-idreplacingbootdriversspanreplacing-boot-drivers"></a><span id="replacing_boot_drivers"></span><span id="REPLACING_BOOT_DRIVERS"></span>将启动的驱动程序

如果你想要通过使用此驱动程序的替换方法来替换启动驱动程序文件，必须将内核调试器连接到 Windows 启动加载器 (Ntldr) 上，而不是 Windows 内核。 您可以进行此连接之前，必须安装 Ntldr 的特殊启用了调试器的版本。 您可以找到 Ntldr 的此版本中 Windows Driver Kit (WDK)，在 %DDKROOT%\\调试目录。

由于目标计算机绕过其 Boot.ini 文件，不能按一般方式来设置内核连接协议。 您必须通过在目标计算机上的 COM1 端口进行连接。 115200 波特率。 因此，主机计算机上的内核调试器应配置为使用 COM 连接以 115200 的速度。

此特殊的方法仅适用于启动驱动程序 (即，Acpi.sys、 Classpnp.sys、 Disk.sys，和任何其他内容的[ **lm t n** ](lm--list-loaded-modules-.md)显示初始 Windows 断点处)。 如果必须替换标准驱动程序的**MmLoadSystemImage**加载启动完成后，应使用前面所述的标准方法。

不能替换而不是 Boot.ini 文件中使用 EFI 固件的计算机上的启动驱动程序。

 

 





