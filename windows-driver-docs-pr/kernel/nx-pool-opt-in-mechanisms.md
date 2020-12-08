---
title: NX 池启用机制
description: 若要从 Windows 的早期版本将内核模式驱动程序代码移植到 Windows 8，你应使用 NonPagedPoolNx 类型的内存池作为最佳实践。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: dedefa6b3006de50bb13c0dca5328b91e41eb7a1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831357"
---
# <a name="nx-pool-opt-in-mechanisms"></a>NX 池启用机制


若要从 Windows 的早期版本将内核模式驱动程序代码移植到 Windows 8，你应使用 **NonPagedPoolNx** 类型的内存池作为最佳实践。 默认情况下，可以使用多个移植辅助工具之一轻松地 "选择加入" 以使用 **NonPagedPoolNx** 池类型。

这些移植辅助工具使用以下一种或两种方法，使驱动程序能够使用 NX 非分页池：

-   使用 `#define` 预处理器语句创建全局定义的宏名称。

-   从 [**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 例程调用内联函数。

对于大多数内核模式驱动程序代码，这些移植辅助工具使开发人员能够以最小的工作量更新其驱动程序。

## <a name="in-this-section"></a>在本节中


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>主题</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="single-binary-opt-in-pool-nx-optin.md" data-raw-source="[Single Binary Opt-In: POOL_NX_OPTIN](single-binary-opt-in-pool-nx-optin.md)">启用单个二进制文件：POOL_NX_OPTIN</a></p></td>
<td><p>若要生成在 Windows 8 和更早版本的 Windows 中运行的单个驱动程序二进制文件，请使用 POOL_NX_OPTIN 选择加入机制。 这是为第三方硬件供应商提供的一项移植辅助，它们提供单个驱动程序二进制文件以支持多个 Windows 版本。</p></td>
</tr>
<tr class="even">
<td><p><a href="multiple-binary-opt-in-pool-nx-optin-auto.md" data-raw-source="[Multiple Binary Opt-In: POOL_NX_OPTIN_AUTO](multiple-binary-opt-in-pool-nx-optin-auto.md)">启用多个二进制文件：POOL_NX_OPTIN_AUTO</a></p></td>
<td><p>如果你是提供不同版本 Windows 的不同驱动程序二进制文件的硬件供应商，则可以使用 POOL_NX_OPTIN_AUTO 选择加入机制。 此移植助手为 Windows 8 和您的驱动程序支持的每个早期版本的 Windows 构建单独的驱动程序二进制文件。</p></td>
</tr>
<tr class="odd">
<td><p><a href="selective-opt-out-pool-nx-optout.md" data-raw-source="[Selective Opt-Out: POOL_NX_OPTOUT](selective-opt-out-pool-nx-optout.md)">选择性禁用：POOL_NX_OPTOUT</a></p></td>
<td><p>你可以全局启用一组驱动程序源文件的 "不执行 (NX) 池" 选择机制，然后使用 POOL_NX_OPTOUT 为一个或多个选定的源文件重写此选择机制。 这允许选定的源文件继续使用可执行的非分页内存。 您可以将 POOL_NX_OPTOUT 选择退出机制与 POOL_NX_OPTIN 或 POOL_NX_OPTIN_AUTO 选择机制一起使用。</p></td>
</tr>
</tbody>
</table>

 

 

