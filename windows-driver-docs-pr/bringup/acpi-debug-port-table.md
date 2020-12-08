---
title: 调试端口表 2 (DBG2)
description: 调试端口 ACPI 表用于平台固件，用于描述系统上可用的调试端口。
keywords:
- DBG2
- DBGP
- KDCOM
- 串行
- UART
ms.date: 09/01/2020
ms.openlocfilehash: a09481cf1a60dc6f1ec9ebc9b4a5a3ea4ba7c8bf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789153"
---
# <a name="microsoft-debug-port-table-2-dbg2"></a>Microsoft 调试端口表 2 (DBG2) 

此规范定义调试端口表 2 (DBG2) 的格式，用于描述系统上可用的调试端口。
此信息适用于以下操作系统： Windows 8 和更高版本。

本文末尾列出了此处讨论的参考和资源。

>专利通知： Microsoft 根据以下两个选项，为此规范的实现提供某些专利权限：
>
>1. Microsoft 的社区承诺，提供于 <https://www.microsoft.com/openspecifications/en/us/programs/community-promise/default.aspx> ; 或
>2. 从1.0 年10月 1 2012 日起，开源最终规范协议版本 ( "OWF 1.0" ) [http://www.openwebfoundation.org/legal/the-owf-1-0-agreements/owfa-1-0/](http://www.openwebfoundation.org/legal/the-owf-1-0-agreements/owfa-1-0) 。

## <a name="document-history"></a>文档历史记录

| **日期** | **更改** |
|----------|------------|
| 2011年11月29日 | 第一次发布。 |
| 5月22日2012 | Windows 8 的每个最终受支持平台的表3更新。 |
| 2015 年 8 月 10 日 | 已更新的专利通知。 |
| 2015 年 10 月 6 日 | 添加了新的串行调试子类型 (ARM SBSA UART，ARM DCC)  |
| 2015 年 12 月 10 日 | 添加了新的串行调试子类型 (BCM2835)  |
| 5月31日，2017 | 添加了新的串行调试子类型， (MX6、通用地址结构16550兼容)  |
| 2020 年 6 月 11 日 | 添加了新的串行调试子类型 (SDM845v2)  |
| 2020 年 9 月 1 日 | 已将文档转换为 Markdown 语法和格式更改。 |
| 2020 年 9 月 21 日 | 添加了新的串行调试子类型 (IALPSS)  |

## <a name="introduction"></a>简介

Microsoft 需要在所有系统上都有调试端口。 为了描述 (s) 上可用的调试端口，Microsoft 定义了特定于操作系统的表 (DBG2) 。 此表指定一个或多个独立端口用于调试目的。 调试端口表的存在指示系统包含调试端口。 该表包含有关调试端口配置的信息。 该表位于具有其他高级配置和电源接口 (ACPI) 表的系统内存中，并且必须在 ACPI 根系统说明表 (RSDT) 中进行引用。

DBG2 表会将 ACPI 调试端口表替换为不能使用 DBGP 描述调试端口实现的平台上的 (DBGP) 。

## <a name="debug-port-table-2-dbg2"></a>调试端口表 2 (DBG2)

表1定义 DBG2 中的字段。

**表1。调试端口表2格式**

| 字段 | **字节长度** | **字节偏移量** | **说明** |
|-----------|-----------------|-----------------|-----------------|
| 标头    |                 |                 |                 |
| 签名 | 4 | 0 | 'DBG2'. 调试端口表2的签名。 |
| 长度 | 4 | 4 | 整个调试端口表2的长度（以字节为单位）。 |
| 修订 | 1 | 8 | 对于此版本的规范，此值为0。 |
| 校验和 | 1 | 9 | 整个表格的总和必须为零。 |
| OEM ID | 6 | 10 | 原始设备制造商 (OEM) ID。 |
| OEM 表格 ID | 8 | 16 | 对于调试端口表2，表 ID 是制造商型号 ID。 |
| OEM 修订 | 4 | 24 | 提供的 OEM 表 ID 的调试端口表2的 OEM 修订版本。 |
| 创建者 ID | 4 | 28 | 创建该表的实用工具的供应商 ID。 |
| 创建者修订 | 4 | 32 | 创建该表的实用工具的修订。 |
| OffsetDbgDeviceInfo | 4 | 36 | 从此表开始到第一个调试设备信息结构条目的偏移量（以字节为单位）。 |
| NumberDbgDeviceInfo | 4 | 40 | 指示调试设备信息结构条目的数目。 |
| 调试设备信息结构 [NumberDbgDeviceInfo] | 变量 | OffsetDbgDeviceInfo  | 此平台的调试设备信息结构的列表。  结构格式是在本文档后面的 "调试设备信息结构" 部分中定义的。 |

<br>

## <a name="debug-device-information-structure"></a>调试设备信息结构

**表2：调试设备信息结构格式**

| 字段 | **字节长度** | **字节偏移量** | **说明** |
|-----------|-----------------|-----------------|-----------------|
| 修订 | 1 | 0 | 调试设备信息结构的修订版本。 对于此版本的规范，此版本必须为0。 |
| Length | 2 | 1 | 此结构的长度（以字节为单位），包括 NamespaceString 和 OEMData。 |
| NumberofGenericAddressRegisters | 1 | 3 | 使用中的通用地址寄存器的数目。 |
| NameSpaceStringLength | 2 | 4 | NamespaceString 的长度（以字节为单位），包括 null 字符。 |
| NameSpaceStringOffset | 2 | 6 | 从该结构开始到字段 NamespaceString [] 的偏移量（以字节为单位）。 此值必须是有效的，因为此字符串必须存在。 |
| OemDataLength | 2 | 8 | OEM 数据块的长度（以字节为单位）。 |
| OemDataOffset | 2 | 10 | 从该结构的开头开始，偏移量（以字节为单位）到字段 OemData []。 如果不存在 OEM 数据，则此值为0。 |
| 端口类型 | 2 | 12 | 调试设备的调试端口类型。 其中每个值都将具有一个对应的子类型值，如表3中所示。 |
| 端口子类型 | 2 | 14 | 调试此调试设备的端口子类型。  请参阅表3。 |
| 预留 | 2 | 16 | 保留，必须为0。 |
| BaseAddressRegisterOffset | 2 | 18 | 从此结构开始到字段 BaseaddressRegister [] 的偏移量（以字节为单位）。 |
| AddressSizeOffset | 2 | 20 | 从此结构开始到字段 AddressSize [] 的偏移量（以字节为单位）。 |
| BaseAddressRegister[] |  (NumberofGenericAddressRegisters) * 12 | BaseAddressRegisterOffset | 泛型地址的数组。 |
| AddressSize[] |  (NumberofGenericAddressRegisters) * 4 | AddressSizeOffset | 与上述每个泛型地址相对应的地址大小的数组。 |
| NamespaceString[] | NameSpaceStringLength | NameSpaceStringOffset | 以 Null 结尾的 ASCII 字符串，用于唯一标识此设备。 此字符串包含对在 ACPI 命名空间中表示此设备的对象的完全限定引用。 如果不存在命名空间设备，则 NamespaceString [] 必须包含句点 "."。 |
| OemData[] | OemDataLength | OemDataOffset | 可选的、可变长度的 OEM 特定数据。 |

<br>

**表3：调试端口类型和子类型**

| **端口** | **类型** | **类型** | **说明** |
|----------|----------|-------------|-----------------|
| 预留 | 0x0000 –0x7FFF 和0xFFFF | 全部 | 保留 (不使用)  |
| 串行   | 0x8000   | 0x0000      | 完全16550兼容 |
|          |          | 0x0001      | 16550子集与 DBGP 修订版本1兼容 |
|          |          | 0x0002      | 保留 (不使用)  |
|          |          | 0x0003      | ARM PL011 UART |
|          |          | 0x0004 – 0x000C | 保留 (不使用)  |
|          |          | 0x000D      |  (不推荐使用) ARM SBSA (2.x 仅) 仅支持32位访问的通用 UART |
|          |          | 0x000E      | ARM SBSA 通用 UART |
|          |          | 0x000F      | ARM DCC |
|          |          | 0x0010      | BCM2835 |
|          |          | 0x0011      | SDM845 的时钟速率为 1.8432 MHz |
|          |          | 0x0012      | 16550-与泛型地址结构中定义的参数兼容 |
|          |          | 0x0013      | SDM845 的时钟速率为 7.372 MHz |
|          |          | 0x0014      | Intel LPSS |
|          |          | 0x0015-0xFFFF | 保留 (供将来使用)  |
| 1394     | 0x8001   | 0x0000      | IEEE1394 标准主机控制器接口 |
|          |          | 0x0001-0xFFFF | 保留 (供将来使用)  |
| USB      | 0x8002   | 0x0000      | 带有调试接口的 XHCI 兼容控制器 |
|          |          | 0x0001      | 带有调试接口的 EHCI 兼容控制器 |
|          |          | 0x0002 –0x0006 | 保留 (不使用)  |
|          |          | 0x0007-0xFFFF | 保留 (供将来使用)  |
| Net      | 0x8003   | NNNN        | NNNN 必须是有效的 PCI 分配供应商 ID |
|          | 0x8004   | 全部         | 保留 (不使用)  |
| 预留 | 0x8005 –0xFFFE | 全部  | 保留 (供将来使用)  |

<br>

### <a name="note-on-the-fields-of-the-generic-address-structure"></a>一般地址结构字段的说明

* BaseAddressRegister [0] 中的通用地址结构用于指定某些串行子类型使用的寄存器位宽度和访问大小。
* 地址空间 ID 和寄存器位偏移量字段必须为0。
* "寄存器位宽度" 字段包含寄存器步幅，必须是2的幂，且至少为访问大小。 在32位平台上，此值不能超过32。 在64位平台上，此值不能超过64。
* "访问大小" 字段用于确定是否要使用 byte、WORD、DWORD 或 QWORD 访问。 QWORD 访问仅适用于64位体系结构。

## <a name="resources"></a>资源

* ACPI 规范
  * http://uefi.org/specifications
