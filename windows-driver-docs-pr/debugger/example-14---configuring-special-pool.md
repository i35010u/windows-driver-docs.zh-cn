---
title: 示例 14 配置特殊池
description: 示例 14 配置特殊池
ms.assetid: a89f8a08-30e4-4d04-9689-c665b2175780
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: c70d2bb2345c4378c2cf2214510ffecfb7250585
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347809"
---
# <a name="example-14-configuring-special-pool"></a>示例 14：配置特殊池


从 Windows Vista 开始，你可以配置[特殊池](special-pool.md)内核标志设置为或注册表设置的功能。 如果将其配置为内核 （运行时间） 的标志设置，您不需要重新启动计算机以使更改生效。 在早期版本的 Windows 中，特殊的池是仅作为注册表设置。

此外，从 Windows Vista 开始，可以设置和配置命令行中的特殊池功能。 在早期版本的 Windows，您可以设置并仅在全局标志对话框中配置特殊池功能。

### <a name="span-idrequestspecialpoolbypooltagwithoutrebootingspanspan-idrequestspecialpoolbypooltagwithoutrebootingspanrequest-special-pool-by-pool-tag-without-rebooting"></a><span id="request_special_pool_by_pool_tag_without_rebooting"></span><span id="REQUEST_SPECIAL_POOL_BY_POOL_TAG_WITHOUT_REBOOTING"></span>请求按池标记的特殊的池，而无需重新启动

以下命令请求的所有分配，则使用的特殊池**标记 1**池标记。 此设置变得立即有效，但如果你关闭或重新启动 Windows，则会丢失。

此命令使用 **/k**参数来指定内核标志 （运行时间） 设置和 + spp 缩写设置特殊池请求。

```console
gflags /k +spp Tag1
```

Gflags 响应通过打印：

```console
Special Pool set to 0x31676154
PoolTagOverruns set to 0x1
Current Running Kernel Settings are: 00000000
```

请注意特殊池分配请求不是内核标志设置不会反映在内核设置值。

此外，特殊的池分配请求不会更改溢出 (0x1) 的值或不足 (0x0) 设置为特殊的池。 若要更改从溢出，默认情况下，到不足，使用 Gflags 对话框。 有关信息，请参阅[检测溢出和不足](detecting-overruns-and-underruns.md)。

你不能在命令行中显示的池标记。 若要验证池标记是一个内核设置，请使用 Gflags 对话框。

### <a name="span-idrequestspecialpoolbypooltagintheregistryspanspan-idrequestspecialpoolbypooltagintheregistryspanrequest-special-pool-by-pool-tag-in-the-registry"></a><span id="request_special_pool_by_pool_tag_in_the_registry"></span><span id="REQUEST_SPECIAL_POOL_BY_POOL_TAG_IN_THE_REGISTRY"></span>通过在注册表中的池标记请求特殊池

以下命令请求的所有分配，则使用的特殊池**标记 1**池标记。 由于此设置存储在注册表中，您必须重新启动计算机以使其生效，但在更改之前保持有效。

此命令使用 **/r**参数指定的注册表设置和 + spp 缩写设置特殊池请求。

```console
gflags /r +spp Tag1
```

Gflags 响应通过打印：

```console
Special Pool set to 0x31676154
PoolTagOverruns set to 0x1
Current Boot Registry Settings are: 00000000
```

请注意特殊池分配请求不是设置一个注册表标志，并且不会反映在注册表设置值。

此外，特殊的池分配请求不会更改溢出 (0x1) 的值或不足 (0x0) 设置为特殊的池。 若要更改从溢出，默认情况下，到不足，使用 Gflags 对话框。 有关信息，请参阅[检测溢出和不足](detecting-overruns-and-underruns.md)。

若要验证值的已添加到注册表，请使用注册表或 Regedit 来显示的值**PoolTag**中的条目**HKEY\_本地\_机\\系统\\CurrentControlSet\\控制\\会话管理器\\内存管理**密钥。

例如：

```console
c:>reg query "HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management" -v PoolTag
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management
    PoolTag    REG_DWORD    0x31676154
```

### <a name="span-idrequestspecialpoolbysizewithoutrebootingspanspan-idrequestspecialpoolbysizewithoutrebootingspanrequest-special-pool-by-size-without-rebooting"></a><span id="request_special_pool_by_size_without_rebooting"></span><span id="REQUEST_SPECIAL_POOL_BY_SIZE_WITHOUT_REBOOTING"></span>请求按大小的特殊的池，而无需重新启动

以下命令请求特殊池分配在 x86 上为 1 到 8 字节的计算机与页\_0x1000 的大小和 8 个字节的分配粒度。

此命令使用 **/k**参数来指定内核标志 （运行时间） 设置和 + spp 缩写设置特殊池请求。 大小值加 0x 以指示它是大小和池标记。

计算的值，0x10，是通过添加分配粒度 （8 个字节） 为在总共 16 个字节 (0x10) 范围内 （8 个字节） 的最大大小。 帮助中确定正确的值输入，请参阅"选择分配大小"中[特殊池](special-pool.md)。

```console
gflags /k +spp 0x10
```

Gflags 响应通过打印：

```console
Special Pool set to 0x10
PoolTagOverruns set to 0x1
Current Running Kernel Settings are: 00000000
```

同样，特殊的池分配请求不是内核标志设置，并不会反映在内核设置值。

此外，特殊的池分配请求不会更改溢出 (0x1) 的值或不足 (0x0) 设置为特殊的池。 若要更改从溢出，默认情况下，到不足，使用 Gflags 对话框。 有关信息，请参阅[检测溢出和不足](detecting-overruns-and-underruns.md)。

### <a name="span-idrequestspecialpoolbysizeintheregistryspanspan-idrequestspecialpoolbysizeintheregistryspanrequest-special-pool-by-size-in-the-registry"></a><span id="request_special_pool_by_size_in_the_registry"></span><span id="REQUEST_SPECIAL_POOL_BY_SIZE_IN_THE_REGISTRY"></span>通过在注册表中的大小来请求特殊池

以下命令请求特殊池用于在 x64 上为 1024年到 1040年字节分配与页计算机\_0x1000 的大小和 16 个字节的分配粒度。

此命令使用 **/r**参数来指定整个系统的注册表设置和 + spp 缩写设置特殊池请求。 大小值加 0x 以指示它是大小和池标记。

值，0x420，会通过添加分配粒度 （16 个字节） 计算到了总共 1056 字节 (0x420) 的范围 （1040 字节） 中的最大大小。 帮助中确定正确的值输入，请参阅"选择分配大小"中[特殊池](special-pool.md)。

```console
gflags /r +spp 0x420
```

Gflags 响应通过打印：

```console
Special Pool set to 0x420
PoolTagOverruns set to 0x1
Current Boot Registry Settings are: 00000000
```

同样，特殊的池分配请求不是设置一个注册表标志并不会反映在注册表设置值。

此外，特殊的池分配请求不会更改溢出 (0x1) 的值或不足 (0x0) 设置为特殊的池。 若要更改从溢出，默认情况下，到不足，使用 Gflags 对话框。 有关信息，请参阅[检测溢出和不足](detecting-overruns-and-underruns.md)。

若要验证值的已添加到注册表，请使用注册表或 Regedit 来显示的值**PoolTag**中的条目**HKEY\_本地\_机\\系统\\CurrentControlSet\\控制\\会话管理器\\内存管理**密钥。

例如：

```console
c:>reg query "HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management" -v PoolTag
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management
    PoolTag    REG_DWORD    0x420
```

### <a name="span-idcancelaspecialpoolrequestspanspan-idcancelaspecialpoolrequestspancancel-a-special-pool-request"></a><span id="cancel_a_special_pool_request"></span><span id="CANCEL_A_SPECIAL_POOL_REQUEST"></span>取消特殊池请求

以下命令为内核 （运行时间） 的标志设置为特殊池取消的请求。 命令为请求按池标记或按大小相同。

```console
gflags /k -spp
```

以下命令取消作为注册表设置特殊的池的请求。 命令为请求按池标记或按大小相同。

```console
gflags /r -spp
```

该命令成功后，Gflags 响应通过打印：

```console
Special Pool value has been deleted.
```

 

 





