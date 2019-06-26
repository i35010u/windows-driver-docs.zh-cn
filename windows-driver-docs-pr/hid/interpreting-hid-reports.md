---
title: 解释 HID 报告
description: 解释 HID 报告
ms.assetid: 10f8c3a1-ad60-4c99-a425-fa8c9a3be0e1
keywords:
- HID 报告 WDK，解释
- 报告 WDK HID，解释
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 833f6a86bacfb0f2cc2b3655d65421cf3f065bd5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375893"
---
# <a name="interpreting-hid-reports"></a>解释 HID 报告





本部分介绍用户模式应用程序和内核模式驱动程序如何使用 HidP\_*Xxx* [HIDClass 支持例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)解释 HID 报表中的控制数据。

从报表中提取控件数据的信息，请参阅：

[通过指定其使用情况数据的提取值](extracting-value-data-by-specifying-its-usage.md)

[提取设置为 ON 的按钮用途](extracting-button-usages-that-are-set-to-on.md)

[提取并设置控制数据的数据索引](extracting-and-setting-control-data-by-data-indices.md)

有关如何设置控制数据在报表中的信息，请参阅：

[通过指定其使用情况设置值数据](setting-value-data-by-specifying-its-usage.md)

[通过指定其使用情况设置按钮状态](setting-button-state-by-specifying-its-usage.md)

[提取并设置控制数据的数据索引](extracting-and-setting-control-data-by-data-indices.md)

 

 




