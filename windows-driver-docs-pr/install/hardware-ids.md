---
title: 硬件 ID
description: 硬件 ID 是供应商定义的标识字符串，Windows 用于将设备与 INF 文件匹配。
ms.assetid: 9eb894d6-4e83-4c08-8165-f30d6636da75
ms.date: 04/20/2017
ms.localizationpriority: High
ms.openlocfilehash: 06787d3c9d10fcfc0558aafa272104672b217c13
ms.sourcegitcommit: c73954a5909ec8c7e189f77fd5813f2eb749687c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2019
ms.locfileid: "72007622"
---
# <a name="hardware-id"></a>硬件 ID


硬件 ID 是供应商定义的标识字符串，Windows 用于将设备与 INF 文件匹配。 在大多数情况下，设备具有与之关联的硬件 ID 列表。 （但是，有一些例外，例如，1394设备的标识符报告设备的硬件 Id 列表，硬件 Id 应按照降低适用性顺序列出。




硬件 ID 具有以下通用格式之一：

`<enumerator>\\<enumerator-specific-device-ID>`

这是单个枚举器报告给即插即用（PnP）管理器的单个 PnP 设备的最常见格式。 新枚举器应使用此格式或以下格式。 有关特定于枚举器的设备 Id 的详细信息，请参阅[设备标识符格式](device-identifier-formats.md)。

`\*<generic-device-ID>`

星号表示设备支持多个枚举器，如 ISAPNP 和 BIOS。 有关此 ID 类型的详细信息，请参阅[通用标识符](generic-identifiers.md)。

`<device-class-specific-ID>`

## <a name="selecting-a-hardware-id"></a>选择硬件 ID

共享常规命名空间的根枚举设备（例如 `ROOT\SYSTEM`）可能导致设备管理器中的操作系统升级发生冲突和黄色感叹号。

若要防止出现这种情况，请为每个包含根枚举设备的驱动程序使用唯一的命名空间。 对于 USB 或系统设备，不使用 `ROOT\USB` 或 `ROOT\SYSTEM”` 使用 `ROOT\[COMPANYNAME]\[DEVICENAME]`。  此外，驱动程序安装程序代码应检查 devnode 是否已存在，并在安装前采取任何必要的纠正措施。

已建立自己的命名约定的现有设备类可能使用自定义格式。 有关其硬件 ID 格式的信息，请参阅此类总线的硬件规格。 新枚举器不应使用此格式。

硬件 ID 的字符数（不包括 NULL 终止符）必须小于 MAX_DEVICE_ID_LEN。 此约束适用于所有字段的长度与硬件 ID 中的任何 "\\" 字段分隔符之和。 有关设备 Id 上的约束的详细信息，请参阅[**IRP_MN_QUERY_ID**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-id)的 "操作" 部分。

## <a name="obtaining-the-list-of-hardware-ids-for-a-device"></a>获取设备的硬件 Id 列表

若要获取设备的硬件 Id 列表，请调用[**IoGetDeviceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdeviceproperty) ，并将*DeviceProperty*参数设置为**DevicePropertyHardwareID**。 此例程检索到的硬件 Id 列表是一个[REG_MULTI_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)值。 硬件列表中的最大字符数（包括每个硬件 ID 和最终 NULL 终止符后的空终止符）为 REGSTR_VAL_MAX_HCID_LEN。 硬件 Id 列表中可能的最大 Id 数为64。

## <a name="examples-of-hardware-ids"></a>硬件 Id 示例

在下面的示例中，第一个示例是 PnP 设备的[通用标识符](generic-identifiers.md)，第二个示例是[PCI 设备的标识符](identifiers-for-pci-devices.md)：

root @ no__t-0 @ no__t-1PNP0F08

PCI @ NO__T-0VEN_1000 & DEV_0001 & SUBSYS_00000000 & REV_02





## <a name="see-also"></a>请参阅

[INF HardwareId 指令](https://docs.microsoft.com/windows-hardware/drivers/install/inf-hardwareid-directive)


