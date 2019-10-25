---
title: RemoveConnectionFromSession
description: RemoveConnectionFromSession
ms.assetid: ae23713a-c75d-4669-a643-44e95dbb713c
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 590e3ba7410419d1d9cd51f5b832e413c20218d9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842715"
---
# <a name="removeconnectionfromsession"></a>RemoveConnectionFromSession


**RemoveConnectionFromSession**方法指示用于管理 iSCSI 发起程序 HBA 的微型端口驱动程序从登录会话中删除连接。

ISCSI 发起程序（即虚拟微型端口驱动程序）不支持具有多个连接的会话。 不要将**RemoveConnectionFromSession**与 iSCSI 发起程序一起使用。

**RemoveConnectionFromSession**方法不会从会话中删除最后一个连接。 应使用[LogoutFromTarget](logoutfromtarget.md)方法通过单一连接关闭会话。

**RemoveConnectionFromSession**属于未发布的[MSISCSI\_操作 WMI 类](msiscsi-operations-wmi-class.md)。 有关**RemoveConnectionFromSession**方法的参数的说明，请参阅[**RemoveConnectionFromSession\_IN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_removeconnectionfromsession_in)和[**RemoveConnectionFromSession\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_removeconnectionfromsession_out)结构的成员说明。

实现 MSiSCSI\_操作 WMI 类的微型端口驱动程序必须支持此方法。

 

 





