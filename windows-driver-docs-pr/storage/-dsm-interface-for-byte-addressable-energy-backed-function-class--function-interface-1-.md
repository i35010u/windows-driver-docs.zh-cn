---
title: '\_字节可寻址能源的 DSM 接口支持的函数类 （函数接口 1）'
description: 此接口设计为映射到 JEDEC 字节可寻址能源支持接口标准，以便最大程度减少 BIOS 复杂性。
ms.assetid: 895F1B13-4F2D-4B6B-A3CE-60A8AC9EE7B0
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ad64fa2cd12d9b0dadcb63d034e9c09dc7109f5d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382752"
---
# <a name="dsm-interface-for-byte-addressable-energy-backed-function-class-function-interface-1"></a>\_字节可寻址能源的 DSM 接口支持的函数类 （函数接口 1）


此接口设计为映射到 JEDEC 字节可寻址能源支持接口标准，以便最大程度减少 BIOS 复杂性。 它提供公共基础的报告设备功能和功能，以便操作系统软件可以通过相同的机制与各种实现交互。 此外，它允许对通过 I2C 寄存器访问特定于供应商的功能的支持。

符合的平台\_DSM 字节可寻址能源支持的函数类接口 (函数接口 1) 可以支持实现 NVDIMM N *JEDEC 字节可寻址能源支持接口*（函数类 0x01 和函数接口 0x01） 规范。 有关详细信息，请参阅[JEDEC 字节可寻址能源支持接口规范 （文档 JESD245）](https://www.jedec.org/document_search?search_api_views_fulltext=jesd245)。

## <a name="span-iddsminterfaceforbyteaddressableenergybackedfunctionclassfunctioninterface1spanspan-iddsminterfaceforbyteaddressableenergybackedfunctionclassfunctioninterface1spanspan-iddsminterfaceforbyteaddressableenergybackedfunctionclassfunctioninterface1spandsm-interface-for-byte-addressable-energy-backed-function-class-function-interface-1"></a><span id="DSM_Interface_for_Byte_Addressable_Energy_Backed_Function_Class_Function_Interface_1"></span><span id="dsm_interface_for_byte_addressable_energy_backed_function_class_function_interface_1"></span><span id="DSM_INTERFACE_FOR_BYTE_ADDRESSABLE_ENERGY_BACKED_FUNCTION_CLASS_FUNCTION_INTERFACE_1"></span>\_字节可寻址能源的 DSM 接口支持的函数类、 函数接口 1


\_DSM GUID 是 1EE68B36-D4BD-4a1a-9A16-4F8E53D46E05。

\_本文档中定义的 DSM 函数应实现 NVDIMM ACPI Namespace 设备对象中。 术语**必需**是否该函数必须返回有效的数据，或不是指。

### <a name="span-idmandatoryfunctionsandfieldsspanspan-idmandatoryfunctionsandfieldsspanspan-idmandatoryfunctionsandfieldsspanmandatory-functions-and-fields"></a><span id="Mandatory_functions_and_fields"></span><span id="mandatory_functions_and_fields"></span><span id="MANDATORY_FUNCTIONS_AND_FIELDS"></span>必需的函数和字段

下表指定的函数和字段都是必需的。

| 函数索引 | 函数名称                                                                                                                                | 对于设备管理能源源 (ES) 策略是必需的 | 对于主机托管能源源 (ES) 策略是必需的 |
|----------------|----------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------|------------------------------------------------------|
| 0              | [查询实现的函数 （函数索引 0）](query-implemented-functions--function-index-0-.md)                                         | 是                                                    | 是                                                  |
| 1              | [获取 NVDIMM N 标识 （函数索引 1）](get-nvdimm-n-identification--function-index-1-.md)                                         | 是                                                    | 是                                                  |
| 2              | [获取保存操作要求 （函数索引 2）](get-save-operation-requirements--function-index-2-.md)                                 | 是                                                    | 是                                                  |
| 3              | [获取能源源识别 （函数索引 3）](get-energy-source-identification--function-index-3-.md)                               | 是                                                    | 是                                                  |
| 4              | [获取最后一个备份的信息 （函数索引 4）](get-last-backup-information--function-index-4-.md)                                         | 是                                                    | 是                                                  |
| 5              | [获取 NVM 阈值 （函数索引 5）](get-nvm-thresholds--function-index-5-.md)                                                           | 是                                                    | 是                                                  |
| 6              | [设置 NVM 生存期百分比警告阈值 （函数索引 6）](set-nvm-lifetime-percentage-warning-threshold--function-index-6-.md)     | 是                                                    | 是                                                  |
| 7              | [获取能源源阈值 （函数索引 7）](get-energy-source-thresholds--function-index-7-.md)                                       | 是                                                    | 否                                                   |
| 8              | [设置能量源生存期警告阈值 （函数索引 8）](set-energy-source-lifetime-warning-threshold--function-index-8-.md)       | 是                                                    | 否                                                   |
| 9              | [设置能源源温度警告阈值 （函数索引 9）](set-energy-source-temperature-warning-threshold--function-index-9-.md) | 是                                                    | 否                                                   |
| 10             | [获取关键运行状况信息 （函数索引 10）](get-critical-health-info--function-index-10-.md)                                             | 是                                                    | 是                                                  |
| 11             | [获取 NVDIMM N 运行状况信息 （函数索引 11）](get-nvdimm-n-health-info--function-index-11-.md)                                             | 是                                                    | 是                                                  |
| 12             | [获取能源源运行状况信息 （函数索引 12）](get-energy-source-health-info--function-index-12-.md)                                   | 是                                                    | 否                                                   |
| 13             | [获取操作统计信息 （函数索引 13）](get-operational-statistics--function-index-13-.md)                                         | 是                                                    | 是                                                  |
| 14             | [获取供应商日志页大小 （函数索引 14）](get-vendor-log-page-size--function-index-14-.md)                                             | 是                                                    | 是                                                  |
| 15             | [获取供应商日志页 （函数索引 15）](get-vendor-log-page--function-index-15-.md)                                                       | 是                                                    | 是                                                  |
| 16             | [查询错误注入状态 （函数索引 16）](query-error-injection-status--function-index-16-.md)                                     | 是                                                    | 是                                                  |
| 17             | [注入错误 （函数索引 17）](inject-error--function-index-17-.md)                                                                     | 是                                                    | 是                                                  |
| 18             | [获取注入错误 （函数索引 18）](get-injected-errors--function-index-18-.md)                                                       | 是                                                    | 是                                                  |
| 19             | [清除 NVM 幅图像 （函数索引 19）](erase-nvm-image--function-index-19-.md)                                                               | 是                                                    | 是                                                  |
| 20             | [Arm NVDIMM N （函数索引 20）](arm-nvdimm-n--function-index-20-.md)                                                                     | 是                                                    | 是                                                  |
| 21             | [重置为出厂默认值 （函数索引 21）](reset-to-factory-defaults--function-index-21-.md)                                           | 是                                                    | 是                                                  |
| 22             | [启动固件更新 （函数索引 22）](start-firmware-update--function-index-22-.md)                                                   | 是                                                    | 是                                                  |
| 23             | [发送固件更新数据 （函数索引 23）](send-firmware-update-data--function-index-23-.md)                                           | 是                                                    | 是                                                  |
| 24             | [完成固件更新 （函数索引 24）](finish-firmware-update--function-index-24-.md)                                                 | 是                                                    | 是                                                  |
| 25             | [选择固件映像槽 （函数索引 25）](select-firmware-image-slot--function-index-25-.md)                                         | 是                                                    | 是                                                  |
| 26             | [获取固件信息 （函数索引 26）](get-firmware-info--function-index-26-.md)                                                           | 是                                                    | 是                                                  |
| 27             | [I2C 读取 （函数索引 27）](i2c-read--function-index-27-.md)                                                                             | 是                                                    | 是                                                  |
| 28             | [I2C 写入 （函数索引 28）](i2c-write--function-index-28-.md)                                                                           | 是                                                    | 是                                                  |
| 29             | [读取类型化的数据 （函数索引 29）](read-typed-data--function-index-29-.md)                                                               | 是                                                    | 是                                                  |
| 30             | [写入类型化的数据 （函数索引 30）](write-typed-data--function-index-30-.md)                                                             | 是                                                    | 是                                                  |
| 31             | [设置内存错误计数器 （函数索引 31）](set-memory-error-counters--function-index-31-.md)                                           | 是                                                    | 是                                                  |

 

## <a name="span-iddsmmethodinputspanspan-iddsmmethodinputspandsm-method-input"></a><span id="DSM_METHOD_INPUT"></span><span id="dsm_method_input"></span>\_DSM 方法输入


*Arg3*的所有函数是包值。 如果该函数不采用一个输入的参数，包值不包含数据。 如果函数采用一个输入的参数，则包值包含一个缓冲区。

如果该函数不采用一个输入的参数和*Arg3*不是一个空包，该函数应返回**常规状态代码**的输入参数无效。

## <a name="dsm-method-output"></a>\_DSM 方法的输出


所有方法将都返回的缓冲区长度大于或等于 4 个字节。 返回缓冲区的前 4 个字节的结构，如下所示：

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
<th align="left">字节偏移</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">常规状态代码</td>
<td align="left">2</td>
<td align="left">0</td>
<td align="left"><p>0-成功</p>
<p>1 – 不受支持</p>
<p>2 – 输入参数无效</p>
<p>3 – I2C 通信错误</p>
<p>4 – 函数特定的错误代码</p>
<p>5 – 供应商特定错误代码</p>
<p>6-0xFFFF – 保留</p></td>
</tr>
<tr class="even">
<td align="left">特定于函数的错误代码</td>
<td align="left">1</td>
<td align="left">2</td>
<td align="left">此字段包含特定于调用该函数的错误代码。 此字段只能包含有效的信息，如果<strong>常规状态代码</strong>等于<strong>特定于函数的错误代码</strong>。</td>
</tr>
<tr class="odd">
<td align="left">供应商特定错误代码</td>
<td align="left">1</td>
<td align="left">3</td>
<td align="left">此字段包含特定于供应商的状态代码。 如果仅包含有效信息<strong>常规状态代码</strong>等于<strong>供应商特定错误代码</strong>。</td>
</tr>
</tbody>
</table>

 

任何非零**常规状态代码**指示失败的函数。 没有在此版本的规范中定义的函数应会返回**常规状态代码**的**不支持**。 所有必需的函数应返回有效的数据或错误代码指示运行时错误。 非强制函数可能返回以指示没有有效数据要返回特定于函数的错误代码。

所有保留的位和字节应具有值为 0。 除非特别声明，否则应以小字节序的方式表示所有多字节字段。

&gt; \[!请注意\]    &gt;Byte Addressable Energy-Backed 接口注册到的引用描述此接口中指定的函数的多个返回字段。 这些字段应相同到寄存器在接口中定义"字节可寻址能源履行，版本 1.0，JEDEC 标准不可以。 2233-22"Byte-Addressable Energy-Backed 接口规范的修订版本。 中报告的规范版本**规范修订**返回的字段[获取 NVDIMM N 标识 (函数索引 1)](get-nvdimm-n-identification--function-index-1-.md)函数。

&gt;某些返回字段指能源源 (ES) 有关的信息。 设备管理 ES 策略时，平台应读取的字段说明检索所有 ES 相关信息中指定的硬件寄存器。 主机托管 ES 策略时，该平台应通过特定于平台的机制获取 ES 相关信息。 在这种情况下，应在相同的二进制布局的硬件那样显示 ES 相关的所有信息字段说明中指定的注册。

&gt;

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[存储驱动程序设计指南](https://go.microsoft.com/fwlink/p/?LinkId=798409)

[JEDEC 字节可寻址能源支持接口 NVDIMM 特定于设备的方法 (\_DSM)](jedec-byte-addressable-energy-backed-interface-nvdimms-device-specific-method---dsm-.md)

 

 






