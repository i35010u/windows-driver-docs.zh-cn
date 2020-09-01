---
title: Bug 检查 0x12B FAULTY_HARDWARE_CORRUPTED_PAGE
description: FAULTY_HARDWARE_CORRUPTED_PAGE bug 检查的值为0x0000012B。 此 bug 检查表明 Windows 内存管理器检测到损坏，损坏可能仅由使用物理寻址访问内存的组件引起。
ms.assetid: caa57d76-946f-4394-bfcf-1dbf3813a55b
keywords:
- Bug 检查 0x12B FAULTY_HARDWARE_CORRUPTED_PAGE
- FAULTY_HARDWARE_CORRUPTED_PAGE
ms.date: 01/18/2019
topic_type:
- apiref
api_name:
- FAULTY_HARDWARE_CORRUPTED_PAGE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 30ef030d04d55f199ab1d956a751f407dd370bed
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208739"
---
# <a name="bug-check-0x12b-faulty_hardware_corrupted_page"></a>Bug 检查0x12B：出错的 \_ 硬件 \_ 损坏 \_ 页

错误的 \_ 硬件 \_ 损坏 \_ 页面 bug 检查的值为0x0000012B。 此 bug 检查表明 Windows 内存管理器检测到损坏，损坏可能仅由使用物理寻址访问内存的组件引起。  

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="faulty_hardware_corrupted_page-parameters"></a>错误的 \_ 硬件 \_ 损坏 \_ 页面参数

在两种情况下，内存管理器将引发 FAULTY_HARDWARE_CORRUPTED_PAGE 错误检查，其中包含两个不同的参数集。 

如果参数3和4均为零，则 bug 检查表示内存管理器检测到应为归零的页面上出现单一位错误。

如果参数3和4为非零，则压缩存储管理器将引发 bug 检查，因为由于物理内存损坏，无法解压缩页面。


### <a name="memory-manager-page-not-zero-error-parameters"></a>内存管理器页不为零错误参数 

此 bug 检查指示在此页中发现了单一位错误。 这是硬件内存错误。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>虚拟地址映射到损坏的页</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>物理页码</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>零</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>零</p></td>
</tr>
</tbody>
</table>


### <a name="compressed-store-manager-error-parameters"></a>压缩的存储管理器错误参数 

 此 bug 检查表明发生了存储管理器内存错误。 这可能是身份验证失败、CRC 故障或解压缩失败。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>FailStatus-指示故障类型</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>正在读取的页的 CompressedSize</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>源缓冲区</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>目标缓冲区</p></td>
</tr>
</tbody>
</table>


## <a name="cause"></a>原因
-----

此错误检查只能由物理内存访问导致的内存损坏导致。 物理内存损坏的原因包括：

1. RAM 硬件故障
2. 驱动程序或设备通过不正确的 DMA 操作或关联的 MDL 错误地修改物理页。
3. 硬件设备或固件损坏内存导致的损坏，如固件在电源转换中非法修改物理页。

注意：压缩的存储管理器可以检测是否损坏是由单一位错误引起的，并自动更正此情况，而不引发 bug 检查。 如果损坏不是由单一位错误引起的，则压缩的存储管理器会报告此错误检测。

有关 Windows 内存管理器和内存压缩的详细信息，请参阅 [Windows 内部版本第7版](/sysinternals/learn/windows-internals) ，Pavel Yosifovich，标记 Russinovich，David，David，Alex Ionescu。

## <a name="resolution"></a>解决方法
-----

**Windows 内存诊断工具**

若要调查此 bug 检查是否是由 RAM 硬件故障引起的，请运行 Windows 内存诊断工具。 在 "控制面板" 搜索框中键入 "内存"，然后选择 " *诊断计算机的内存问题*"。运行测试后，使用事件查看器查看系统日志下的结果。 查找“内存诊断结果”条目以查看结果  。

## <a name="see-also"></a>另请参阅
----------

[Bug 检查代码参考](bug-check-code-reference2.md)

[Windows 内核模式内存管理器](../kernel/windows-kernel-mode-memory-manager.md)

[内存压缩的第9频道视频](https://channel9.msdn.com/Blogs/Seth-Juarez/Memory-Compression-in-Windows-10-RTM)