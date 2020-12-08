---
title: iSCSI WMI 操作类
description: iSCSI WMI 操作类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4d2c9998a47e4f200b0932f39a950c3e713fd4ad
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835065"
---
# <a name="iscsi-wmi-operations-classes"></a>iSCSI WMI 操作类


## <span id="ddk_iscsi_wmi_classes_that_define_the_interface_between_the_iscsi_disc"></span><span id="DDK_ISCSI_WMI_CLASSES_THAT_DEFINE_THE_INTERFACE_BETWEEN_THE_ISCSI_DISC"></span>


ISCSI 操作类是内部的未发布 WMI 类，iSCSI 发起程序服务使用这些类来与 iSCSI 发起程序通信。 存储微型端口驱动程序必须实现这些类才能与 iSCSI 发现库通信。 有关在微型端口驱动程序中支持这些类所需的内容的详细信息，请参阅与类关联的结构的参考页。 这些结构在 *Iscsiop* 中定义。

ISCSI 操作类不属于用户模式 WMI 架构，WMI 管理应用程序不能尝试直接调用其方法。

发起程序微型端口驱动程序必须支持以下 WMI 工具类：

[ISCSI \_ 持久性 \_ 登录 WMI 类](iscsi-persistent-login-wmi-class.md)

[MSiSCSI \_ ADAPTEREVENT WMI 类](msiscsi-adapterevent-wmi-class.md)

[MSiSCSI \_ BOOTINFORMATION WMI 类](msiscsi-bootinformation-wmi-class.md)

[MSiSCSI \_ LUNMAPPINGINFORMATION WMI 类](msiscsi-lunmappinginformation-wmi-class.md)

[MSiSCSI \_ 操作 WMI 类](msiscsi-operations-wmi-class.md)

[MSiSCSI \_ PERSISTENTLOGINS WMI 类](msiscsi-persistentlogins-wmi-class.md)

[MSiSCSI \_ SECURITYCONFIGOPERATIONS WMI 类](msiscsi-securityconfigoperations-wmi-class.md)

[MSiSCSI \_ TARGETMAPPINGS WMI 类](msiscsi-targetmappings-wmi-class.md)

 

 





