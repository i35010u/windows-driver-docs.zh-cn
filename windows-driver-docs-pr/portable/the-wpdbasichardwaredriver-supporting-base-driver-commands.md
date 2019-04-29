---
Description: 对基础驱动程序命令 (WpdBasicHardwareDriverSample) 的支持
title: 对基础驱动程序命令 (WpdBasicHardwareDriverSample) 的支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 709d0a97c013101eaf92bb1eb650e094bb703e11
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378819"
---
# <a name="support-for-base-driver-commands-wpdbasichardwaredriversample"></a>对基础驱动程序命令 (WpdBasicHardwareDriverSample) 的支持


该示例的基础驱动程序模块 (*WpdBaseDriver.cpp*) 处理单个命令 (WPD\_命令\_常见\_获取\_对象\_ID\_从\_的永久\_UNIQUE\_ID)。 但是，此模块也是所有命令中的示例驱动程序的处理的起始点。 这意味着所有命令首先都处理的**WpdBaseDriver::DispatchMessage**方法。 此方法检查给定命令的类别，然后将其转发到枚举、 属性或功能的命令处理程序。

中出现一次更改**WpdBaseDriver::DispatchMessage**方法就删除检查与资源相关的命令的代码。 示例驱动程序不支持资源，因为它已不需要处理相关的命令;将非实现命令发送的任何应用程序接收电子\_NOTIMPL 错误。

下表中所介绍的是该模块支持的基本驱动程序，以及命令的处理程序的命令。

| Command                                                               | 处理程序                              | 描述                                                                                                              |
|-----------------------------------------------------------------------|--------------------------------------|--------------------------------------------------------------------------------------------------------------------------|
| WPD\_命令\_常见\_获取\_对象\_ID\_FROM\_的永久\_UNIQUE\_ID | OnGetOjectIDsFromPersistentUniqueIDs | 当应用程序尝试检索与给定的永久唯一标识符匹配的对象标识符时发出。 |

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


****
[WpdBasicHardwareDriverSample](the-wpdbasichardwaredriver-sample.md)

[WPD 驱动程序示例](the-wpd-driver-samples.md)

 

 





