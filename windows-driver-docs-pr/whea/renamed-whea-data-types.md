---
title: 重命名的 WHEA 数据类型
description: 重命名的 WHEA 数据类型
ms.assetid: e2c511a2-fd6e-4c7a-a47f-eb9b9f917bb4
keywords:
- Windows 硬件错误体系结构 WDK，已重命名的数据类型
- WHEA WDK 重命名数据类型
- 硬件错误 WDK WHEA，已重命名的数据类型
- 已重命名的数据类型 WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c564fe152a01f57a2406bd9e9002cb22f32e8ab1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387148"
---
# <a name="renamed-whea-data-types"></a>重命名的 WHEA 数据类型


从开始使用 Windows 7 Windows Driver Kit (WDK) 一起，各种 WHEA 数据类型已重命名从早期版本的 WDK。 大多数这些更改所做，以便在 WDK 中的命名约定是一致的命名约定*常见平台错误记录*格式。 此格式所述的版本 2.2 的附录 N[统一可扩展固件接口 (UEFI) 规范](https://go.microsoft.com/fwlink/p/?linkid=69484)。

在本部分中列出的数据类型不修订了针对 Windows 7。 例如，列表和类型的已重命名结构中的成员未更改，尽管将成员自己可能已重命名。

如果你正在开发新[特定于平台的硬件错误驱动程序 (PSHED) 插件](platform-specific-hardware-error-driver-plug-ins2.md)，使用 Windows 7 和更高版本的 WDK 中定义的新 WHEA 数据类型名称。

如果您正在构建 Windows 7 和更高版本的 WDK 插件现有 PSHED，仍可以使用以前的 WHEA 数据类型名称。 若要执行此操作，将以下代码添加到*源*用于生成该插件的文件：

`C_DEFINES = $(C_DEFINES) /DWHEA_DOWNLEVEL_TYPE_NAMES`

但是，对于现有 PSHED 插件，我们强烈建议通过使用 Windows 7 和更高版本的 WDK 中定义的名称的 WHEA 数据类型重命名。

下表列出了 WHEA 数据类型的以前和新名称。

### <a href="" id="renamed-whea-globally-unique-identifiers--guids-"></a> 已重命名的 WHEA 全局唯一标识符 (Guid)

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>以前的名称 （在 Windows 7 之前的 WDK 版本）</th>
<th>新名称 (Windows 7 WDK 和更高版本)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>IPF_PROCESSOR_SPECIFIC_SECTION_GUID</p></td>
<td><p>IPF_PROCESSOR_ERROR_SECTION_GUID</p></td>
</tr>
<tr class="even">
<td><p>IPF_SAL_RECORD_REFERENCE_SECTION_GUID</p></td>
<td><p>FIRMWARE_ERROR_RECORD_REFERENCE_GUID</p></td>
</tr>
<tr class="odd">
<td><p>PCIEXPRESS_SECTION_GUID</p></td>
<td><p>PCIEXPRESS_ERROR_SECTION_GUID</p></td>
</tr>
<tr class="even">
<td><p>PCIX_BUS_SECTION_GUID</p></td>
<td><p>PCIXBUS_ERROR_SECTION_GUID</p></td>
</tr>
<tr class="odd">
<td><p>PCIX_COMPONENT_SECTION_GUID</p></td>
<td><p>PCIXBUS_ERROR_SECTION_GUID</p></td>
</tr>
<tr class="even">
<td><p>PLATFORM_MEMORY_SECTION_GUID</p></td>
<td><p>MEMORY_ERROR_SECTION_GUID</p></td>
</tr>
<tr class="odd">
<td><p>PROCESSOR_GENERIC_SECTION_GUID</p></td>
<td><p>PROCESSOR_GENERIC_ERROR_SECTION_GUID</p></td>
</tr>
<tr class="even">
<td><p>X86_PROCESSOR_SPECIFIC_SECTION_GUID</p></td>
<td><p>XPF_PROCESSOR_ERROR_SECTION_GUID</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="renamed-whea-defines"></a> 已重命名的 WHEA 定义

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>以前的名称 （在 Windows 7 之前的 WDK 版本）</th>
<th>新名称 (Windows 7 WDK 和更高版本)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WHEA_SECTION_DESCRIPTOR_REVISION</p></td>
<td><p>WHEA_ERROR_RECORD_SECTION_DESCRIPTOR_REVISION</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="renamed-whea-structures-and-unions"></a> 已重命名的 WHEA 结构和联合

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>以前的名称 （在 Windows 7 之前的 WDK 版本）</th>
<th>新名称 (Windows 7 WDK 和更高版本)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WHEA_FIRMWARE_RECORD</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_whea_firmware_error_record_reference" data-raw-source="[&lt;strong&gt;WHEA_FIRMWARE_ERROR_RECORD_REFERENCE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_whea_firmware_error_record_reference)"><strong>WHEA_FIRMWARE_ERROR_RECORD_REFERENCE</strong></a></p></td>
</tr>
<tr class="even">
<td><p>WHEA_GENERIC_PROCESSOR_ERROR</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_whea_processor_generic_error_section" data-raw-source="[&lt;strong&gt;WHEA_PROCESSOR_GENERIC_ERROR_SECTION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_whea_processor_generic_error_section)"><strong>WHEA_PROCESSOR_GENERIC_ERROR_SECTION</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>WHEA_GENERIC_PROCESSOR_ERROR_VALIDBITS</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_whea_processor_generic_error_section_validbits" data-raw-source="[&lt;strong&gt;WHEA_PROCESSOR_GENERIC_ERROR_SECTION_VALIDBITS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_whea_processor_generic_error_section_validbits)"><strong>WHEA_PROCESSOR_GENERIC_ERROR_SECTION_VALIDBITS</strong></a></p></td>
</tr>
<tr class="even">
<td><p>WHEA_MEMORY_ERROR</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_whea_memory_error_section" data-raw-source="[&lt;strong&gt;WHEA_MEMORY_ERROR_SECTION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_whea_memory_error_section)"><strong>WHEA_MEMORY_ERROR_SECTION</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>WHEA_MEMORY_ERROR_VALIDBITS</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_whea_memory_error_section_validbits" data-raw-source="[&lt;strong&gt;WHEA_MEMORY_ERROR_SECTION_VALIDBITS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_whea_memory_error_section_validbits)"><strong>WHEA_MEMORY_ERROR_SECTION_VALIDBITS</strong></a></p></td>
</tr>
<tr class="even">
<td><p>WHEA_NMI_ERROR</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_whea_nmi_error_section" data-raw-source="[&lt;strong&gt;WHEA_NMI_ERROR_SECTION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_whea_nmi_error_section)"><strong>WHEA_NMI_ERROR_SECTION</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>WHEA_PCIEXPRESS_ERROR</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_whea_pciexpress_error_section" data-raw-source="[&lt;strong&gt;WHEA_PCIEXPRESS_ERROR_SECTION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_whea_pciexpress_error_section)"><strong>WHEA_PCIEXPRESS_ERROR_SECTION</strong></a></p></td>
</tr>
<tr class="even">
<td><p>WHEA_PCIEXPRESS_ERROR_VALIDBITS</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_whea_pciexpress_error_section_validbits" data-raw-source="[&lt;strong&gt;WHEA_PCIEXPRESS_ERROR_SECTION_VALIDBITS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_whea_pciexpress_error_section_validbits)"><strong>WHEA_PCIEXPRESS_ERROR_SECTION_VALIDBITS</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>WHEA_PCIXBUS_ERROR</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_whea_pcixbus_error_section" data-raw-source="[&lt;strong&gt;WHEA_PCIXBUS_ERROR_SECTION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_whea_pcixbus_error_section)"><strong>WHEA_PCIXBUS_ERROR_SECTION</strong></a></p></td>
</tr>
<tr class="even">
<td><p>WHEA_PCIXBUS_ERROR_VALIDBITS</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_whea_pcixbus_error_section_validbits" data-raw-source="[&lt;strong&gt;WHEA_PCIXBUS_ERROR_SECTION_VALIDBITS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_whea_pcixbus_error_section_validbits)"><strong>WHEA_PCIXBUS_ERROR_SECTION_VALIDBITS</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>WHEA_PCIXDEVICE_ERROR</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_whea_pcixdevice_error_section" data-raw-source="[&lt;strong&gt;WHEA_PCIXDEVICE_ERROR_SECTION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_whea_pcixdevice_error_section)"><strong>WHEA_PCIXDEVICE_ERROR_SECTION</strong></a></p></td>
</tr>
<tr class="even">
<td><p>WHEA_PCIXDEVICE_ERROR_VALIDBITS</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_whea_pcixdevice_error_section_validbits" data-raw-source="[&lt;strong&gt;WHEA_PCIXDEVICE_ERROR_SECTION_VALIDBITS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_whea_pcixdevice_error_section_validbits)"><strong>WHEA_PCIXDEVICE_ERROR_SECTION_VALIDBITS</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>WHEA_XPF_PROCESSOR_ERROR</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff560655" data-raw-source="[&lt;strong&gt;WHEA_XPF_PROCESSOR_ERROR_SECTION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560655)"><strong>WHEA_XPF_PROCESSOR_ERROR_SECTION</strong></a></p></td>
</tr>
<tr class="even">
<td><p>WHEA_XPF_PROCESSOR_ERROR_VALIDBITS</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff560657" data-raw-source="[&lt;strong&gt;WHEA_XPF_PROCESSOR_ERROR_SECTION_VALIDBITS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560657)"><strong>WHEA_XPF_PROCESSOR_ERROR_SECTION_VALIDBITS</strong></a></p></td>
</tr>
</tbody>
</table>

 

 

 




