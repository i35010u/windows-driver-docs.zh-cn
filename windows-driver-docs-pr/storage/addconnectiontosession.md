---
title: AddConnectionToSession
description: AddConnectionToSession
ms.assetid: c2762e75-8732-4c48-83a9-24ccd39218eb
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8bf9abc658b7e73db4c388276dcfa4d0c81c479b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382745"
---
# <a name="addconnectiontosession"></a>AddConnectionToSession


**AddConnectionToSession**方法指示的微型端口驱动程序，用于管理 iSCSI 发起程序以将新的连接添加到登录会话的 HBA。

支持的微型端口驱动程序[MSiSCSI\_操作类](msiscsi-operations-wmi-class.md)必须提供至少一个存根 （stub） 针对此方法，但该方法的功能的实现是可选的。 如果该方法未实现添加的连接功能，它应返回错误。

**AddConnectionToSession**属于未发布 MSiSCSI\_操作 WMI 类。 有关参数的说明**AddConnectionToSession**方法，请参阅成员的说明[ **AddConnectionToSession\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff550122)和[ **AddConnectionToSession\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff550123)结构。

 

 





