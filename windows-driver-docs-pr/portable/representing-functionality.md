---
Description: 表示功能
title: 表示功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca55b289195133a11db9a2e56c10f3442312de3f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376220"
---
# <a name="representing-functionality"></a>表示功能


函数对象的用途是设备的确定或以逻辑方式分组的功能。 例如，应用程序能够看到设备支持短信服务 (SMS)，方法是查看 SMS 功能对象。 或者，应用程序可以查看设备具有相机功能的寻找仍然映像捕获的功能对象。

这种灵活的对象表示形式启用多功能功能的设备的支持。 驱动程序可以公开任何功能的对象表示其设备，这是比使用传统设备类更精细。 也很有用来隔离重叠的功能部分。 例如，某些单元格手机可能有两个相机、 四个存储设备等。

在 Windows 7 和及更高版本，服务对象通过提供丰富的功能查询和内容的抽象分组来扩展功能的对象。 应用程序可以使用服务对象来发现设备功能并更有效地与内容交互。 例如，应用程序能够看到设备通过查找实现 Microsoft 的完整枚举同步联系人服务的服务对象来支持联系人同步。 现在，应用程序可以找到所有联系人在设备上而无需搜索存储层次结构。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[**WPD 驱动程序概述**](wpd-drivers-overview.md)

 

 





