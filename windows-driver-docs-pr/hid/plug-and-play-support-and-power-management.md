---
title: I2C 的即插即用支持
description: 本部分介绍支持在 I i2c 上支持 HID 的设备的即插即用支持。
ms.assetid: 2D51B1B7-345E-4311-81D6-8A14CE2B44FE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1182e8d65061c647c3dfd434b4c393717dbe6b57
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968454"
---
# <a name="plug-and-play-support-for-i2c"></a>I2C 的即插即用支持


本部分介绍对通过 I i2c 传输支持 HID 的设备的即插即用支持。

### <a name="driver-loading"></a>驱动程序加载

Windows 基于硬件标识符和 INF 之间兼容的标识符匹配，加载 HID I i2c 类驱动程序。 此标识符是由高级配置和电源接口（ACPI）生成的。 在 ACPI 中为 I i2c 设备节点生成硬件标识符。 除唯一的硬件标识符外，所有 HID I i2c 兼容设备都必须公开兼容标识符。

ACPI 5.0 规范包括对 HID 类设备的支持。 HID I ²的 ACPI 定义如下所示。

|                           |                                             |             |                                                 |                                                                                      |
|---------------------------|---------------------------------------------|-------------|-------------------------------------------------|--------------------------------------------------------------------------------------|
| 字段                     | Value                                       | ACPI 对象 | 格式                                          | 注释                                                                             |
| 兼容 ID             | PNP0C50                                     | \_CID       | 采用 ACPI0C50 或 PNP0C50 格式的字符串     | CompatibleID                                                                         |
| 硬件 ID               | 特定于供应商                             | \_HID       | 格式为 VVVVdddd 的字符串（例如 NVDA0001） | VendorID + DeviceID                                                                  |
| 子系统                 | 特定于供应商                             | \_该子       | 格式为 VVVVssss 的字符串（例如 INTL1234） | SubVendorID + SubSystemID                                                            |
| 硬件修订         | 特定于供应商                             | \_HRV       | 0xRRRR （2byte 修订版）                         | RevisionID                                                                           |
| 当前资源设置 | 特定于供应商                             | \_CRS       | 字节流                                     | \_对于 I2C 控制器和 gpio 中断 resp，必须包含 I2CSerialBus 和 gpio INT。 |
| 设备特定方法    | GUID {3CDFF6F7-4267-4555-AD05-B30A3D8938DE} | \_DSM       | 程序包                                         | 定义包含 HID 描述符地址的结构。                        |

 

每个 HID I i2c 设备必须提供以下必填字段：

-   兼容 ID
-   硬件 ID
-   硬件修订
-   当前资源设置
-   设备特定方法

有关其他信息，请参阅高级配置和电源接口（ACPI）5.0 规范。

下面提供了随机 HID I i2c 设备的硬件 Id 和兼容 Id 的示例。 这些详细信息基于一个示例设备，该设备将自身报告为一个包含 "供应商特定" 类的顶级集合的隐藏。

高级配置和电源接口（ACPI）生成以下硬件 Id 和兼容 Id 以加载 HID I i2c 传输驱动程序：

**硬件标识符**：兼容标识符

**ACPI \\Vid \_ xxxx&Pid \_ Yyyy&Rev \_ zzzz;**： ACPI \\ PNP0C50

**ACPI \\Vid \_ xxxxPid \_ yyyy;**： 

**ACPI \\ xxxxyyyy;**： 


 

在上面的示例中，硬件 ID 是使用从 \_ 示例设备的 HID ACPI 方法中提取的值生成的。 可使用从 \_ 示例设备的 CID ACPI 方法中提取的值生成兼容 ID。 适用于 PNP0C50 的 HID 的兼容 ID 必须始终为版本1.0 的。

**注意**   如果提供了一个 INF，则只应使用上表的左栏中的硬件标识符。 （请勿使用右列中的兼容标识符。）

 

HIDClass.sys 组件生成的 HID 客户端设备节点的硬件 ID 如下所示：

**硬件标识符**：兼容标识符

**HID \\即使 \_ MSFT&DEV \_ 0010&REV \_ 0002&Col01;**： N/A

**-HID \\即使 \_ MSFT&DEV \_ 0010&Col01 HID \\ MSFT0010&Col01;**： N/A

**-HID \\ \*MSFT0010Col01**：暂缺

**-HID \_设备已 \_ 启动： FF00 \_ U:0001;**： N/A

**-HID \_设备**：暂缺


 

硬件 ID 是 HIDClass.sys 生成的，对所有传输都是相同的。 此标识符基于从 HIDI2C.sys （从 ACPI 提取）传递到 HIDClass.sys 的值。

### <a name="device-enumeration-sequence"></a>设备枚举序列

加载 HID I i2c 设备驱动程序（HIDI2C.Sys）后，它将开始通过 i2c 总线与设备进行通信。 驱动程序执行的第一个操作是设备枚举序列。

下面的列表提供枚举序列。 请注意，此列表的顺序可能会在将来的 Windows 版本中发生更改。

1.  从系统 BIOS 检索 HID I i2c 设备的 ACPI ASL 代码。
2.  从设备检索 HID 描述符。
    -   写入 HID 描述符地址
    -   读取 HID 描述符

3.  \_向设备发出设置电源。
    -   写入设置 \_ 电源命令

4.  向设备发出重置（主机启动的重置）。
    -   写入重置命令
    -   设备断言 GPIO 中断
    -   从输入注册读取值（0x00 0x00）

5.  检索设备中的报表描述符。
    -   写入报表描述符地址
    -   读取报表描述符

如果主机未能成功完成与设备的任何步骤1-5，则 HIDI ² C 驱动程序可能会加载，错误值为*代码 10*。 此类命令中没有内置的重试逻辑。

**注意**   步骤4和5可能会并行执行，以优化 I i2c 的时间。 由于报表描述符为（a）静态和（b）非常长，因此 Windows 8 可能会发出5的请求，同时等待来自设备的响应。

 

### <a name="supported-hid-ic-commands"></a><a href="" id="supported-hid-i2c-commands"></a>支持的 HID I i2c 命令

HIDI2C.SYS 驱动程序支持以下命令

|                 |                                                |                                                                                                                                                                                                       |
|-----------------|------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 命令         | 用途                                  | 使用时                                                                                                                                                                                        |
| 重置           | Windows 支持主机发起的重置。     | Windows 将在以下情况下发出此命令-设备初始化-禁用/启用-卸载/重新安装                                                                         |
| 获取/设置 \_ 报表 | Windows 支持 Get/Set \_ 报表命令。 | Windows 将在以下情况下发出此命令-当 HID 客户端驱动程序发出 get/set 功能报表请求时（当 HID 客户端驱动程序发出同步输入/输出报表时） |
| 设置 \_ 电源      | Windows 支持设置 \_ 电源命令        | 在以下情况下，Windows 将发出此命令-当系统在关闭系统时转换为低功耗 S3/连接待机状态。                               |

 

 

 




