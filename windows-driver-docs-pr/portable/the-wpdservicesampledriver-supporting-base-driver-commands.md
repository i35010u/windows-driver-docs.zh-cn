---
Description: 对基础驱动程序命令 (WpdServiceSampleDriver) 的支持
title: 对基础驱动程序命令 (WpdServiceSampleDriver) 的支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e97804a357b14431b945461821b1441da193c6a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370493"
---
# <a name="support-for-base-driver-commands-wpdservicesampledriver"></a>对基础驱动程序命令 (WpdServiceSampleDriver) 的支持


基础驱动程序模块 (*WpdBaseDriver.cpp*) 有关此示例处理两个命令：WPD\_命令\_常见\_获取\_对象\_ID\_FROM\_的永久\_UNIQUE\_ID 和 WPD\_命令\_常见\_保存\_客户端\_信息。

但是， *WpdBaseDriver.cpp*也是在我们的驱动程序中处理的所有命令的起始点。 这意味着所有命令首先都处理的**WpdBaseDriver::DispatchMessage**方法。 此方法检查给定命令的类别，然后将其转发到枚举、 属性的、 功能或服务命令处理程序。

下表介绍了支持的基本驱动程序模块，以及支持的基本驱动程序模块的命令的处理程序的两个命令。

|                                                                       |                                      |                                                                                                                       |
|-----------------------------------------------------------------------|--------------------------------------|-----------------------------------------------------------------------------------------------------------------------|
| Command                                                               | 处理程序                              | 描述                                                                                                           |
| WPD\_命令\_常见\_获取\_对象\_ID\_FROM\_的永久\_UNIQUE\_ID | OnGetOjectIDsFromPersistentUniqueIDs | 当应用程序尝试检索与给定的永久唯一标识符匹配的对象标识符时发出。 |
| WPD\_命令\_常见\_保存\_客户端\_信息                       | OnSaveClientInfo                     | 当应用程序尝试打开到设备或服务的连接时发出。                                       |

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


****
[The WpdServiceSampleDriver](the-wpdservicesampledriver-sample.md)

[WPD 驱动程序示例](the-wpd-driver-samples.md)

 

 





