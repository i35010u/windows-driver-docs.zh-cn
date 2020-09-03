---
title: 用于操作内存的启动参数
description: 用于操作内存的启动参数
ms.assetid: 04504216-20b5-4c65-a1e2-6eec7480ce17
keywords:
- 与内存相关的启动选项 WDK
- 启动参数 WDK
- 启动项参数 WDK
- 操作内存 WDK 启动参数
- 低内存环境 WDK 启动参数
- 模拟低内存环境 WDK 启动参数
- 内存 WDK 启动参数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bab859bc3875208a9c63c8f04345b424d2b9f9c6
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89384353"
---
# <a name="boot-parameters-to-manipulate-memory"></a>用于操作内存的启动参数


## <span id="ddk_boot_parameters_to_manipulate_memory_tools"></span><span id="DDK_BOOT_PARAMETERS_TO_MANIPULATE_MEMORY_TOOLS"></span>


可以模拟用于测试的低内存环境，而无需更改计算机上的物理内存量。 相反，可以通过将 **truncatememory** 或 **Removememory** 选项与 [**BCDedit/set**](./bcdedit--set.md) 命令配合使用来限制操作系统可用的内存。

**/Maxmem**参数指定 Windows 可用的最大内存量。 它以兆字节 (MB) 校准。 将值设置为小于计算机上实际物理内存的任何数量。

**/Maxmem**参数实际上确定了适用于 Windows 的最大内存地址。 由于物理内存映射存在间隙，Windows 可能会获得比 **/maxmem**值小得多的内存。 若要获得更高的精度，请使用 **/burnmemory**。

Windows 7 和更高版本中提供了 **truncatememory** 或 **removememory** 选项。 **Truncatememory**选项忽略指定物理地址或其上方的所有内存。 **Removememory**选项可按指定的量减少对 Windows 可用的内存量 (以 MB) 度量。 这两个选项都可以减少内存，但在考虑内存间隙时， **removememory** 选项会更好地限制操作系统使用指定的内存。

### <a name="span-idboot_parameters_to_test_in_a_low_memory_environment_in_windows_vista_aspanspan-idboot_parameters_to_test_in_a_low_memory_environment_in_windows_vista_aspanboot-parameters-to-test-in-a-low-memory-environment-in-windows"></a><span id="boot_parameters_to_test_in_a_low_memory_environment_in_windows_vista_a"></span><span id="BOOT_PARAMETERS_TO_TEST_IN_A_LOW_MEMORY_ENVIRONMENT_IN_WINDOWS_VISTA_A"></span>在 Windows 中的低内存环境中测试的启动参数

若要模拟低内存环境，请使用 [**BCDedit/set**](./bcdedit--set.md) 命令和 **removememory** 选项来修改启动项。 将 **removememory** 的值设置为系统上的物理内存量减去此测试所需的内存大小。

例如，若要将具有 2 GB 物理内存的计算机的内存限制为最大 512 MB 的可用内存，请将 **removememory** 参数的值设置为 1536 (2 gb (2048 mb) -512 MB = 1536 mb) 。

下面的示例演示了一个 BCDEdit 命令，该命令用于从系统的总可用空间中删除指定启动项的 1536 MB 内存。

```
bcdedit /set {18b123cd-2bf6-11db-bfae-00e018e2b8db} removememory 1536
```

还可以将 **truncatememory** 选项与 **bcdedit/set** 命令一起使用，以获得相同的结果。 使用此选项时，Windows 会忽略指定物理地址或以上的所有内存。 指定地址（以字节为单位）。 例如，以下命令将指定启动项的物理地址限制设置为 1 GB。 可以以十进制 (1073741824) 或十六进制 (0x40000000) 指定地址。

```
bcdedit /set {18b123cd-2bf6-11db-bfae-00e018e2b8db} truncatememory Ox40000000
```

由于 **removememory** 选项可以更有效地使用系统内存，因此建议使用它而不是 **truncatememory**。

完成测试后，可以使用[**BCDEdit/deletevalue**](./bcdedit--deletevalue.md)命令删除**removememory**和**truncatememory** boot entry 选项。

 

