---
description: 表示功能
title: 表示功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 437a4723061d8e90a106e2e83c5ba0617874a235
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88968550"
---
# <a name="representing-functionality"></a>表示功能


功能对象的目的是在逻辑上标识或对设备的特征功能进行分组。 例如，应用程序可以通过查找 SMS 功能对象来查看设备是否支持短消息服务 (SMS) 。 或者，应用程序可以通过查找静止图像捕获功能对象来查看设备是否具有相机功能。

这种灵活的对象表示形式启用了对具有多功能功能的设备的支持。 驱动程序可以公开代表其设备的任何功能对象，而不是使用传统的设备类。 这对于隔离重叠的功能块也很有用。 例如，某些手机可能有两个照相机、四个存储设备等。

在 Windows 7 和更高版本中，服务对象通过提供丰富的功能查询和内容的抽象分组来扩展函数对象。 应用程序可以使用服务对象发现设备功能并更有效地与内容交互。 例如，应用程序可以通过查找实现 Microsoft Full 枚举同步联系人服务的服务对象来查看设备是否支持联系人同步。 现在，应用程序可以找到设备上的所有联系人，无需搜索存储层次结构。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[**WPD 驱动程序概述**](wpd-drivers-overview.md)

 

 





