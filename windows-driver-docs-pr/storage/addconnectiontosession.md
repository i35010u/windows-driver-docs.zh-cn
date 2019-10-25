---
title: AddConnectionToSession
description: AddConnectionToSession
ms.assetid: c2762e75-8732-4c48-83a9-24ccd39218eb
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 32644be4288bed8ea8918a651ff73afeffcb22eb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845119"
---
# <a name="addconnectiontosession"></a>AddConnectionToSession


**AddConnectionToSession**方法指示用于管理 iSCSI 发起程序 HBA 的微型端口驱动程序，以将新连接添加到登录会话。

支持[MSiSCSI\_操作类](msiscsi-operations-wmi-class.md)的微型端口驱动程序必须至少为此方法提供存根，但该方法的功能的实现是可选的。 如果该方法未实现添加连接功能，它应该返回错误。

**AddConnectionToSession**属于未发布的 MSiSCSI\_操作 WMI 类。 有关**AddConnectionToSession**方法的参数的说明，请参阅[**AddConnectionToSession\_IN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_addconnectiontosession_in)和[**AddConnectionToSession\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_addconnectiontosession_out)结构的成员说明。

 

 





