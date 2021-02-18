---
title: 排查常见错误
description: '本部分介绍硬件供应商和驱动程序开发人员在调试其 I # C 固件或驱动程序软件时可能遇到的常见问题。'
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 163177001c2cf4a7b999c886ab52c913912a2d46
ms.sourcegitcommit: 20569e032b1e0963ad295e9c46b7682832af3d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/18/2021
ms.locfileid: "100648144"
---
# <a name="troubleshooting-common-errors"></a>排查常见错误

本文介绍硬件供应商和驱动程序开发人员在调试其 I # C 固件或驱动程序软件时可能遇到的常见问题。

## <a name="hidic-driver-does-not-load"></a>HIDI ² C 驱动程序未加载

如果加载了 i2c 控制器驱动程序，但设备未出现在 Windows Device Manager 中，请参阅以下内容：

如果没有有效的 [ACPI 源语言 (](https://uefi.org/htmlspecs/ACPI_Spec_6_4_html/19_ASL_Reference/ACPI_Source_Language_Reference.html?highlight=acpi%20source%20language) 主机或设备的 ASL) 代码，则通常会出现上述问题。 若要确定问题是否是由 INF 匹配失败引起的，请参阅 setupapi.log 文件。 导致问题的另一个指示器是 Windows Device Manager 中的 *错误代码 10* 。

若要解决此问题，请确保以下各项：

- \_CID 值必须是 **PNP0C50**。
- 在 BIOS 中，I e **控制器** 和 **设备特征** 必须准确。
- 在 BIOS 中，设备) 的 **HID 描述符地址** (必须准确。
- 必须正确地标识 GPIO 中断，并将其标记为 " **独占"、"级别"、"ActiveLow**"。

有关更多详细信息，请参阅 [HID I2C 协议规范](/previous-versions/windows/hardware/design/dn642101(v=vs.85)) 的第13部分。

## <a name="invalid-report-descriptor"></a>报表描述符无效

如果主机未能从设备检索正确的报表描述符，请确保满足以下条件：

- 枚举序列必须在检索报表描述符之前完成运行。
- HID 描述符中的字节偏移量4和6必须有效。  (请特别注意长度。 ) 

如果已验证从设备检索到正确的报表描述符，但仍存在相关问题，请确保满足以下条件：

- WReportDescLength 字段是正确的。
- HID 报表的格式正确。  (验证此项，请测试备用总线，如 USB。 ) 

### <a name="faq"></a>常见问题解答

本部分重点介绍硬件供应商和驱动程序开发人员经常提出的问题。

- Windows 8 收件箱 HIDI ² C 驱动程序是否适用于通过 i2c 连接的 HID 设备
  - 是的，如果固件符合此 HID I i2c 协议规范，它将正常工作

- 设备 (（例如键盘) 和操作系统驱动程序）之间的数据结构是什么？
  - 数据结构的形式为根据 HID 标准，由报表描述符定义的输入报表。 设备本身而不是 HIDI ² C 定义输入报告结构。 你只需像使用 USB 键盘一样报告键盘用法，然后根据 HID I i2c 规范提供描述符和相应的输入报告

- 如果同时缓存多个报表，该设备应该做什么？
  - 如果正在缓存多个报表，则设备应将中断断言，直到最后一个报表读取 (确认) 。 只要在给定的读取操作之后有更多的数据要报告，设备就应该使用级别触发器 GPIO 设置来使该线路断言。

- 是否准确指出，在采用 USB 和 I-C 连接的情况下，我们应该获得相同的 DevicePath？
  - 不能，USB 和 I u 之间的设备路径将不相同。 差异很小，但值得注意。 有关更多详细信息，请参阅 Windows 驱动程序工具包 (WDK) 中的硬件 ID 部分。

- HIDI ²设备使用 Windows 收件箱 HIDI ² C 驱动程序所需的 I i2c 传输限制是什么？
  - 所有的 i2c 控制器都需要支持最大为 4 KB 的传输。 最大 HID 报表描述符长度为 4 KB。