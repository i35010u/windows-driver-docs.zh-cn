---
title: 用于操作内存的启动参数
description: 用于操作内存的启动参数
ms.assetid: 04504216-20b5-4c65-a1e2-6eec7480ce17
keywords:
- 与内存相关的启动选项 WDK
- 引导参数 WDK
- 启动入口参数 WDK
- 操作内存 WDK 引导参数
- 内存不足的环境 WDK 引导参数
- 模拟内存不足的环境 WDK 引导参数
- 内存 WDK 引导参数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44f681a3c60afec6b3d5d72bb2078d517e70f993
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577553"
---
# <a name="boot-parameters-to-manipulate-memory"></a>用于操作内存的启动参数


## <span id="ddk_boot_parameters_to_manipulate_memory_tools"></span><span id="DDK_BOOT_PARAMETERS_TO_MANIPULATE_MEMORY_TOOLS"></span>


您可以模拟用于测试而无需更改的计算机上的物理内存量的内存不足的环境。 相反，您可以通过使用限制可用于操作系统的内存**truncatememory**或**removememory**使用选项[ **BCDedit /set**](https://msdn.microsoft.com/library/windows/hardware/ff542202)命令。

**/Maxmem**参数指定的最大 Windows 的可用内存量。 它被校准兆字节 (MB)。 将值设置为在计算机上任何金额小于实际的物理内存。

**/Maxmem**参数实际确定可用于 Windows 的最大内存地址。 由于物理内存的映射中的缺口，Windows 可能会收到略少内存的值比 **/maxmem**。 对于更高的精度，使用 **/burnmemory**。

**Truncatememory**或**removememory**选项是可用在 Windows 7 和更高版本。 **Truncatememory**选项不考虑版本或高于指定物理地址的所有内存。 **Removememory**选项可减少内存可用于 Windows 指定的量 （以 MB 为单位）。 这两个选项减少内存，但**removememory**选项是更好地限制操作系统以使用指定的内存，同时考虑内存存在空白。

### <a name="span-idbootparameterstotestinalowmemoryenvironmentinwindowsvistaaspanspan-idbootparameterstotestinalowmemoryenvironmentinwindowsvistaaspanboot-parameters-to-test-in-a-low-memory-environment-in-windows"></a><span id="boot_parameters_to_test_in_a_low_memory_environment_in_windows_vista_a"></span><span id="BOOT_PARAMETERS_TO_TEST_IN_A_LOW_MEMORY_ENVIRONMENT_IN_WINDOWS_VISTA_A"></span>在 Windows 中的内存不足的环境中测试的启动参数

若要模拟内存不足的环境，请使用[ **BCDedit /set** ](https://msdn.microsoft.com/library/windows/hardware/ff542202)命令并**removememory**选择修改的启动项。 设置的值**removememory**减去此测试所需的内存大小的系统上的物理内存量。

例如，若要限制使用 2 GB 到 512 MB 的可用内存的最大物理内存的计算机的内存，可设置的值**removememory** 1536 (2 GB (2048 MB)-512 MB = 1536 MB) 的参数。

下面的示例显示了 BCDEdit 命令用于向指定的启动项目系统中删除从总可用 1536 MB 的内存。

```
bcdedit /set {18b123cd-2bf6-11db-bfae-00e018e2b8db} removememory 1536
```

此外可以使用**truncatememory**选项与**bcdedit /set**命令来实现相同的结果。 在使用此选项，Windows 将忽略所有内存处于或高于指定物理地址。 指定*地址*以字节为单位。 例如，以下命令设置指定的启动项目为 1 GB 的物理地址限制。 以十进制 (1073741824) 或十六进制 (0x40000000)，可以指定的地址。

```
bcdedit /set {18b123cd-2bf6-11db-bfae-00e018e2b8db} truncatememory Ox40000000
```

因为**removememory**选项不会进行更有效地使用系统内存，而不是建议其使用**truncatememory**。

完成后测试，您可以删除**removememory**并**truncatememory**使用的启动项选项[ **BCDEdit /deletevalue** ](https://msdn.microsoft.com/library/windows/hardware/jj856916)命令。

 

 





