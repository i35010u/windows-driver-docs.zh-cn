---
title: 错误记录
description: 错误记录
ms.assetid: 080da29a-b5cb-45a5-848d-048d9612ee2a
keywords:
- Windows 硬件错误体系结构 WDK，错误记录
- WHEA WDK，错误记录
- 错误 WDK WHEA，错误记录
- 错误记录 WDK WHEA
- 错误记录格式 WDK WHEA
- 错误记录的标头 WDK WHEA
- 错误记录部分 WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a2813b78757b9740ac5a7c0ae516a5d6568f7d8e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575962"
---
# <a name="error-records"></a>错误记录


Windows 硬件错误体系结构 (WHEA) 使用标准错误记录格式来表示所有平台的硬件错误。 因此，系统固件、 Windows 操作系统和用户模式应用程序可以设计硬件错误报告和恢复机制都基于相同的错误记录格式。

基于由 WHEA 错误记录的格式*常见平台错误记录*版本 2.2 的附录 N 中所述[统一可扩展固件接口 (UEFI) 规范](https://go.microsoft.com/fwlink/p/?linkid=69484).

下图显示错误记录的一般的格式。

![说明错误记录的一般格式的关系图](images/whearecord.png)

错误记录包含后跟一个或多个固定长度错误记录段描述符的错误记录标头。 对于每个错误记录部分描述符没有包含错误数据或信息性数据相关联的变量长度错误记录部分。 错误记录必须包含至少一个错误记录部分。

错误记录可以包括错误记录各节和节描述符的动态添加额外的缓冲空间。 额外的缓冲空间还可用来动态增加现有错误记录各节的大小。

错误记录所描述[ **WHEA\_错误\_记录**](https://msdn.microsoft.com/library/windows/hardware/ff560483)描述的错误记录标头结构[ **WHEA\_错误\_记录\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff560487)结构和错误记录段描述符每个描述了[ **WHEA\_错误\_记录\_一节\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff560496)结构。

每个错误记录部分可以是以下部分类型之一：

<a href="" id="hardware-error-packet"></a>硬件错误数据包  
此错误记录部分包含通过报告了错误的低级别的硬件错误处理程序 (LLHEH) 传递到操作系统的硬件错误数据包。 在本部分中包含的数据描述由[WHEA\_错误\_数据包](https://msdn.microsoft.com/library/windows/hardware/ff560465)结构。

<a href="" id="generic-processor-error"></a>泛型处理器错误  
此错误记录部分包含不是特定于特定的处理器体系结构的处理器错误数据。 在本部分中包含的数据描述由[ **WHEA\_处理器\_泛型\_错误\_部分**](https://msdn.microsoft.com/library/windows/hardware/ff560607)结构。

<a href="" id="x86-x64-processor-error"></a>x86/x64 处理器错误  
此错误记录部分包含特定于 x86 或 x64 处理器体系结构的处理器错误数据。 在本部分中包含的数据描述由[ **WHEA\_XPF\_处理器\_错误\_部分**](https://msdn.microsoft.com/library/windows/hardware/ff560655)结构。 下图显示了如何将包含处理器错误数据的数据结构存储在 VariableInfo 成员。 

![处理器错误数据](images/wheaxpfsection.gif)

<a href="" id="itanium-processor-error"></a>Itanium 处理器错误  
此错误记录部分包含特定于 Itanium 处理器体系结构的处理器错误数据。 有关此错误记录部分包含的错误数据的格式的详细信息，请参阅[Intel Itanium 处理器系列系统抽象层规范](https://go.microsoft.com/fwlink/p/?linkid=72212)。

<a href="" id="itanium-processor-firmware-error-record-reference"></a>Itanium 处理器固件错误记录参考  
此错误记录部分包含对特定于 Itanium 处理器体系结构的固件错误记录的引用。 此错误记录部分所描述[ **WHEA\_固件\_错误\_记录\_引用**](https://msdn.microsoft.com/library/windows/hardware/ff560520)结构。

<a href="" id="platform-memory-error"></a>平台内存错误  
此错误记录部分包含平台内存错误数据。 在本部分中包含的数据描述由[ **WHEA\_内存\_错误\_部分**](https://msdn.microsoft.com/library/windows/hardware/ff560565)结构。

<a href="" id="nonmaskable-interrupt"></a>不可屏蔽的中断  
此错误记录部分包含不可屏蔽的中断 (NMI) 数据。 在本部分中包含的数据描述由[ **WHEA\_NMI\_错误\_部分**](https://msdn.microsoft.com/library/windows/hardware/ff560571)结构。

<a href="" id="pci-express-error"></a>PCI Express Error  
此错误记录部分包含 PCI Express 错误数据。 在本部分中包含的数据描述由[ **WHEA\_PCIEXPRESS\_错误\_部分**](https://msdn.microsoft.com/library/windows/hardware/ff560576)结构。

<a href="" id="pci-pci-x-bus-error"></a>PCI/PCI-X 总线错误  
此错误记录部分包含 PCI/PCI-X 总线错误数据。 在本部分中包含的数据描述由[ **WHEA\_PCIXBUS\_错误\_部分**](https://msdn.microsoft.com/library/windows/hardware/ff560583)结构。

<a href="" id="pci-pci-x-device-error"></a>PCI/PCI-X 设备错误  
此错误记录部分包含 PCI/PCI-X 设备错误数据。 在本部分中包含的数据描述由[ **WHEA\_PCIXDEVICE\_错误\_部分**](https://msdn.microsoft.com/library/windows/hardware/ff560589)结构。

对于不适合上述列表中的部分类型之一的附加硬件错误数据，可以定义特定于平台的错误记录部分包含的数据。 对于每种类型的特定于平台的错误记录部分定义，用于标识错误类型的相应 GUID 必须定义记录部分。 中指定此 GUID **SectionType**的任何成员[ **WHEA\_错误\_记录\_部分\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff560496)结构，描述该类型的错误记录部分。

如果没有额外的硬件错误数据不符合到上一列表中的部分类型之一或定义的特定于平台的错误记录部分，使用一般性错误记录部分包含的数据。

 

 




