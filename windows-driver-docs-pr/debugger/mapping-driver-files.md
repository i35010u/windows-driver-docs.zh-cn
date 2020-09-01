---
title: 映射驱动程序文件
description: 映射驱动程序文件
ms.assetid: 9a13a6a9-b585-4be1-b7c8-da65fa3ba6c6
keywords:
- 映射驱动程序文件
- 驱动程序替换图
- 驱动程序替换地图，概述
- 驱动程序替换地图，文件格式
- 驱动程序替换图，替换启动驱动程序
- 启动驱动程序替换
ms.date: 05/13/2020
ms.localizationpriority: medium
ms.openlocfilehash: 9f5b224163df80d0775ae963fbd62b0fe5130f69
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217366"
---
# <a name="mapping-driver-files"></a>映射驱动程序文件

## <span id="ddk_mapping_driver_files_dbg"></span><span id="DDK_MAPPING_DRIVER_FILES_DBG"></span>

替换驱动程序文件可能会很困难。 通常，必须启动到 Microsoft Windows *安全生成*，替换驱动程序二进制文件，然后重新启动。

使用映射文件存在替代方法。 您可以使用此映射方法替换任何内核模式驱动程序 (包括显示驱动程序) 、任何 Windows 子系统驱动程序或任何其他内核模式模块。 为简单起见，在本主题中，这些文件称为 " *驱动程序* "，即使您可以对任何内核模式模块使用此方法也是如此。

无论何时将 WinDbg 或 KD 附加为内核调试器，都可以使用此方法。 你还可以在启动驱动程序上使用此方法，但这会比较困难。 有关如何将此方法用于启动驱动程序的详细信息，请参阅替换启动驱动程序。

若要使用驱动程序替换图来替换驱动程序文件，请执行以下操作：

1.  创建 *驱动程序替换映射文件*。 此文件是一个文本文件，其中列出了目标计算机上的驱动程序及其在主计算机上的替换驱动程序。 可以替换任意数量的驱动程序。 例如，你可能会在 \\ 包含以下信息的主计算机的 d： Map Files 目录中创建名为 Mymap.ini 的文件 \_ 。

    ```ini
    map
    \Systemroot\system32\drivers\videoprt.sys
    \\myserver\myshare\new_drivers\videoprt.sys
    ```

    有关此文件的语法的详细信息，请参阅驱动程序替换映射文件格式。

2.  设置与目标计算机的内核调试连接，并在主计算机上 (KD 或 WinDbg) 启动内核调试器。  (不必实际中断目标计算机。 ) 

3.  通过执行以下操作之一加载驱动程序替换映射文件：
    -   \_ \_ 启动内核调试器之前，请设置 NT KD \_ FILES[环境变量](environment-variables.md)。

        ```console
        D:\Debugging Tools for Windows> set _NT_KD_FILES=d:\Map_Files\mymap.ini
        D:\Debugging Tools for Windows> kd
        ```

    -   启动内核调试器后，使用 [**kdfiles (设置驱动程序替换映射) **](-kdfiles--set-driver-replacement-map-.md) 命令。

        ```console
        D:\Debugging Tools for Windows> kd
        kd> .kdfiles d:\Map_Files\mymap.ini
        KD file associations loaded from 'd:\Map_Files\mymap.ini'
        ```

        你还可以使用 **kdfiles** 命令来显示当前的驱动程序替换映射文件或删除驱动程序替换图。 如果不使用此命令，映射将一直存在，直到退出调试器。

完成此过程之后，驱动程序替换映射会生效。

只要目标计算机要加载驱动程序，它就会查询内核调试器，以确定是否已映射此驱动程序。 如果已映射该驱动程序，则会通过内核连接发送替换文件，并通过旧的驱动程序文件对其进行复制。 然后，将加载新的驱动程序。

### <a name="span-iddriver_replacement_map_file_formatspanspan-iddriver_replacement_map_file_formatspandriver-replacement-map-file-format"></a><span id="driver_replacement_map_file_format"></span><span id="DRIVER_REPLACEMENT_MAP_FILE_FORMAT"></span>驱动程序替换映射文件格式

驱动程序替换映射文件中的每个驱动程序文件替换均由三行表示。

-   第一行包含 "map" 一词。

-   第二行指定目标计算机上旧驱动程序的路径和文件名。

-   第三行指定新驱动程序的完整路径。 此驱动程序可以位于主计算机上，也可以位于其他某个服务器上。

您可以任意多次重复此信息模式。

路径和文件名不区分大小写，实际驱动程序文件名可能不同。 当目标计算机将要加载该驱动程序时，将在第三行中指定的文件复制到第二行中指定的文件。

Kdfiles 将尝试将存储在服务控制管理器 (SCM) 数据库中的文件名匹配。 SCM 数据库中的名称与传递给 MmLoadSystemImage 的名称相同。

在 Windows 10 和更高版本的调试工具中，驱动程序映射可用于动态匹配驱动程序名称并确定正确的路径。 无需指定完整路径，并且文件扩展名是可选的。 您可以使用这些项中的任意项来匹配 NT 文件系统驱动程序。

-   ntfs
-   NTFS
-   ntfs.sys
-   windows \\ system32 \\ 驱动程序 \\ntfs.sys

您可以使用这些项中的任意项来匹配 NT 内核驱动程序。

-   ntoskrnl.exe
-   NTOSKRNL.EXE
-   ntoskrnl.sys
-   windows \\ system32 \\ 驱动程序 \\ntoskrnl.sys

地图文件可以包含空行，并可以包含以数字符号开头的注释行 (**\#**) 。 但是，在文件中出现 "map" 后，接下来的两行必须是旧驱动程序和新驱动程序。 空行和注释行不能分解三行地图块。

下面的示例演示了驱动程序替换映射文件。

```text
# Use the # for comments like this one
map
\Systemroot\system32\drivers\videoprt.sys
e:\MyNewDriver\binaries\videoprt.sys
map
\Systemroot\system32\mydriver.sys
\\myserver\myshare\new_drivers\mydriver0031.sys

# This is replacing a beep driver
map
\??\c:\windows\system32\beep.sys
\\myserver\myshare\new_drivers\new_beep.sys
```

驱动程序替换映射文件必须是文本文件，但您可以使用任何文件名和文件扩展名 ( .ini、.txt、.map 等) 。

### <a name="span-idadditional_notesspanspan-idadditional_notesspanadditional-notes"></a><span id="additional_notes"></span><span id="ADDITIONAL_NOTES"></span>其他说明

出现驱动程序替换时，内核调试器中会出现一条消息。

如果在 KD 中使用 [**ctrl + D**](ctrl-d--toggle-debug-info-.md) () 或在 WinDbg) 中按 CTRL + ALT + d (，则会看到有关替换请求的详细信息。 如果你不确定列出的名称是否与 SCM 数据库中的名称匹配，则此信息会很有用。

可以启用 bcdedit bootdebug 选项，以查看可用于替换内核、hal 或启动驱动程序的早期启动信息。

```console
bcdedit -bootdebug on
```

有关详细信息，请参阅 [BCDEdit Options Reference](../devtest/bcd-boot-options-reference.md)。

如果内核调试器退出，则不会再进行驱动程序替换。 但是，已替换的任何驱动程序都不会还原为其旧的二进制文件，因为驱动程序文件实际上被覆盖。

此驱动程序替换功能会自动绕过 Windows 文件保护 (WFP) 。

您无需重新启动目标计算机。 无论目标计算机是否已重启，都将在目标计算机加载驱动程序时进行替换。 当然，大多数驱动程序都是在启动过程中加载的，因此，在此过程中，在加载映射文件后，应该重启目标计算机。

如果 \_ 定义了 NT \_ KD \_ FILES 变量，则启动内核调试器时，将读取指定的驱动程序替换映射文件。 如果发出 **kdfiles** 命令，则会立即读取指定的文件。 此时，调试器将验证该文件是否具有基本的映射/行/行格式。 但在发生替换之前，不会验证实际路径和文件名。

读取映射文件后，调试器将存储其内容。 如果在此之后更改此文件，则所做的更改不会 (，除非重新发出 **kdfiles** 命令) 。