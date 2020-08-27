---
description: 支持 (WpdBasicHardwareDriverSample) 的基本驱动程序命令
title: 支持 (WpdBasicHardwareDriverSample) 的基本驱动程序命令
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b760edaceaa600518586f37c07e5771fe02ff679
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969180"
---
# <a name="support-for-base-driver-commands-wpdbasichardwaredriversample"></a>支持 (WpdBasicHardwareDriverSample) 的基本驱动程序命令


 (*WpdBaseDriver* 的示例的基本驱动程序模块) 处理单个命令 (WPD \_ 命令 \_ 公共 \_ GET \_ OBJECT \_ id \_ FROM \_ 持久性 \_ UNIQUE \_ id) 。 不过，此模块也是示例驱动程序中所有命令处理的起点。 这意味着， **WpdBaseDriver：:D ispatchmessage** 方法首先处理所有命令。 此方法检查给定命令的类别，然后将其转发到枚举、属性或功能命令处理程序。

**WpdBaseDriver：:D ispatchmessage**方法中发生的一项更改是，删除了用于检查与资源相关的命令的代码。 由于示例驱动程序不支持资源，因此不再需要处理相关的命令;任何发送非实现的命令的应用程序都会收到 E \_ NOTIMPL 错误。

下表中的信息描述了基本驱动程序模块支持的命令以及命令的处理程序。

| Command                                                               | Handler                              | 说明                                                                                                              |
|-----------------------------------------------------------------------|--------------------------------------|--------------------------------------------------------------------------------------------------------------------------|
| WPD \_ 命令 \_ COMMON \_ \_ \_ \_ 从 \_ 持久的 \_ 唯一 \_ ID 获取对象 ID | OnGetOjectIDsFromPersistentUniqueIDs | 当应用程序尝试检索与给定的持久唯一标识符相匹配的对象标识符时发出。 |

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


****
[WpdBasicHardwareDriverSample](the-wpdbasichardwaredriver-sample.md)

[WPD 驱动程序示例](the-wpd-driver-samples.md)

 

 





