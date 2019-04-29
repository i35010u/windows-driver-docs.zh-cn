---
title: RemoveConnectionFromSession
description: RemoveConnectionFromSession
ms.assetid: ae23713a-c75d-4669-a643-44e95dbb713c
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 90ffa0371ee38faa104854609c99ec2cf2592166
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374182"
---
# <a name="removeconnectionfromsession"></a>RemoveConnectionFromSession


**RemoveConnectionFromSession**方法指示的微型端口驱动程序，用于管理 iSCSI 发起程序 HBA 登录会话中删除的连接。

ISCSI 发起程序 （即，虚拟微型端口驱动程序） 不支持具有多个连接的会话。 不要使用**RemoveConnectionFromSession** iSCSI 发起程序。

**RemoveConnectionFromSession**方法不会在会话中删除最后一次连接。 您应关闭与使用单个连接的会话[LogoutFromTarget](logoutfromtarget.md)方法。

**RemoveConnectionFromSession**属于未发布[MSiSCSI\_Operations WMI 类](msiscsi-operations-wmi-class.md)。 有关参数的说明**RemoveConnectionFromSession**方法，请参阅成员的说明[ **RemoveConnectionFromSession\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff563974)并[ **RemoveConnectionFromSession\_出**](https://msdn.microsoft.com/library/windows/hardware/ff563976)结构。

微型端口驱动程序实现 MSiSCSI\_操作 WMI 类必须支持此方法。

 

 





