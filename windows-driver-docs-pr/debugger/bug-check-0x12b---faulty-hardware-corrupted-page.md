---
title: Bug 检查 0x12B FAULTY_HARDWARE_CORRUPTED_PAGE
description: FAULTY_HARDWARE_CORRUPTED_PAGE bug 检查具有 0x0000012B 值。 此 bug 检查指示 Windows 内存管理器检测到损坏，并且损坏可能只是由访问内存使用物理寻址的组件。
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
ms.openlocfilehash: 02cd8f6a04923fb0da6d64e7f2bb8e77fee732fd
ms.sourcegitcommit: fb8b1d2e18dd727e8a479b04c9e6051e7e9fa484
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2019
ms.locfileid: "59238614"
---
# <a name="bug-check-0x12b-faultyhardwarecorruptedpage"></a>Bug 检查 0x12B：发生故障\_硬件\_损坏\_页

故障\_硬件\_损坏\_页 bug 检查的值为 0x0000012B。 此 bug 检查指示 Windows 内存管理器检测到损坏，并且损坏可能只是由访问内存使用物理寻址的组件。  

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="faultyhardwarecorruptedpage-parameters"></a>发生故障\_硬件\_损坏\_页参数

有两种方案，内存管理器将引发 FAULTY_HARDWARE_CORRUPTED_PAGE bug 检查，与两个不同的参数集。 

如果参数 3 和 4 均为零，bug 检查指示内存管理器检测到应清除的页面上的单一位错误。

如果参数 3 和 4 为非零值，由于无法解压缩由于物理内存损坏的页压缩的存储管理器将引发错误检查。


### <a name="memory-manager-page-not-zero-error-parameters"></a>内存管理器页不为零的错误参数 

此 bug 检查指示，在此页中找到的单一位错误。 这是硬件内存错误。

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
<td align="left"><p>虚拟地址映射到已损坏的页面</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>物理页号</p></td>
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

 此 bug 检查指示已发生的存储管理器内存错误。 它可以是身份验证失败、 CRC 故障时或解压缩失败。

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
<td align="left"><p>FailStatus-指示故障的类型</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>正在读取页的 CompressedSize</p></td>
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

由于物理内存访问的内存损坏，才会发生此错误检查。 物理内存损坏的原因包括：

1.  出现故障的 RAM 硬件
2.  驱动程序或设备不当地修改通过 DMA 操作不正确或关联的 MDL 物理页。
3.  硬件设备或固件损坏内存，例如固件非法跨电源转换修改物理页引起的损坏。

注意：如果单一位错误，导致的损坏，并且会自动更正这种情况不会生成错误检查，可以检测到压缩的存储管理器。 如果损坏不由单个位错误，压缩的存储管理器会报告此错误检查。

Windows 内存管理器和内存压缩的详细信息，请参阅[第 1 部分 Windows 内部结构第七版](https://docs.microsoft.com/en-us/sysinternals/learn/windows-internals)通过 Pavel Yosifovich、 Mark E.Russinovich、 David A.Solomon 和 Alex Ionescu。


## <a name="resolution"></a>分辨率
-----

**Windows 内存诊断工具**

若要调查如果此 bug 检查由有故障 RAM 的硬件，运行 Windows 内存诊断工具。 在控件面板的搜索框中，键入内存，然后单击*诊断您的计算机的内存问题*。在测试运行后，使用事件查看器查看系统日志下的结果。 寻找*MemoryDiagnostics 结果*条目以查看结果。


## <a name="see-also"></a>请参阅
----------

[Bug 检查代码参考](bug-check-code-reference2.md)

[Windows Kernel-Mode Memory Manager](https://docs.microsoft.com/en-us/windows-hardware/drivers/kernel/windows-kernel-mode-memory-manager)

[第 9 频道视频内存压缩](https://channel9.msdn.com/Blogs/Seth-Juarez/Memory-Compression-in-Windows-10-RTM)

 

 




