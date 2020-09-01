---
title: Bug 检查 0x1C7 STORE_DATA_STRUCTURE_CORRUPTION
description: STORE_DATA_STRUCTURE_CORRUPTION bug 检查的值为0x000001C7。 它指示存储区组件检测到其数据结构有损坏。
keywords:
- Bug 检查 0x1C7 STORE_DATA_STRUCTURE_CORRUPTION
- STORE_DATA_STRUCTURE_CORRUPTION
ms.date: 01/28/2019
topic_type:
- apiref
api_name:
- STORE_DATA_STRUCTURE_CORRUPTION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a448387947d5295be102f0ccac42967126c6aebd
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214840"
---
# <a name="bug-check-0x1c7-store_data_structure_corruption"></a>Bug 检查0x1C7：存储 \_ 数据 \_ 结构 \_ 损坏

存储 \_ 数据 \_ 结构 \_ 损坏 bug 检查的值为0x000001C7。 它指示存储区组件检测到其数据结构有损坏。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。

 

## <a name="store_data_structure_corruption-parameters"></a>存储 \_ 数据 \_ 结构 \_ 损坏参数

|参数|说明|
|-------- |---------- |
|1|损坏 ID。 请参阅下面的值。 |
|2| 请参阅下面的值。 |
|3| 请参阅下面的值。 |
|4| 请参阅下面的值。 |


**损坏 ID**

```text
 0x0 : A chunk heap buffer's hash doesn't match.
    2 - Chunk heap buffer whose hash didn't match.
    3 - Expected buffer hash.
    4 - Page frame number of the corrupted page.

 0x1 : An unhandled exception occurred on the store thread and a chunk heap buffer's hash doesn't match, which is likely the source of the exception.
    2 - Chunk heap buffer whose hash didn't match.
    3 - Expected buffer hash.
    4 - Page frame number of the corrupted page.

 0x2 : Page data appears corrupt during a read and the corresponding page record's heap buffer hash doesn't match.
    2 - Chunk heap buffer whose hash didn't match containing the page record of the data being read.
    3 - Expected buffer hash.
    4 - Page frame number of the corrupted page.
 
 0x3 : Page data appears corrupt during a read and the corresponding page record has changed since the start of the read operation.
    2 - Pointer to the page location information snapped from the page record that was found when the read was initiated.
    3 - Pointer to the page record currently in the page tree for the same page key.
    4 - Reserved.
```

## <a name="cause"></a>原因
-----

存储区组件检测到其数据结构损坏。

由于物理内存访问导致内存损坏，可能会发生此错误检测。 物理内存损坏的原因包括：

1.  RAM 硬件故障
2.  驱动程序或设备通过不正确的 DMA 操作或关联的 MDL 错误地修改物理页。
3.  硬件设备或固件损坏内存导致的损坏，如固件在电源转换中非法修改物理页。

有关 Windows 内存管理器的详细信息，请参阅 [Windows 内部版本第1部分](/sysinternals/learn/windows-internals) ，按 Pavel Yosifovich，标记 Russinovich，David，David，Alex Ionescu。

## <a name="resolution"></a>解决方法
-----

**Windows 内存诊断工具**

若要调查此 bug 检查是否是由 RAM 硬件故障引起的，请运行 Windows 内存诊断工具。 在 "控制面板" 搜索框中键入 "内存"，然后选择 " *诊断计算机的内存问题*"。运行测试后，使用事件查看器查看系统日志下的结果。 查找“内存诊断结果”条目以查看结果  。

## <a name="see-also"></a>另请参阅
----------

[Bug 检查代码参考](bug-check-code-reference2.md)

[Windows 内核模式内存管理器](../kernel/windows-kernel-mode-memory-manager.md)