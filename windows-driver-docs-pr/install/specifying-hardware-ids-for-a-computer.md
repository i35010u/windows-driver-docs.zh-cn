---
title: 指定计算机的硬件 Id
description: 指定计算机的硬件 Id
ms.assetid: af0dbfc4-747c-4e16-a3ed-678df0e07757
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d72d987afa5f0358d16a766f13ffe77ab2791149
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554303"
---
#  <a name="specifying-hardware-ids-for-a-computer"></a>指定计算机的硬件 Id

设备和打印机会将计算机作为识别[设备容器](container-ids.md)。 因此，计算机可以被标识设备元数据包中使用[ **HardwareID** ](https://msdn.microsoft.com/library/windows/hardware/ff546114)指定一个唯一的 XML 元素[硬件 ID](hardware-ids.md)值。  此硬件 ID 值的 （有时称为计算机硬件 ID 或 CHID） 的计算机可以指定系统管理 BIOS (SMBIOS) 字段中数据的组合。

与不同[硬件 Id](hardware-ids.md)对于其他设备的容器，在计算机的硬件 ID 生成通过 Windows 每次系统启动时。 可以通过运行 ComputerHardwareIds 工具 (ComputerHardwareIDs.exe)，它所包含的 Windows 7、 Windows 8 和 Windows 8.1 的 Windows Driver Kit (WDK) 中生成的计算机的硬件 Id。 从 Windows 10 开始，ComputerHardwareIds 工具包含在软件开发工具包 (SDK)。

ComputerHardwareIds 工具生成一组基于系统的系统管理 BIOS (SMBIOS) 中的字段中的信息的计算机的硬件 Id。 下表描述了这些 SMBIOS 字段。

|字段名称|结构名称和类型|SMBIOS 规范版本|偏移量|长度|值|描述|
|--- |--- |--- |--- |--- |--- |--- |
|制造商|系统信息(类型 1)|2.0+|04h|BYTE|STRING|dmiStrucBuffer 数组中以 Null 结尾的字符串的索引。 此字符串指定计算机制造商的名称。|
|系列|系统信息(类型 1)|2.4+|1Ah|BYTE|STRING|dmiStrucBuffer 数组中以 Null 结尾的字符串的索引。 此字符串指定特定的计算机所属的系列。  一系列是指一组类似但不从硬件或软件的角度来看完全相同的计算机。  通常一系列组成不同的计算机模型，有不同的配置和定价的点。 同一系列中的计算机通常具有相似的品牌和外观特点。|
|产品名称|系统信息(类型 1)|2.0+|05h|BYTE|STRING|dmiStrucBuffer 数组中以 Null 结尾的字符串的索引。 此字符串指定计算机的产品名称。|
|供应商|BIOS 信息(类型 0)|2.0+|04h|BYTE|STRING|dmiStrucBuffer 数组中以 Null 结尾的字符串的索引。 此字符串指定 BIOS 供应商的名称。|
|BIOS 版本|BIOS 信息(类型 0)|2.+0|05h|BYTE|STRING|dmiStrucBuffer 数组中以 Null 结尾的字符串的索引。 此字符串包含有关处理器核心和 OEM 版本的信息。|
|系统 BIOS 主要版本|BIOS 信息(类型 0)|2.4+|14h|BYTE|视情况而定。|系统 BIOS 的主要版本。|
|系统 BIOS 次要版本|BIOS 信息(类型 0)|2.4+|15h|BYTE|变化不定|系统 BIOS 的次要版本。|
|机箱类型|系统机箱(类型 3)|2.0+|05h|BYTE|变化不定|系统机箱或机壳类型。|
|SKU 号|SKU 号 （类型 1）|2.4+|19h|BYTE|STRING|销售的特定计算机配置的标识。|
|主板制造商|制造商 （类型 2）| |04h|BYTE|STRING|以 null 结尾的字符串数。 此字符串标识的制造商的基板，其中基板 – 板类型是 0Ah （主板）。|
|基板产品|产品 （类型 2）| |05h|BYTE|STRING|以 null 结尾的字符串数。 此字符串标识的基板，其中基板 – 板类型是 0Ah 的产品名称 （主板）。|

有关详细信息*dmiStrucBuffer*数组和 SMBIOS 字段，请参阅[系统管理 BIOS (SMBIOS)](https://go.microsoft.com/fwlink/p/?linkid=145867)分布式管理任务组 (DMTF) 网站上的规范。

ComputerHardwareIds 工具运行时，它从 SMBIOS 信息创建唯一硬件 Id。 ID 是每个硬件*GUID*和通过连接中的 SMBIOS 字段的值来创建。

下表显示了使用为 Windows 7、 Windows 8、 Windows 8.1 和 Windows 10 中的每个硬件 ID 的 SMBIOS 字段。

**重要**  中系统的 SMBIOS 数据填充每个单独的 SMBIOS 字段用于生成 HardwareID 才会生成每个计算机硬件 Id。

 

| HWID         | Windows 7                                                                                                            |
|--------------|----------------------------------------------------------------------------------------------------------------------|
| HardwareID-0 | 制造商 + 系列 + 产品名称 + 供应商 + BIOS 版本 + 系统 BIOS 主要发布 + 系统 BIOS 次要版本 |
| HardwareID-1 | 制造商 + 产品名称 + BIOS 供应商 + BIOS 版本 + 系统 BIOS 主要发布 + 系统 BIOS 次要版本     |
| HardwareID-2 | 制造商 + 系列 + 产品名称                                                                                  |
| HardwareID-3 | 制造商 + 产品名称                                                                                           |
| HardwareID-4 | 制造商 + 系列                                                                                                |
| HardwareID-5 | 制造商 + 机箱类型                                                                                        |
| HardwareID-6 | 制造商                                                                                                         |

 

| HWID         | Windows 8，Windows 8.1                                                                                                   |
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
| HardwareID-3  | 制造商 + 系列 + 产品名称 + SKU 数 + 基板制造商 + 基板产品                           |
| HardwareID-4  | 制造商 + 系列 + 产品名称 + SKU 编号                                                                        |
| HardwareID-5  | 制造商 + 系列 + 产品名称                                                                                     |
| HardwareID-6  | 制造商 + SKU 数 + 基板制造商 + 基板产品                                                   |
| HardwareID-7  | 制造商 + SKU 号                                                                                                |
| HardwareID-8  | 制造商 + 产品名称 + 基板制造商 + 基板产品                                                 |
| HardwareID-9  | 制造商 + 产品名称                                                                                              |
| HardwareID-10 | 制造商 + 系列 + 基板制造商 + 基板产品                                                       |
| HardwareID-11 | 制造商 + 系列                                                                                                    |
| HardwareID-12 | 制造商 + 机箱类型                                                                                            |
| HardwareID-13 | 制造商 + 基板制造商 + 基板产品                                                                |
| HardwareID-14 | 制造商                                                                                                             |

 

通过使用 sha-1 哈希算法情况下，每个硬件 ID 字符串转换为 GUID。

### <a name="using-computer-hardwareids-with-pc-device-metadata-packages"></a>计算机 HardwareIDs 使用 PC 设备元数据包

对于 Windows 7 系统，我们强烈建议选择时，供应商，执行以下[硬件 ID](hardware-ids.md)要用作值[ **HardwareID** ](https://msdn.microsoft.com/library/windows/hardware/ff546114) XML 元素值计算机。

-   使用**HardwareID 3**或**HardwareID 4**为设备元数据包匹配具有特定品牌、 系列和型号的计算机中的第一个选项。 这允许元数据包，以匹配指定的计算机的计算机提供最精确的元数据。

-   使用**HardwareID 5**，为如果设备元数据包包含整个系列的计算机中的第二个选项。 在这种情况下，计算机系列是唯一的并且不与多个产品系列品牌。

-   使用**HardwareID 6**或**HardwareID 7**为如果盖住了设备元数据包的所有计算机或特定的机箱类型与这些计算机中的第三个选项。

**请注意**  对于 Windows 7 PC 设备元数据，不要使用**HardwareID 1**或**HardwareID 2**的计算机的硬件 id。 **硬件 ID 1**或**HardwareID 2**是保留供将来使用。

 

**请注意**  对于 Windows 8 PC 设备元数据，我们强烈建议不使用供应商**HardwareID 1**， **HardwareID 2**， **HardwareID 3**的计算机的硬件 id。 **HardwareID 1**， **HardwareID 2**， **HardwareID 3**是保留供将来使用。 相反，可以使用供应商**硬件 Id 4**， **HardwareID 5**， **HardwareID 6**， **HardwareID 7**， **HardwareID 8**， **HardwareID 9**，和**HardwareID 10**。

 

若要指定硬件 ID 是计算机设备容器，请使用以下规则：

-   分隔的硬件 ID 字符串 {和} 个字符。

-   添加前缀 ComputerMetadata\\硬件 ID 字符串的前面。

以下是一种[ **HardwareID** ](https://msdn.microsoft.com/library/windows/hardware/ff546114)的计算机的 XML 元素：

```cpp
DOID:ComputerMetadata\{c20d5449-511e-4cb5-902a-a541239322aa}
```

有关格式的要求的详细信息**HardwareID** XML 元素，请参阅[ **HardwareID**](https://msdn.microsoft.com/library/windows/hardware/ff546114)。

## <a name="related-topics"></a>相关主题


[发布工作流的 Windows 10 驱动程序](https://go.microsoft.com/fwlink/p/?LinkId=617374 )

 

 






