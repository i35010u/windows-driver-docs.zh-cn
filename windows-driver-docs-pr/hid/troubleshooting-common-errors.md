---
title: 排查常见错误
description: 本部分介绍调试其 I²C 固件或驱动程序软件时，硬件供应商和驱动程序开发人员可能会遇到的常见问题。
ms.assetid: F53BD17C-ABBC-495F-895A-99BFC7E29B71
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60d99d986283e81e41e7dad5137302f03f45ba91
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376741"
---
# <a name="troubleshooting-common-errors"></a>排查常见错误


本部分介绍调试其 I²C 固件或驱动程序软件时，硬件供应商和驱动程序开发人员可能会遇到的常见问题。

## <a name="troubleshooting-common-errors"></a>排查常见错误


### <a href="" id="hidi2c-driver-does-not-load"></a>HIDI²C 驱动程序不会加载

如果加载 I²C 控制器驱动程序，但设备未显示在 Windows 设备管理器，请参阅以下。

如果没有在主机或设备的无效 ASL 代码，通常会出现上述问题。 若要确定问题是否是由于未能匹配 INF，请参阅 setupapi.dev.log 文件。 另一个问题是由于不匹配的标记是*错误代码 10* Windows 设备管理器中。

若要解决此问题，请确保以下。

-   \_CID 值必须是**PNP0C50**。
-   I²C**控制器**并**设备特征**在 BIOS 中必须是准确。
-   **HID 描述符地址**（适用于设备） 在 BIOS 中必须是准确。
-   GPIO 中断必须正确标识并标记为**排他性的、 级别、 ActiveLow**。

请参阅以了解详细信息在 HID I2C 协议规范的第 13 节。 （此规范可在更高版本的日期。）

### <a name="invalid-report-descriptor"></a>无效的报表描述符

如果主机无法正确报告描述符检索设备时，请确保满足以下条件。

1.  枚举序列必须完成运行之前检索到的报表描述符。
2.  4 和 6 HID 描述符中的字节偏移量必须是有效的。 （注意特定长度。）

如果你验证该设备中检索到的正确报表描述符，但仍存在似乎是一个相关的问题，请确保在以下情况成立。

1.  WReportDescLength 字段是准确的。
2.  隐藏报表的格式正确。 （若要验证这一点，测试的替代如 USB 总线。）

### <a name="faq"></a>常见问题

本部分重点介绍问题由硬件供应商和驱动程序开发人员常见问题。

1.  Windows 8 的收件箱 HIDI²C 驱动程序适用的 HID 设备通过 I²C 连接？
    -   是的它将在提供的固件是符合 HID I²C 协议规范

2.  设备 （如键盘） 和 OS 驱动程序之间传输的数据结构是什么？
    -   数据结构会根据 HID 标准中定义的是报表的描述符，输入报表的窗体。 在设备本身，而不是 HIDI²C 定义输入的报表结构。 您只需报告键盘用法就像使用 USB 键盘，然后提供每个 HID I²C 规范报告描述符和相应的输入

3.  如果多个报表都在同一时间被缓冲，设备怎么办？
    -   如果多个报表都被缓冲，设备应保留断言直到最后一个报表具有读取 （确认） 的中断。 只要指定的读取操作后对报表的更多数据，设备应保留的行添加使用级别触发器 GPIO 设置。

4.  是准确地说，我们应获取在 USB 和 I²C 连接的情况下相同 DevicePath？
    -   否，设备路径不是 USB 和 I²C 之间完全相同。 差异是细微但值得注意的内容。 请参阅硬件 ID 部分的更多详细信息中 Windows Driver Kit (WDK)。

5.  什么是为了使 HIDI²C 设备来利用 Windows 收件箱 HIDI²C 驱动程序所需的 I²C 传输限制？
    -   控制器支持所需的所有 I²C 都传输最多为 4 KB。 HID 报表描述符的最大长度为 4 KB。

 

 




