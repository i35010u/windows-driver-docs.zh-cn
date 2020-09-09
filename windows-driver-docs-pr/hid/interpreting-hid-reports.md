---
title: 解释 HID 报告
description: 解释 HID 报告
ms.assetid: 10f8c3a1-ad60-4c99-a425-fa8c9a3be0e1
keywords:
- HID 报告 WDK，解释
- 报告 WDK HID，解释
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 281cc36e540f9ba5268dc3e875db59e7a98b96d7
ms.sourcegitcommit: 9145bffd4cc3b990a9ebff43b588db6ef2001f5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/09/2020
ms.locfileid: "89592419"
---
# <a name="interpreting-hid-reports"></a>解释 HID 报告





本部分介绍用户模式的应用程序和内核模式驱动程序如何使用 HidP \_ *Xxx* [HIDClass 支持例程](/windows-hardware/drivers/ddi/index)来解释 HID 报表中的控件数据。

有关从报表提取控件数据的信息，请参阅以下内容：

[通过指定值数据的使用情况来提取该值]()

[正在提取设置为 ON 的按钮用法]()

[按数据索引提取和设置控件数据]()

有关如何在报表中设置控件数据的信息，请参阅以下内容：

[通过指定值数据的使用情况来设置该值]()

[通过指定其用法来设置按钮状态]()

[按数据索引提取和设置控件数据]()

 

