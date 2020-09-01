---
title: 指定计算机的硬件 ID
description: 指定计算机的硬件 ID
ms.assetid: af0dbfc4-747c-4e16-a3ed-678df0e07757
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e56dd17b061fedc6ad779079c54095fb2cefc53a
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89096241"
---
#  <a name="specifying-hardware-ids-for-a-computer"></a>指定计算机的硬件 ID

设备和打印机将计算机识别为 [设备容器](container-ids.md)。 因此，可以通过使用指定唯一[硬件 ID](hardware-ids.md)值的[**HardwareID**](/previous-versions/windows/hardware/metadata/ff546114(v=vs.85)) XML 元素在设备元数据包内标识计算机。  计算机的此硬件 ID 值 (有时称为计算机硬件 ID，或子) 可以指定系统管理 BIOS (SMBIOS) 字段数据的组合。

与其他设备容器的 [硬件](hardware-ids.md) id 不同，每次系统启动时，计算机的硬件 id 都是由 Windows 生成的。 可以通过运行 ComputerHardwareIds 工具 ( # A0) 生成计算机的硬件 Id，该工具包含在 windows 驱动程序工具包)  (适用于 Windows 7、Windows 8 和 Windows 8.1 的 windows 驱动程序工具包中。 从 Windows 10 开始，ComputerHardwareIds 工具包含在软件开发工具包 (SDK) 中。

ComputerHardwareIds 工具将基于系统的系统管理 BIOS (SMBIOS) 中的字段中的信息生成一组硬件 Id。 下表介绍了这些 SMBIOS 字段。

|字段名称|结构名称和类型|SMBIOS 规范版本|偏移量|长度|值|说明|
|--- |--- |--- |--- |--- |--- |--- |
|制造商|系统信息(类型 1)|2.0+|04h|BYTE|STRING|dmiStrucBuffer 数组中以 Null 结尾的字符串的索引。 此字符串指定计算机制造商的名称。|
|家庭|系统信息(类型 1)|2.4+|1Ah|BYTE|STRING|dmiStrucBuffer 数组中以 Null 结尾的字符串的索引。 此字符串指定特定计算机所属的系列。  系列是指一组类似但不同于硬件或软件观点的计算机。  通常，系列由不同的计算机型号组成，它们具有不同的配置和价格点。 同一系列中的计算机通常具有相似的品牌和外观特点。|
|产品名称|系统信息(类型 1)|2.0+|05h|BYTE|STRING|dmiStrucBuffer 数组中以 Null 结尾的字符串的索引。 此字符串指定计算机的产品名称。|
|供应商|BIOS 信息(类型 0)|2.0+|04h|BYTE|STRING|dmiStrucBuffer 数组中以 Null 结尾的字符串的索引。 此字符串指定 BIOS 供应商的名称。|
|BIOS 版本|BIOS 信息(类型 0)|2. + 0|05h|BYTE|STRING|dmiStrucBuffer 数组中以 Null 结尾的字符串的索引。 此字符串包含有关处理器核心和 OEM 版本的信息。|
|系统 BIOS 主要版本|BIOS 信息(类型 0)|2.4+|14h|BYTE|视情况而定。|系统 BIOS 的主要版本。|
|系统 BIOS 次要版本|BIOS 信息(类型 0)|2.4+|15h|BYTE|多种多样|系统 BIOS 的次要版本。|
|机箱类型|系统机箱(类型 3)|2.0+|05h|BYTE|多种多样|系统机箱或机壳类型。|
|SKU 号|SKU 编号 (类型 1) |2.4+|19h|BYTE|STRING|用于销售的特定计算机配置的标识。|
|基板制造商|制造商 (类型 2) | |04h|BYTE|STRING|以 null 结尾的字符串的数目。 此字符串标识基板的制造商，其中基板–板类型为 0Ah (主板) 。|
|基板产品|Product (类型 2) | |05h|BYTE|STRING|以 null 结尾的字符串的数目。 此字符串标识基板的产品名称，其中基板–板类型为 0Ah (主板) 。|

有关 *dmiStrucBuffer* 数组和 SMBIOS 字段的详细信息，请参阅分布式管理任务组 (DMTF) 网站上的 " [系统管理" BIOS (SMBIOS) ](https://go.microsoft.com/fwlink/p/?linkid=145867) 规范。

当 ComputerHardwareIds 工具运行时，它会根据 SMBIOS 信息创建唯一的硬件 Id。 每个硬件 ID 都是一个 *GUID* ，并通过将这些值与 SMBIOS 字段连接来创建。

下表显示了用于在 Windows 7、Windows 8、Windows 8.1 和 Windows 10 中形成每个硬件 ID 的 SMBIOS 字段。

**重要提示**   仅当用于生成 HardwareID 的每个单独 SMBIOS 字段都填充在系统的 SMBIOS 数据中时，才会生成每个计算机 HardwareID。

 

| HWID         | Windows 7                                                                                                            |
|--------------|----------------------------------------------------------------------------------------------------------------------|
| HardwareID-0 | 制造商 + 家族 + 产品名称 + 供应商 + BIOS 版本 + 系统 BIOS 主要版本 + 系统 BIOS 次要版本 |
| HardwareID-1 | 制造商 + 产品名称 + BIOS 供应商 + BIOS 版本 + 系统 BIOS 主要版本 + 系统 BIOS 次要版本     |
| HardwareID-2 | 制造商 + 系列 + 产品名称                                                                                  |
| HardwareID-3 | 制造商 + 产品名称                                                                                           |
| HardwareID-4 | 制造商 + 系列                                                                                                |
| HardwareID-5 | 制造商 + 机箱类型                                                                                        |
| HardwareID-6 | 制造商                                                                                                         |

 

| HWID         | Windows 8、Windows 8.1                                                                                                   |
|--------------|--------------------------------------------------------------------------------------------------------------------------|
| HardwareID-0 | 制造商 + 系列 + 产品名称 + SKU 号 + BIOS 供应商 + BIOS 版本 + BIOS 主要版本 + BIOS 次要版本 |
| HardwareID-1 | 制造商 + 系列 + 产品名称 + BIOS 供应商 + BIOS 版本 + BIOS 主要版本 + BIOS 次要版本              |
| HardwareID-2 | 制造商 + 产品名称 + BIOS 供应商 + BIOS 版本 + BIOS 主要版本 + BIOS 次要版本                       |
| HardwareID-3 | 制造商 + 系列 + 产品名称 + SKU 号                                                                         |
| HardwareID-4 | 制造商 + 系列 + 产品名称                                                                                      |
| HardwareID-5 | 制造商 + SKU 号                                                                                                |
| HardwareID-6 | 制造商 + 产品名称                                                                                               |
| HardwareID-7 | 制造商 + 系列                                                                                                    |
| HardwareID-8 | 制造商 + 机箱类型                                                                                            |
| HardwareID-9 | 制造商                                                                                                             |

 

| HWID          | Windows 10                                                                                                               |
|---------------|--------------------------------------------------------------------------------------------------------------------------|
| HardwareID-0  | 制造商 + 系列 + 产品名称 + SKU 号 + BIOS 供应商 + BIOS 版本 + BIOS 主要版本 + BIOS 次要版本 |
| HardwareID-1  | 制造商 + 系列 + 产品名称 + BIOS 供应商 + BIOS 版本 + BIOS 主要版本 + BIOS 次要版本              |
| HardwareID-2  | 制造商 + 产品名称 + BIOS 供应商 + BIOS 版本 + BIOS 主要版本 + BIOS 次要版本                       |
| HardwareID-3  | 制造商 + 家族 + 产品名称 + SKU 编号 + 基板制造商 + 基板产品                           |
| HardwareID-4  | 制造商 + 家族 + 产品名称 + SKU 编号                                                                        |
| HardwareID-5  | 制造商 + 家族 + 产品名称                                                                                     |
| HardwareID-6  | 制造商 + SKU 编号 + 基板制造商 + 基板产品                                                   |
| HardwareID-7  | 制造商 + SKU 号                                                                                                |
| HardwareID-8  | 制造商 + 产品名称 + 基板制造商 + 基板产品                                                 |
| HardwareID-9  | 制造商 + 产品名称                                                                                              |
| HardwareID-10 | 制造商 + 家族 + 基板制造商 + 基板产品                                                       |
| HardwareID-11 | 制造商 + 系列                                                                                                    |
| HardwareID-12 | 制造商 + 机箱类型                                                                                            |
| HardwareID-13 | 制造商 + 基板制造商 + 基板产品                                                                |
| HardwareID-14 | 制造商                                                                                                             |

 

每个硬件 ID 字符串使用 SHA-1 哈希算法转换为 GUID。

### <a name="using-computer-hardwareids-with-pc-device-metadata-packages"></a>将计算机 HardwareIDs 与电脑设备元数据包一起使用

对于 Windows 7 系统，我们强烈建议供应商在选择要用作计算机的[**HardwareID**](/previous-versions/windows/hardware/metadata/ff546114(v=vs.85)) XML 元素值的[硬件 ID](hardware-ids.md)值时执行以下操作。

-   如果设备元数据包与具有特定品牌、系列和型号的计算机匹配，请使用 **HardwareID-3** 或 **HardwareID-4** 作为第一个选项。 这允许元数据包与指定的计算机匹配，后者为计算机提供最精确的元数据。

-   如果设备元数据包涵盖整个计算机系列，请使用 **HardwareID-5**作为第二个选择。 在这种情况下，计算机系列是唯一的，且不带多个产品系列的品牌。

-   如果设备元数据包涵盖了所有计算机或具有特定机箱类型的计算机，请使用 **HardwareID-6** 或 **HardwareID** 作为第三个选项。

**注意**   对于 Windows 7 电脑设备元数据，请不要将**HardwareID-1**或**HardwareID-2**用于计算机的硬件 ID。 **硬件 ID-1** 或 **HardwareID-2** 保留供将来使用。

 

**注意**   对于 Windows 8 PC 设备元数据，我们强烈建议供应商不要将**HardwareID-1**、 **HardwareID-2**和**HARDWAREID**用于计算机的硬件 ID。 **HardwareID-1**、 **HardwareID-2**、 **HardwareID** 将保留以供将来使用。 相反，供应商可**使用 HardwareID**、 **HardwareID**、 **HardwareID**、 **HardwareID**、 **HardwareID、HardwareID**、HardwareID、 **、** 和**HardwareID-10**。

 

若要指定硬件 ID 适用于计算机设备容器，请使用以下规则：

-   用 "{" 和 "}" 个字符分隔硬件 ID 字符串。

-   \\在硬件 ID 字符串前面添加前缀 "ComputerMetadata"。

下面是计算机的 [**HardwareID**](/previous-versions/windows/hardware/metadata/ff546114(v=vs.85)) XML 元素的示例：

```cpp
DOID:ComputerMetadata\{c20d5449-511e-4cb5-902a-a541239322aa}
```

有关 **HardwareID** XML 元素的格式要求的详细信息，请参阅 [**HardwareID**](/previous-versions/windows/hardware/metadata/ff546114(v=vs.85))。

## <a name="related-topics"></a>相关主题


[Windows 10 驱动程序发布工作流](https://go.microsoft.com/fwlink/p/?LinkId=617374 )

 

