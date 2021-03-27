---
title: 硬件 ID
description: 硬件 ID 是供应商定义的标识字符串，Windows 使用该字符串将设备与 INF 文件匹配。
ms.date: 01/11/2021
ms.localizationpriority: High
ms.custom: contperf-fy21q3
ms.openlocfilehash: 4249fddba530770dd007180d742a953e6356ed2c
ms.sourcegitcommit: 76a7b604f13cf419ff21518337913820a703347f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2021
ms.locfileid: "104719460"
---
# <a name="hardware-id"></a>硬件 ID


硬件 ID 是供应商定义的标识字符串，Windows 使用该字符串将设备与 INF 文件匹配。 在大多数情况下，一个设备关联了多个硬件 ID。 通常，硬件 ID 列表按与设备的适配程度由高到低的顺序排列。

若要查找给定设备的硬件 ID，请执行以下步骤：

1. 打开“设备管理器”。
2. 在树中找到该设备。
3. 右键单击该设备并选择“属性”。
4. 选择“详细信息”选项卡。
5. 在“属性”下拉列表中，选择“硬件 ID”或“兼容 ID”。  

## <a name="creating-a-hardware-id-for-a-device"></a>为设备创建硬件 ID

通常，为设备创建新的硬件 ID 时，将使用以下通用格式之一：

`<enumerator>\<enumerator-specific-device-ID>`

这是单个枚举器报告给即插即用 (PnP) 管理器的单个 PnP 设备的最常见格式。

`\*<generic-device-ID>`

星号表示设备受多个枚举器支持，如 ISAPNP 和 BIOS。 

`<device-class-specific-ID>`

有关详细信息，请参阅[通用标识符](generic-identifiers.md)。

## <a name="selecting-a-hardware-id"></a>选择硬件 ID

更新 Windows 时，共享通用命名空间（如 `ROOT\SYSTEM`）的根枚举设备可能会发生冲突，并导致设备管理器中出现一个黄色感叹号错误图标。

为防止出现这种情况，可为具有根枚举设备的每个驱动程序使用唯一命名空间。 对于 USB 或系统设备，请使用 `ROOT\[COMPANYNAME]\[DEVICENAME]`，而不是使用 `ROOT\USB` 或 `ROOT\SYSTEM”`。  然后，在安装之前检查 devnode 是否已存在。

已建立自己的命名约定的现有设备类可能会使用自定义格式。 有关其硬件 ID 格式的信息，请参阅此类总线的硬件规范。

硬件 ID 的字符数（不包括 NULL 终止符）必须小于 `MAX_DEVICE_ID_LEN`。 此约束适用于硬件 ID 中所有字段与任何 `\\` 字段分隔符的长度总和。 有关详细信息，请参阅 [IRP_MN_QUERY_ID](../kernel/irp-mn-query-id.md) 的“操作”部分。

## <a name="obtaining-the-list-of-hardware-ids-for-a-device"></a>获取设备的硬件 ID 列表

若要获取设备的硬件 ID 列表，请在将 *DeviceProperty* 参数设置为 **DevicePropertyHardwareID** 的情况下调用 [**IoGetDeviceProperty**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty)。 此例程检索到的硬件 ID 列表是一个 [REG_MULTI_SZ](/windows/desktop/SysInfo/registry-value-types) 值。

硬件列表中的字符的最大数目（包括每个硬件 ID 后的 NULL 终止符和最终 NULL 终止符）为 `REGSTR_VAL_MAX_HCID_LEN`。 硬件 ID 列表中最多可以包含的 ID 数为 64 个。

## <a name="examples-of-hardware-ids"></a>硬件 ID 示例

下面是 PnP 设备[通用标识符](generic-identifiers.md)的示例：

`root\*PNP0F08`

下面是 [PCI 设备标识符](identifiers-for-pci-devices.md)的示例：

`PCI\VEN_1000&DEV_0001&SUBSYS_00000000&REV_02`


## <a name="see-also"></a>另请参阅

[INF HardwareId 指令](./inf-hardwareid-directive.md)
