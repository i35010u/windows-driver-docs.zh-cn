---
title: 可按 JEDEC 字节寻址且以能源为支持的功能类的 _DSM 接口（功能接口 1）
description: ) 接口 (_DSM 的 Device-Specific 方法旨在映射到 JEDEC Byte 可寻址的支持电源的接口标准，以最大程度地减少 BIOS 复杂性。
ms.localizationpriority: medium
ms.date: 12/15/2019
ms.openlocfilehash: 4ffeb153acd3ad9a278dce60da2c0b945311faf3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804819"
---
# <a name="_dsm-interface-for-jedec-byte-addressable-energy-backed-function-class-function-interface-1"></a>可按 JEDEC 字节寻址且以能源为支持的功能类的 _DSM 接口（功能接口 1）

) 接口 (_DSM 的 Device-Specific 方法旨在映射到 JEDEC Byte 可寻址的支持电源的接口标准，以最大程度地减少 BIOS 复杂性。 它提供了报表设备功能 & 功能的常见基础，使 OS 软件可以通过相同的机制与各种实现交互。 此外，它还允许通过访问 I2C 寄存器来支持供应商特定的功能。

_DSM 符合 (函数接口 1) 的用于支持字节寻址的支持字节的功能的函数类的平台，可支持实现 *JEDEC 字节*)  (可寻址的、支持 有关详细信息，请参阅 [JEDEC Byte 可寻址能量支持的接口规范 (文档 JESD245) ](https://www.jedec.org/document_search?search_api_views_fulltext=jesd245)。

## <a name="_dsm-interface-for-byte-addressable-energy-backed-function-class-function-interface-1"></a>用于支持字节寻址的支持功能的函数类的 _DSM 接口，函数接口1

_DSM GUID 为1EE68B36-D4BD-4a1a-9A16-4F8E53D46E05。

本部分中定义的 _DSM 函数应在 NVDIMM ACPI 命名空间设备对象中实现。 " **强制** " 一词是指函数是否必须返回有效的数据。

### <a name="mandatory-functions-and-fields"></a>必需的函数和字段

下表指定了必需的函数 & 字段。

| 函数索引 | 函数名称                                                                                                                                | Device-Managed 能量源 (ES) 策略的必需 | Host-Managed 能量源 (ES) 策略的必需 |
|----------------|----------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------|------------------------------------------------------|
| 0              | [查询实现的功能（功能索引 0）](query-implemented-functions--function-index-0-.md)                                         | 是                                                    | 是                                                  |
| 1              | [获取 NVDIMM-N 标识（功能索引 1）](get-nvdimm-n-identification--function-index-1-.md)                                         | 是                                                    | 是                                                  |
| 2              | [获取保存操作要求（功能索引 2）](get-save-operation-requirements--function-index-2-.md)                                 | 是                                                    | 是                                                  |
| 3              | [获取能量源标识（功能索引 3）](get-energy-source-identification--function-index-3-.md)                               | 是                                                    | 是                                                  |
| 4              | [获取上次备份信息（功能索引 4）](get-last-backup-information--function-index-4-.md)                                         | 是                                                    | 是                                                  |
| 5              | [获取 NVM 阈值（功能索引 5）](get-nvm-thresholds--function-index-5-.md)                                                           | 是                                                    | 是                                                  |
| 6              | [设置 NVM 生存期百分比警告阈值（功能索引 6）](set-nvm-lifetime-percentage-warning-threshold--function-index-6-.md)     | 是                                                    | 是                                                  |
| 7              | [获取能量源阈值（功能索引 7）](get-energy-source-thresholds--function-index-7-.md)                                       | 是                                                    | 否                                                   |
| 8              | [设置能量源生存期警告阈值（功能索引 8）](set-energy-source-lifetime-warning-threshold--function-index-8-.md)       | 是                                                    | 否                                                   |
| 9              | [设置能量源温度警告阈值（功能索引 9）](set-energy-source-temperature-warning-threshold--function-index-9-.md) | 是                                                    | 否                                                   |
| 10             | [获取关键的运行状况信息（功能索引 10）](get-critical-health-info--function-index-10-.md)                                             | 是                                                    | 是                                                  |
| 11             | [获取 NVDIMM-N 运行状况信息（功能索引 11）](get-nvdimm-n-health-info--function-index-11-.md)                                             | 是                                                    | 是                                                  |
| 12             | [获取能量源运行状况信息（功能索引 12）](get-energy-source-health-info--function-index-12-.md)                                   | 是                                                    | 否                                                   |
| 13             | [获取操作统计信息（功能索引 13）](get-operational-statistics--function-index-13-.md)                                         | 是                                                    | 是                                                  |
| 14             | [获取供应商日志页大小（功能索引 14）](get-vendor-log-page-size--function-index-14-.md)                                             | 是                                                    | 是                                                  |
| 15             | [获取供应商日志页（功能索引 15）](get-vendor-log-page--function-index-15-.md)                                                       | 是                                                    | 是                                                  |
| 16             | [查询错误注入状态（功能索引 16）](query-error-injection-status--function-index-16-.md)                                     | 是                                                    | 是                                                  |
| 17             | [注入错误（功能索引 17）](inject-error--function-index-17-.md)                                                                     | 是                                                    | 是                                                  |
| 18             | [获取注入的错误（功能索引 18）](get-injected-errors--function-index-18-.md)                                                       | 是                                                    | 是                                                  |
| 19             | [擦除 NVM 图像（功能索引 19）](erase-nvm-image--function-index-19-.md)                                                               | 是                                                    | 是                                                  |
| 20             | [Arm NVDIMM-N（功能索引 20）](arm-nvdimm-n--function-index-20-.md)                                                                     | 是                                                    | 是                                                  |
| 21             | [重置为出厂默认设置（功能索引 21）](reset-to-factory-defaults--function-index-21-.md)                                           | 是                                                    | 是                                                  |
| 22             | [启动固件更新（功能索引 22）](start-firmware-update--function-index-22-.md)                                                   | 是                                                    | 是                                                  |
| 23             | [发送固件更新数据（功能索引 23）](send-firmware-update-data--function-index-23-.md)                                           | 是                                                    | 是                                                  |
| 24             | [完成固件更新（功能索引 24）](finish-firmware-update--function-index-24-.md)                                                 | 是                                                    | 是                                                  |
| 25             | [选择固件映像槽（功能索引 25）](select-firmware-image-slot--function-index-25-.md)                                         | 是                                                    | 是                                                  |
| 26             | [获取固件信息（功能索引 26）](get-firmware-info--function-index-26-.md)                                                           | 是                                                    | 是                                                  |
| 27             | [I2C 读取（功能索引 27）](i2c-read--function-index-27-.md)                                                                             | 是                                                    | 是                                                  |
| 28             | [I2C 写入（功能索引 28）](i2c-write--function-index-28-.md)                                                                           | 是                                                    | 是                                                  |
| 29             | [读取类型化数据（功能索引 29）](read-typed-data--function-index-29-.md)                                                               | 是                                                    | 是                                                  |
| 30             | [写入类型化数据（功能索引 30）](write-typed-data--function-index-30-.md)                                                             | 是                                                    | 是                                                  |
| 31             | [设置内存错误计数器（功能索引 31）](set-memory-error-counters--function-index-31-.md)                                           | 是                                                    | 是                                                  |

## <a name="_dsm-method-input"></a>_DSM 方法输入

*Arg3* 为 "所有函数" 是一个包值。 如果函数不采用输入参数，则包值不包含任何数据。 如果函数采用输入参数，则包值将包含一个缓冲区。

如果函数不采用输入参数，并且 *Arg3* 不是空包，则函数应返回无效输入参数的 **常规状态代码** 。

## <a name="_dsm-method-output"></a>_DSM 方法输出

所有方法都将返回一个长度大于或等于4个字节的缓冲区。 返回缓冲区的前4个字节的结构如下所示：

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">字段</th>
<th align="left">字节长度</th>
<th align="left">字节偏移量</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">常规状态代码</td>
<td align="left">2</td>
<td align="left">0</td>
<td align="left"><p>0–成功</p>
<p>1-不支持</p>
<p>2–输入参数无效</p>
<p>3-I2C 通信错误</p>
<p>4-Function-Specific 错误代码</p>
<p>5–特定于供应商的错误代码</p>
<p>6-0xFFFF –保留</p></td>
</tr>
<tr class="even">
<td align="left">Function-Specific 错误代码</td>
<td align="left">1</td>
<td align="left">2</td>
<td align="left">此字段包含特定于调用的函数的错误代码。 如果 <strong>常规状态代码</strong> 等于 <strong>特定于函数的错误代码</strong>，则此字段只包含有效的信息。</td>
</tr>
<tr class="odd">
<td align="left">特定于供应商的错误代码</td>
<td align="left">1</td>
<td align="left">3</td>
<td align="left">此字段包含供应商特定的状态代码。 如果 <strong>常规状态代码</strong> 等于 <strong>供应商特定的错误代码</strong>，则它仅包含有效的信息。</td>
</tr>
</tbody>
</table>

任何非零 **常规状态代码** 都指示函数失败。 在此版本的规范中定义的函数不会返回 **常规状态代码** " **不受支持**"。 所有必需函数应返回有效数据或指示运行时错误的错误代码。 非必需函数可能会返回 Function-Specific 错误代码，以指示没有要返回的有效数据。

所有保留的位和字节的值都应为0。 除非特别声明，否则所有多字节字段应以小字节序方式表示。

> [!NOTE]
> 对字节可寻址 Energy-Backed 接口寄存器的引用介绍了此接口中指定的函数的许多返回字段。 这些字段应与 "可通过字节寻址的支持能源的接口版本1.0，JEDEC 标准版" 中定义的寄存器完全相同。 2233-22 "Byte-Addressable Energy-Backed 接口规范的修订版本。 规范版本在 "[获取 NVDIMM-N 标识" (函数索引 1)](get-nvdimm-n-identification--function-index-1-.md)函数返回的 "**规范修订**" 字段中报告。
>
> 某些返回字段指 (ES) 有关能源源的信息。 当 ES 策略是设备管理的时，该平台应读取字段说明中指定的硬件注册，以检索与 ES 相关的所有信息。 当 ES 策略由主机管理时，平台应通过特定于平台的机制获得 ES 相关信息。 在这种情况下，所有与 ES 相关的信息都应与字段说明中指定的硬件寄存器相同的二进制布局提供。
