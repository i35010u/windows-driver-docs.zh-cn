---
title: 初始化 HID 报告
description: 初始化 HID 报告
ms.assetid: 14229315-3928-4421-a8d8-c3f7837bf1c3
keywords:
- HID 报告 WDK，初始化
- 报告 WDK HID，初始化
- 初始化报表
- 控制 WDK HID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 33d5ec11b0545ec914cbb7a42f7ff5bf7d4ec6e9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841583"
---
# <a name="initializing-hid-reports"></a>初始化 HID 报告





本部分介绍用户模式应用程序和内核模式驱动程序如何初始化 HID 报表，然后再使用[HIDClass 支持例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)或 HID 类驱动程序 IOCTLs。

若要初始化报表缓冲区，应用程序或驱动程序将创建该报表类型所需大小的零初始化缓冲区（以字节为单位）。 作为 HID 集合的[**HIDP\_cap**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/ns-hidpi-_hidp_caps)结构的*Xxx*ReportByteLength 成员指定输入、输出和功能报表所需的大小。 初始化报表缓冲区后，应用程序或驱动程序可以使用**HidP\_set**_Xxx_例程来设置报表中的控件数据。 首次使用报表时， **HidP\_set**_Xxx_例程将报表 ID 设置为与指定的[HID 使用情况](hid-usages.md)关联的 ID。 如果应用程序或驱动程序随后尝试设置与报表 ID 不兼容的使用情况，则**HidP\_set**_Xxx_例程将\_状态\_不兼容\_报表\_ID 返回状态。

 

 




