---
title: Bug 检查 0x1C7 STORE_DATA_STRUCTURE_CORRUPTION
description: STORE_DATA_STRUCTURE_CORRUPTION bug 检查具有 0x000001C7 值。 它指示，存储组件在其数据结构中检测到损坏。
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
ms.openlocfilehash: 422218ac6fb5f1441997f01ecce1f81194a94e7b
ms.sourcegitcommit: fb8b1d2e18dd727e8a479b04c9e6051e7e9fa484
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2019
ms.locfileid: "59238976"
---
# <a name="bug-check-0x1c7-storedatastructurecorruption"></a>Bug 检查 0x1C7：应用商店\_数据\_结构\_损坏

应用商店\_数据\_结构\_损坏错误检查的值为 0x000001C7。 它指示，存储组件在其数据结构中检测到损坏。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

 

## <a name="storedatastructurecorruption-parameters"></a>应用商店\_数据\_结构\_损坏参数

|参数|描述|
|-------- |---------- |
|1|损坏 id。 请参阅下面的值。 |
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

存储组件在其数据结构中检测到损坏。

可以通过由于物理内存访问的内存损坏会发生此错误检查。 物理内存损坏的原因包括：

1.  出现故障的 RAM 硬件
2.  驱动程序或设备不当地修改通过 DMA 操作不正确或关联的 MDL 物理页。
3.  硬件设备或固件损坏内存，例如固件非法跨电源转换修改物理页引起的损坏。

Windows 内存管理器的详细信息，请参阅[第 1 部分 Windows 内部结构第七版](https://docs.microsoft.com/en-us/sysinternals/learn/windows-internals)通过 Pavel Yosifovich、 Mark E.Russinovich、 David A.Solomon 和 Alex Ionescu。

## <a name="resolution"></a>分辨率
-----

**Windows 内存诊断工具**

若要调查如果此 bug 检查由有故障 RAM 的硬件，运行 Windows 内存诊断工具。 在控件面板的搜索框中，键入内存，然后单击*诊断您的计算机的内存问题*。在测试运行后，使用事件查看器查看系统日志下的结果。 寻找*MemoryDiagnostics 结果*条目以查看结果。

## <a name="see-also"></a>请参阅
----------

[Bug 检查代码参考](bug-check-code-reference2.md)

[Windows Kernel-Mode Memory Manager](https://docs.microsoft.com/en-us/windows-hardware/drivers/kernel/windows-kernel-mode-memory-manager)
