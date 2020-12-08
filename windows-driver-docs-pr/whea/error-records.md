---
title: 错误记录
description: 错误记录
keywords:
- Windows 硬件错误体系结构 WDK，错误记录
- WHEA WDK，错误记录
- 错误 WDK WHEA，错误记录
- 错误记录 WDK WHEA
- 错误记录格式 WDK WHEA
- 错误记录标头 WDK WHEA
- 错误记录部分 WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11aadad95c380e45f304d55bb899fd2c0bf2a3df
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824821"
---
# <a name="error-records"></a>错误记录


Windows 硬件错误体系结构 (WHEA) 使用标准错误记录格式来表示所有平台硬件错误。 因此，系统固件、Windows 操作系统和用户模式应用程序可以设计硬件错误报告和恢复机制，它们都基于相同的错误记录格式。

WHEA 使用的错误记录格式基于 *常见平台错误记录* (CPER) ，如 [统一可扩展固件接口 (UEFI) 规范](https://go.microsoft.com/fwlink/p/?linkid=69484)的版本2.2 中的附录 N 所述。

下图显示了错误记录的一般格式。

![说明错误记录的一般格式的关系图](images/whearecord.png)

错误记录由错误记录标头和后跟一个或多个固定长度错误记录部分说明符组成。 对于每个错误记录部分描述符，都有一个关联的可变长度错误记录部分，其中包含错误数据或信息性数据。 错误记录必须包含至少一个错误记录部分。

错误记录可能包括用于动态添加错误记录部分和节描述符的额外缓冲区空间。 额外的缓冲区空间还可用于动态增加现有错误记录部分的大小。

错误记录由 [**WHEA \_ 错误 \_ 记录**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_error_record) 结构描述，错误记录标头由 [**WHEA \_ 错误 \_ 记录 \_ 标头**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_error_record_header) 结构描述，错误记录部分描述符由 [**WHEA \_ 错误 \_ 记录 \_ 部分 \_ 描述符**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_error_record_section_descriptor) 结构描述。

每个错误记录部分可以是以下部分类型之一：

<a href="" id="hardware-error-packet"></a>硬件错误数据包  
此错误记录部分包含硬件错误数据包，该数据包由低级硬件错误处理程序传递给操作系统 (LLHEH) 报告了该错误。 此部分中包含的数据由 [WHEA \_ 错误 \_ 数据包](/previous-versions/windows/hardware/drivers/ff560465(v=vs.85)) 结构描述。

<a href="" id="generic-processor-error"></a>一般处理器错误  
此错误记录部分包含不特定于特定处理器体系结构的处理器错误数据。 本部分包含的数据由 [**WHEA \_ 处理器 \_ 一般 \_ 错误 \_ 部分**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_processor_generic_error_section) 结构描述。

<a href="" id="x86-x64-processor-error"></a>x86/x64 处理器错误  
此错误记录部分包含特定于 x86 或 x64 处理器体系结构的处理器错误数据。 本部分包含的数据由 [**WHEA \_ XPF \_ 处理器 \_ 错误 \_ 部分**](/previous-versions/ff560655(v=vs.85)) 结构描述。 下图显示了包含处理器错误数据的数据结构如何存储在 VariableInfo 成员中。 

![处理器错误数据](images/wheaxpfsection.gif)

<a href="" id="itanium-processor-error"></a>Itanium 处理器错误  
此错误记录部分包含特定于 Itanium 处理器体系结构的处理器错误数据。 有关此错误记录部分中包含的错误数据格式的详细信息，请参阅 [Intel Itanium 处理器系列系统抽象层规范](https://go.microsoft.com/fwlink/p/?linkid=72212)。

<a href="" id="itanium-processor-firmware-error-record-reference"></a>Itanium 处理器固件错误记录引用  
此错误记录部分包含对特定于 Itanium 处理器体系结构的固件错误记录的引用。 此错误记录部分由 [**WHEA \_ 固件 \_ 错误 \_ 记录 \_ 引用**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_firmware_error_record_reference) 结构描述。

<a href="" id="platform-memory-error"></a>平台内存错误  
此错误记录部分包含平台内存错误数据。 本部分包含的数据由 [**WHEA \_ 内存 \_ 错误 \_ 部分**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_memory_error_section) 结构描述。

<a href="" id="nonmaskable-interrupt"></a>不可屏蔽中断  
此错误记录部分包含 (NMI) 数据的不可屏蔽中断。 本部分包含的数据由 [**WHEA \_ NMI \_ 错误 \_ 部分**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_nmi_error_section) 结构描述。

<a href="" id="pci-express-error"></a>PCI Express 错误  
此错误记录部分包含 PCI Express 错误数据。 本节中包含的数据由 [**WHEA \_ PCIEXPRESS \_ 错误 \_ 部分**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_pciexpress_error_section) 结构描述。

<a href="" id="pci-pci-x-bus-error"></a>PCI/PCI-X 总线错误  
此错误记录部分包含 PCI/PCI-X 总线错误数据。 本节中包含的数据由 [**WHEA \_ PCIXBUS \_ 错误 \_ 部分**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_pcixbus_error_section) 结构描述。

<a href="" id="pci-pci-x-device-error"></a>PCI/PCI-X 设备错误  
此错误记录部分包含 PCI/PCI-X 设备错误数据。 本节中包含的数据由 [**WHEA \_ PCIXDEVICE \_ 错误 \_ 部分**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_pcixdevice_error_section) 结构描述。

对于不属于上一列表部分类型的其他硬件错误数据，可以定义特定于平台的错误记录部分来包含数据。 对于定义的每个特定于平台的错误记录部分类型，必须定义标识错误记录部分类型的相应 GUID。 此 GUID 是在描述该类型错误记录部分的任何 [**WHEA \_ 错误 \_ 记录 \_ 部分 \_ 描述符**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_error_record_section_descriptor)结构的 **SectionType** 成员中指定的。

如果有其他硬件错误数据无法适应上一列表中的一种节类型或定义的特定于平台的错误记录部分，则使用一般错误记录部分来包含数据。

 

