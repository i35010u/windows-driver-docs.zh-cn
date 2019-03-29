---
title: Bug 检查 0x108 THIRD_PARTY_FILE_SYSTEM_FAILURE
description: THIRD_PARTY_FILE_SYSTEM_FAILURE bug 检查具有 0x00000108 值。 这表示第三方文件系统或文件系统筛选器中出现不可恢复的问题。
ms.assetid: 1ed82617-b0f0-4b41-9af9-b309b6b75dfd
keywords:
- Bug 检查 0x108 THIRD_PARTY_FILE_SYSTEM_FAILURE
- THIRD_PARTY_FILE_SYSTEM_FAILURE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- THIRD_PARTY_FILE_SYSTEM_FAILURE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c14c440df742e2c3651a7bc862872db3a9e98f50
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565702"
---
# <a name="bug-check-0x108-thirdpartyfilesystemfailure"></a>Bug 检查 0x108：第三个\_参与方\_文件\_系统\_失败


第三个\_参与方\_文件\_系统\_故障错误检查的值为 0x00000108。 这表示第三方文件系统或文件系统筛选器中出现不可恢复的问题。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="thirdpartyfilesystemfailure-parameters"></a>第三个\_参与方\_文件\_系统\_失败参数


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>标识失败的文件系统。 可能值的包括：</p>
<p><strong>1:</strong>Polyserve (Psfs.sys)</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>异常记录的地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>上下文记录的地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>保留。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

此 bug 检查的一个可能的原因是磁盘损坏。 第三方文件系统或在硬盘上的坏扇区 （扇区） 中的损坏可导致此错误。 损坏的 SCSI 和 IDE 驱动程序可能会反过来会影响 Windows 操作系统的能力来读取和写入到磁盘，因此这会导致错误。

另一个可能原因是非分页缓冲的池内存耗尽。 如果非分页缓冲的池完全耗尽时，此错误可以停止系统。

<a name="resolution"></a>分辨率
----------

**若要调试此问题：** 使用[ **.cxr （显示上下文记录）** ](-cxr--display-context-record-.md)命令参数 3 中，并使用[ **kb （显示堆栈回溯）**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)。

**若要解决磁盘损坏问题：** 事件查看器检查从 SCSI、 IDE 或其他磁盘控制器的错误消息可能有助于确定该设备或导致错误的驱动程序的系统中。 请尝试禁用任何病毒扫描程序、 备份程序或持续监视系统的磁盘碎片整理程序工具。 您还应运行硬件诊断由文件系统或文件系统筛选器制造商提供。

**若要解决非分页缓冲的池内存耗尽问题：** 向计算机添加新的物理内存。 这会增加可用的内核的非分页缓冲的池内存的数量。

 

 




