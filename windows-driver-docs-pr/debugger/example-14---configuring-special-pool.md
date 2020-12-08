---
title: 示例14配置特殊池
description: 示例14配置特殊池
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8fc83ca58245e802529d630efe07fe3434f2808a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792405"
---
# <a name="example-14-configuring-special-pool"></a>示例14：配置特殊池


从 Windows Vista 开始，可以将 [特殊池](special-pool.md) 功能配置为内核标志设置或注册表设置。 如果将其配置为 (运行时) 设置的内核标志，则无需重新启动计算机以使更改生效。 在早期版本的 Windows 中，特殊池仅作为注册表设置提供。

此外，从 Windows Vista 开始，你可以从命令行设置和配置特殊的池功能。 在较早版本的 Windows 中，只能在 "全局标志" 对话框中设置和配置特殊池功能。

### <a name="span-idrequest_special_pool_by_pool_tag_without_rebootingspanspan-idrequest_special_pool_by_pool_tag_without_rebootingspanrequest-special-pool-by-pool-tag-without-rebooting"></a><span id="request_special_pool_by_pool_tag_without_rebooting"></span><span id="REQUEST_SPECIAL_POOL_BY_POOL_TAG_WITHOUT_REBOOTING"></span>在不重新启动的情况下请求按池标记的特殊池

以下命令请求具有 **Tag1** 池标记的所有分配的特殊池。 此设置将立即生效，但如果关闭或重新启动 Windows，则会丢失此设置。

此命令使用 **/k** 参数指定 (运行时) 设置的内核标志，并使用 + spp 缩写设置特殊的池请求。

```console
gflags /k +spp Tag1
```

Gflags 通过打印做出响应：

```console
Special Pool set to 0x31676154
PoolTagOverruns set to 0x1
Current Running Kernel Settings are: 00000000
```

请注意，特殊池分配请求不是内核标志设置，并且不会反映在内核设置值中。

此外，特殊池分配请求不会将溢出 (0x1 的值更改) 或不足以 (0x0) 设置。 若要从溢出（默认值）更改为不足，请使用 "Gflags" 对话框。 有关信息，请参阅 [检测超支和不足](detecting-overruns-and-underruns.md)。

不能在命令行中显示池标记。 若要验证池标记是否为内核设置，请使用 "Gflags" 对话框。

### <a name="span-idrequest_special_pool_by_pool_tag_in_the_registryspanspan-idrequest_special_pool_by_pool_tag_in_the_registryspanrequest-special-pool-by-pool-tag-in-the-registry"></a><span id="request_special_pool_by_pool_tag_in_the_registry"></span><span id="REQUEST_SPECIAL_POOL_BY_POOL_TAG_IN_THE_REGISTRY"></span>在注册表中请求按池标记的特殊池

以下命令请求具有 **Tag1** 池标记的所有分配的特殊池。 由于此设置存储在注册表中，因此你必须重新启动计算机才能使其生效，但在你更改它之前，它将一直有效。

此命令使用 **/r** 参数指定注册表设置，并使用 + spp 缩写来设置特殊的池请求。

```console
gflags /r +spp Tag1
```

Gflags 通过打印做出响应：

```console
Special Pool set to 0x31676154
PoolTagOverruns set to 0x1
Current Boot Registry Settings are: 00000000
```

请注意，特殊池分配请求不是注册表标志设置，并且不会反映在注册表设置值中。

此外，特殊池分配请求不会将溢出 (0x1 的值更改) 或不足以 (0x0) 设置。 若要从溢出（默认值）更改为不足，请使用 "Gflags" 对话框。 有关信息，请参阅 [检测超支和不足](detecting-overruns-and-underruns.md)。

若要验证是否已将值添加到注册表中，请使用 Reg 或 Regedit 在 **HKEY \_ 本地 \_ 计算机 \\ 系统 \\ CurrentControlSet \\ 控制 \\ 会话管理器 \\ 内存管理** 密钥中显示 **PoolTag** 项的值。

例如：

```console
c:>reg query "HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management" -v PoolTag
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management
    PoolTag    REG_DWORD    0x31676154
```

### <a name="span-idrequest_special_pool_by_size_without_rebootingspanspan-idrequest_special_pool_by_size_without_rebootingspanrequest-special-pool-by-size-without-rebooting"></a><span id="request_special_pool_by_size_without_rebooting"></span><span id="REQUEST_SPECIAL_POOL_BY_SIZE_WITHOUT_REBOOTING"></span>按大小请求特殊池而不重新启动

以下命令请求特殊的池，以在 x86 计算机上分配1到8个字节，页面 \_ 大小为0x1000，分配粒度为8个字节。

此命令使用 **/k** 参数指定 (运行时) 设置的内核标志，并使用 + spp 缩写设置特殊的池请求。 大小值以0x 开头，表示它是大小而不是池标记。

值0x10，通过将分配粒度)  (8 个字节添加到范围中的最大大小， (8 个字节) ，总共16字节 (0x10) 。 若要帮助确定输入正确的值，请参阅 [特殊池中](special-pool.md)的 "选择分配大小"。

```console
gflags /k +spp 0x10
```

Gflags 通过打印做出响应：

```console
Special Pool set to 0x10
PoolTagOverruns set to 0x1
Current Running Kernel Settings are: 00000000
```

同样，特殊池分配请求不是内核标志设置，并且不会反映在内核设置值中。

此外，特殊池分配请求不会将溢出 (0x1 的值更改) 或不足以 (0x0) 设置。 若要从溢出（默认值）更改为不足，请使用 "Gflags" 对话框。 有关信息，请参阅 [检测超支和不足](detecting-overruns-and-underruns.md)。

### <a name="span-idrequest_special_pool_by_size_in_the_registryspanspan-idrequest_special_pool_by_size_in_the_registryspanrequest-special-pool-by-size-in-the-registry"></a><span id="request_special_pool_by_size_in_the_registry"></span><span id="REQUEST_SPECIAL_POOL_BY_SIZE_IN_THE_REGISTRY"></span>在注册表中按大小请求特殊池

以下命令请求在 x64 计算机上为1024到1040字节的分配分配特殊池，其页 \_ 大小为0x1000，分配粒度为16字节。

此命令使用 **/r** 参数指定系统范围的注册表设置，并使用 + spp 缩写来设置特殊的池请求。 大小值以0x 开头，表示它是大小而不是池标记。

值0x420 是通过将)  (16 个字节的分配粒度添加到 (1040 字节) 范围内的最大大小为1056个字节的最大大小 (0x420) 来计算的。 若要帮助确定输入正确的值，请参阅 [特殊池中](special-pool.md)的 "选择分配大小"。

```console
gflags /r +spp 0x420
```

Gflags 通过打印做出响应：

```console
Special Pool set to 0x420
PoolTagOverruns set to 0x1
Current Boot Registry Settings are: 00000000
```

同样，特殊池分配请求不是注册表标志设置，并且不会反映在注册表设置值中。

此外，特殊池分配请求不会将溢出 (0x1 的值更改) 或不足以 (0x0) 设置。 若要从溢出（默认值）更改为不足，请使用 "Gflags" 对话框。 有关信息，请参阅 [检测超支和不足](detecting-overruns-and-underruns.md)。

若要验证是否已将值添加到注册表中，请使用 Reg 或 Regedit 在 **HKEY \_ 本地 \_ 计算机 \\ 系统 \\ CurrentControlSet \\ 控制 \\ 会话管理器 \\ 内存管理** 密钥中显示 **PoolTag** 项的值。

例如：

```console
c:>reg query "HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management" -v PoolTag
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management
    PoolTag    REG_DWORD    0x420
```

### <a name="span-idcancel_a_special_pool_requestspanspan-idcancel_a_special_pool_requestspancancel-a-special-pool-request"></a><span id="cancel_a_special_pool_request"></span><span id="CANCEL_A_SPECIAL_POOL_REQUEST"></span>取消特殊池请求

以下命令将特殊池的请求作为内核标志取消 (运行时) 设置。 对于按池标记或大小的请求，命令是相同的。

```console
gflags /k -spp
```

以下命令将对特殊池的请求取消为注册表设置。 对于按池标记或大小的请求，命令是相同的。

```console
gflags /r -spp
```

如果此命令成功，Gflags 将通过打印进行响应：

```console
Special Pool value has been deleted.
```

 

 





