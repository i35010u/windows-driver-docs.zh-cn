---
title: MSiSCSI \_ 操作 WMI 类
description: MSiSCSI \_ 操作 WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 0ff877c5d853ea6f301c2e7112ed860c7a9f17fb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821215"
---
# <a name="msiscsi_operations-wmi-class"></a>MSiSCSI \_ 操作 WMI 类


## <span id="ddk_msiscsi_operations_wmi_class_kr"></span><span id="DDK_MSISCSI_OPERATIONS_WMI_CLASS_KR"></span>


MSiSCSI \_ 操作 wmi 类提供 iSCSI 发起程序服务用来与 HBA 发起程序通信的 wmi 方法。

由于此类与存储微型端口驱动程序的特定实例相关联，因此微型端口驱动程序必须使用微型端口驱动程序管理 (PDO) 的特定物理设备对象的名称注册该类。

此 WMI 类没有数据块;因此，当 WMI 工具套件编译此类定义时，它不会生成任何对应于类的结构声明。 编译会生成与类方法关联的结构声明，这些声明在类方法的引用页中进行了介绍。

对于属于此类的每个方法，托管对象格式 (MOF) 语法在该方法的参考页中进行了介绍。 以下主题介绍了这些方法及其随附的结构：

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

 

 





