---
title: 初始化 HID 报告
description: 初始化 HID 报告
keywords:
- HID 报告 WDK，初始化
- 报告 WDK HID，初始化
- 初始化报表
- 控制 WDK HID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b5fb576c040282ef35a4606904cc4e58a01b1932
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796215"
---
# <a name="initializing-hid-reports"></a>初始化 HID 报告

本部分介绍用户模式应用程序和内核模式驱动程序如何初始化 HID 报表，然后再使用 [HIDClass 支持例程](/windows-hardware/drivers/ddi/index) 或 HID 类驱动程序 IOCTLs。

若要初始化报表缓冲区，应用程序或驱动程序将创建该报表类型所需大小的零初始化缓冲区（以字节为单位）。 ReportByteLength 的 [**HIDP \_ cap**](/windows-hardware/drivers/ddi/hidpi/ns-hidpi-_hidp_caps)结构的 *Xxx* 成员指定输入、输出和功能报表所需的大小。 初始化报表缓冲区后，应用程序或驱动程序可以使用 **HidP \_ set**_Xxx_ 例程来设置报表中的控件数据。 首次使用报表时， **HidP \_ set**_Xxx_ 例程将报表 ID 设置为与指定的 [HID 使用情况](hid-usages.md)关联的 ID。 如果应用程序或驱动程序随后尝试设置与报表 ID 不兼容的用法，则 **HidP \_ set**_XXX_ 例程将返回 HidP \_ 状态 \_ 不兼容 \_ 报表 id 的状态 \_ 。
