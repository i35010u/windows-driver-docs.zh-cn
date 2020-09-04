---
title: 硬件 ID
description: 硬件 ID 是供应商定义的标识字符串，Windows 使用该字符串将设备与 INF 文件匹配。
ms.assetid: 9eb894d6-4e83-4c08-8165-f30d6636da75
ms.date: 04/20/2017
ms.localizationpriority: High
ms.openlocfilehash: 70138aeb0d105bfd15d067dd5b793261b9cf0be0
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095309"
---
# <a name="hardware-id"></a>硬件 ID


硬件 ID 是供应商定义的标识字符串，Windows 使用该字符串将设备与 INF 文件匹配。 在大多数情况下，设备有一个与之关联的硬件 ID 列表。 但是，有一些例外 − 请参阅“1394 设备的标识符”，其中报告了设备的硬件 ID 列表，硬件 ID 应按适用性降序列出。




硬件 ID 具有以下通用格式之一：

`<enumerator>\<enumerator-specific-device-ID>`

这是单个枚举器报告给即插即用 (PnP) 管理器的单个 PnP 设备的最常见格式。 新枚举器应使用此格式或以下格式。 有关特定于枚举器的设备 ID 的详细信息，请参阅[设备标识符格式](device-identifier-formats.md)。

`\*<generic-device-ID>`

星号表示设备受多个枚举器支持，如 ISAPNP 和 BIOS。 有关此类型的 ID 的详细信息，请参阅[通用标识符](generic-identifiers.md)。

`<device-class-specific-ID>`

## <a name="selecting-a-hardware-id"></a>选择硬件 ID

共享通用命名空间（如 `ROOT\SYSTEM`）的根枚举设备可能会导致在操作系统升级时出现冲突，并且设备管理器中会显示黄色感叹号。

为防止出现这种情况，请为每个驱动程序使用包含根枚举设备的唯一命名空间。 对于 USB 或系统设备，请使用 `ROOT\[COMPANYNAME]\[DEVICENAME]`，而不是使用 `ROOT\USB` 或 `ROOT\SYSTEM”`。  此外，驱动程序安装程序代码还应检查 devnode 是否已存在，并在安装前采取任何必要的更正措施。

已建立自己的命名约定的现有设备类可能会使用自定义格式。 有关其硬件 ID 格式的信息，请参阅此类总线的硬件规范。 新枚举器不应使用此格式。

硬件 ID 的字符数（不包括 NULL 终止符）必须小于 MAX_DEVICE_ID_LEN。 此约束适用于硬件 ID 中所有字段与任何“\\”字段分隔符的长度总和。 有关设备 ID 上的约束的详细信息，请参阅 [**IRP_MN_QUERY_ID**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-id) 的“操作”部分。

## <a name="obtaining-the-list-of-hardware-ids-for-a-device"></a>获取设备的硬件 ID 列表

若要获取设备的硬件 ID 列表，请在将 *DeviceProperty* 参数设置为 **DevicePropertyHardwareID** 的情况下调用 [**IoGetDeviceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty)。 此例程检索到的硬件 ID 列表是一个 [REG_MULTI_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types) 值。 硬件列表中的字符的最大数目（包括每个硬件 ID 后的 NULL 终止符和最终 NULL 终止符）为 REGSTR_VAL_MAX_HCID_LEN。 硬件 ID 列表中最多可以包含的 ID 数为 64 个。

## <a name="examples-of-hardware-ids"></a>硬件 ID 示例

在下面的示例中，第一个示例是 PnP 设备的[通用标识符](generic-identifiers.md)，第二个示例是 [PCI 设备的标识符](identifiers-for-pci-devices.md)：

`root\*PNP0F08`

`PCI\VEN_1000&DEV_0001&SUBSYS_00000000&REV_02`





## <a name="see-also"></a>另请参阅

[INF HardwareId 指令](./inf-hardwareid-directive.md)