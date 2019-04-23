---
title: Bug 检查 0xA4 CNSS_FILE_SYSTEM_FILTER
description: CNSS_FILE_SYSTEM_FILTER bug 检查具有 0x000000A4 值。 此 bug 检查指示 CNSS 文件系统筛选器中出现问题。
ms.assetid: fbf04b17-424c-4b9b-beae-5327d20bf0b9
keywords:
- Bug 检查 0xA4 CNSS_FILE_SYSTEM_FILTER
- CNSS_FILE_SYSTEM_FILTER
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CNSS_FILE_SYSTEM_FILTER
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 576648c2109492a229570a127fbe8cf4e190423e
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59902839"
---
# <a name="bug-check-0xa4-cnssfilesystemfilter"></a>Bug 检查 0xA4：CNSS\_FILE\_SYSTEM\_FILTER


CNSS\_文件\_系统\_筛选器错误检查的值为 0x000000A4。 此 bug 检查指示 CNSS 文件系统筛选器中出现问题。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="cnssfilesystemfilter-parameters"></a>CNSS\_文件\_系统\_筛选器参数


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
<td align="left"><p>指定源代码文件和行号信息。 高 16 位 （"0x"后的前四个十六进制数字） 标识由其标识符编号的源代码文件。 低 16 位标识发生错误检查的文件中的源行。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>保留</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>保留</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>保留</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

CNSS\_文件\_系统\_筛选器 bug 检查可能会导致非分页缓冲的池内存已满。 如果非分页缓冲的池内存占满，此错误可以停止系统。 但是，在索引过程中，如果可用的非分页缓冲的池内存量为非常低，需要非分页缓冲的池的内存的另一个内核模式驱动程序还可以触发此错误。

<a name="resolution"></a>分辨率
----------

**若要解决非分页缓冲的池内存耗尽问题：** 向计算机添加新的物理内存。 此内存 sincrease 非分页缓冲的池内存提供给内核的数量。

 

 




