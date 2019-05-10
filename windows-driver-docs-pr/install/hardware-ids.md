---
title: 硬件 ID
description: 硬件 ID 是 Windows 用来与设备 INF 文件匹配供应商定义的标识字符串。
ms.assetid: 9eb894d6-4e83-4c08-8165-f30d6636da75
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5312df32adcc5a63e470491253cb1f5ec0c66c3
ms.sourcegitcommit: 944535d8e00393531f6b265317a64da3567e4f2c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2019
ms.locfileid: "65106417"
---
# <a name="hardware-id"></a>硬件 ID


硬件 ID 是 Windows 用来与设备 INF 文件匹配供应商定义的标识字符串。 在大多数情况下，设备具有与之关联的硬件 ID 列表。 （但是，有异常 − 看到标识符 1394年设备报告的设备，应降低适用性的顺序列出 Id 的硬件的硬件 Id 的列表。




硬件 ID 具有以下通用格式之一：

`<enumerator>\\<enumerator-specific-device-ID>`

这是最常用的格式为插 (PnP) 管理器报告的单个枚举器的各个即插即用设备。 新枚举器应使用此格式或以下的格式。 有关特定于枚举器的设备 Id 的详细信息，请参阅[设备标识符格式](device-identifier-formats.md)。

`\*<generic-device-ID>`

星号指示该设备支持多个枚举器，如 ISAPNP 和 BIOS。 有关此类型的 ID 的详细信息，请参阅[通用标识符](generic-identifiers.md)。

`<device-class-specific-ID>`

## <a name="selecting-a-hardware-id"></a>选择硬件 ID

根枚举设备共享通用的命名空间，如`ROOT\SYSTEM`可能会导致冲突，在 OS 升级时的设备管理器中的黄色感叹号。

若要防止此情况，每个包含根枚举的设备的驱动程序使用唯一的命名空间。 对于 USB 或系统设备，而不是使用`ROOT\USB`或`ROOT\SYSTEM”`使用`ROOT\[COMPANYNAME]\[DEVICENAME]`。  此外，驱动程序安装程序代码应检查以查看是否已存在 devnode 并采取任何必要的纠正措施，然后再安装。

已建立自己的命名约定的现有设备类可能使用自定义格式。 有关其硬件 ID 格式的信息，请参阅此类总线的硬件规格。 新枚举器不应使用此格式。

硬件 ID，不包括 NULL 终止符的字符数必须小于 MAX_DEVICE_ID_LEN。 此约束应用于所有字段和任意长度的总和"\\"字段中的硬件 id。 有关设备 Id 上的约束的详细信息，请参阅的操作部分[ **IRP_MN_QUERY_ID**](https://msdn.microsoft.com/library/windows/hardware/ff551679)。

## <a name="obtaining-the-list-of-hardware-ids-for-a-device"></a>获取设备的硬件 Id 的列表

若要获取的设备硬件 Id 列表，请调用[ **IoGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff549203)与*DeviceProperty*参数设置为**DevicePropertyHardwareID**. 硬件 Id，此例程检索列表是[REG_MULTI_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)值。 中的硬件列表，每个硬件 ID 和最后一个 NULL 终止符之后, 包括 NULL 终止符的字符的最大数是 REGSTR_VAL_MAX_HCID_LEN。 Id 可能的硬件 Id 列表中的最大数目为 64。

## <a name="examples-of-hardware-ids"></a>硬件 Id 的示例

在下面的示例，例如，如果[通用标识符](generic-identifiers.md)即插即用设备和第二个示例是[PCI 设备标识符](identifiers-for-pci-devices.md):

root\\\*PNP0F08

PCI\\VEN_1000&DEV_0001&SUBSYS_00000000&REV_02





## <a name="see-also"></a>请参阅

[INF HardwareId 指令](https://docs.microsoft.com/windows-hardware/drivers/install/inf-hardwareid-directive)


