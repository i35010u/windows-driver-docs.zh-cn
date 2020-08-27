---
description: 支持 (WpdServiceSampleDriver) 的基本驱动程序命令
title: 支持 (WpdServiceSampleDriver) 的基本驱动程序命令
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce3cb3702095b0239fb29f3c58899a10a86cd38b
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969400"
---
# <a name="support-for-base-driver-commands-wpdservicesampledriver"></a>支持 (WpdServiceSampleDriver) 的基本驱动程序命令

基本驱动程序模块 (*WpdBaseDriver*) 的示例处理两个命令： WPD \_ 命令 \_ 公共 \_ \_ \_ \_ 从永久性唯一 id 获取对象 id \_ \_ \_ 和 WPD \_ 命令 \_ 常见的 \_ 保存 \_ 客户端 \_ 信息。

但是， *WpdBaseDriver* 也是驱动程序中所有命令处理的起点。 这意味着， **WpdBaseDriver：:D ispatchmessage** 方法首先处理所有命令。 此方法检查给定命令的类别，然后将其转发到枚举、属性、功能或服务命令处理程序。

下表描述了基本驱动程序模块支持的两个命令，以及基础驱动程序模块支持的命令的处理程序。

| Command                                                               | Handler                              | 说明                                                                                                           |
|-----------------------------------------------------------------------|--------------------------------------|-----------------------------------------------------------------------------------------------------------------------|
| WPD \_ 命令 \_ COMMON \_ \_ \_ \_ 从 \_ 持久的 \_ 唯一 \_ ID 获取对象 ID | OnGetOjectIDsFromPersistentUniqueIDs | 当应用程序尝试检索与给定的持久唯一标识符相匹配的对象标识符时发出。 |
| WPD \_ 命令 \_ 通用 \_ 保存 \_ 客户端 \_ 信息                       | OnSaveClientInfo                     | 当应用程序尝试打开与设备或服务的连接时发出。                                       |

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题

****
[WpdServiceSampleDriver](the-wpdservicesampledriver-sample.md)

[WPD 驱动程序示例](the-wpd-driver-samples.md)
