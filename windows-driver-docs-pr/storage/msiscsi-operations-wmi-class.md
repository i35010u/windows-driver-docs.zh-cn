---
title: MSiSCSI\_操作 WMI 类
description: MSiSCSI\_操作 WMI 类
ms.assetid: 993118db-cddf-438a-8fdd-566353a6246b
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5c1750284c9eb452d5af8eac6d9f0a6062d1eeb6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387449"
---
# <a name="msiscsioperations-wmi-class"></a>MSiSCSI\_操作 WMI 类


## <span id="ddk_msiscsi_operations_wmi_class_kr"></span><span id="DDK_MSISCSI_OPERATIONS_WMI_CLASS_KR"></span>


MSiSCSI\_操作 WMI 类提供的 iSCSI 发起程序服务使用与 HBA 发起程序进行通信的 WMI 方法。

因为此类与存储微型端口驱动程序的特定实例相关联，微型端口驱动程序必须注册使用的微型端口驱动程序管理的特定的物理设备对象 (PDO) 名称的类。

此 WMI 类都有无数据块;因此，当 WMI 工具套件编译此类定义，它不会生成对应于类的任何结构声明。 编译确实会生成具有类方法中，关联的结构声明并描述了这些内容在类方法的参考页。

属于此类的每个方法的托管的对象格式 (MOF) 语法所述的方法的参考页。 以下主题介绍了这些方法和其随附的结构：

[AddConnectionToSession](addconnectiontosession.md)

[AddRADIUSServer](addradiusserver.md)

[DeleteInitiatorNodeName](deleteinitiatornodename.md)

[LoginToTarget](logintotarget.md)

[LogoutFromTarget](logoutfromtarget.md)

[RemoveConnectionFromSession](removeconnectionfromsession.md)

[RemovePersistentLogin](removepersistentlogin.md)

[RemoveRADIUSServer](removeradiusserver.md)

[**ScsiInquiry**](scsiinquiry.md)

[**ScsiReadCapacity**](scsireadcapacity.md)

[**ScsiReportLuns**](scsireportluns.md)

[SendTargets](sendtargets.md)

[SetCHAPSharedSecret](setchapsharedsecret.md)

[SetInitiatorNodeName](setinitiatornodename.md)

[SetRADIUSSharedSecret](setradiussharedsecret.md)

 

 





