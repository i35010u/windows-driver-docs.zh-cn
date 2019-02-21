---
title: NX 池选择机制
description: 移植内核模式驱动程序代码到 Windows 8 从早期版本的 Windows，应将内存池的 NonPagedPoolNx 类型用作一种最佳做法。
ms.assetid: 9C868569-14EC-4915-8553-FD2D94C5A855
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e2e8fa1f4f7ac1fe963d16ad73ee454ea290fab1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524068"
---
# <a name="nx-pool-opt-in-mechanisms"></a>NX 池选择机制


移植内核模式驱动程序代码到 Windows 8 从早期版本的 Windows，则应使用**NonPagedPoolNx**最佳做法是内存池的类型。 可以使用多个迁移辅助工具之一来轻松地"选择"使用**NonPagedPoolNx**池类型默认情况下。

这些迁移辅助工具使用一个或两个以下方法启用驱动程序使用 NX 非分页缓冲的池：

-   使用`#define`预处理器语句来创建全局定义的宏名称。

-   调用内联函数从[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)例程。

对于大多数内核模式驱动程序代码，这些迁移的辅助功能使开发人员能够轻松地更新其驱动程序。

## <a name="in-this-section"></a>本部分内容


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
<td><p><a href="single-binary-opt-in-pool-nx-optin.md" data-raw-source="[Single Binary Opt-In: POOL_NX_OPTIN](single-binary-opt-in-pool-nx-optin.md)">单个二进制参加：POOL_NX_OPTIN</a></p></td>
<td><p>若要生成运行在 Windows 8 和 Windows 的早期版本中的单个驱动程序二进制文件，请使用 POOL_NX_OPTIN 参加机制。 这是第三方硬件供应商提供单个驱动程序支持多个 Windows 版本的二进制移植辅助工具。</p></td>
</tr>
<tr class="even">
<td><p><a href="multiple-binary-opt-in-pool-nx-optin-auto.md" data-raw-source="[Multiple Binary Opt-In: POOL_NX_OPTIN_AUTO](multiple-binary-opt-in-pool-nx-optin-auto.md)">多个二进制参加：POOL_NX_OPTIN_AUTO</a></p></td>
<td><p>如果您的硬件供应商提供不同的驱动程序二进制文件的不同版本的 Windows，您可以使用 POOL_NX_OPTIN_AUTO 参加机制。 对 Windows 8 和 Windows 驱动程序支持的每个早期版本，此移植帮助生成单独的驱动程序二进制文件。</p></td>
</tr>
<tr class="odd">
<td><p><a href="selective-opt-out-pool-nx-optout.md" data-raw-source="[Selective Opt-Out: POOL_NX_OPTOUT](selective-opt-out-pool-nx-optout.md)">选择性退出：POOL_NX_OPTOUT</a></p></td>
<td><p>可以全局启用一种不执行 (NX) 池参加机制的一套驱动程序源文件，然后，重写为一个或多个选定的源文件与 POOL_NX_OPTOUT 此选择机制。 这样，所选的源代码文件，以继续使用可执行文件的非分页的内存。 与 POOL_NX_OPTIN 或 POOL_NX_OPTIN_AUTO 参加机制，可以使用 POOL_NX_OPTOUT 选择退出机制。</p></td>
</tr>
</tbody>
</table>

 

 

 




