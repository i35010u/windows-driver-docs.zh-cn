---
title: iSCSI WMI 操作类
description: iSCSI WMI 操作类
ms.assetid: de8b31f8-e5dc-4ac0-8bd4-6912868310a0
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 71698517b723b0a01eed4ac533443250a6dd7620
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555562"
---
# <a name="iscsi-wmi-operations-classes"></a>iSCSI WMI 操作类


## <span id="ddk_iscsi_wmi_classes_that_define_the_interface_between_the_iscsi_disc"></span><span id="DDK_ISCSI_WMI_CLASSES_THAT_DEFINE_THE_INTERFACE_BETWEEN_THE_ISCSI_DISC"></span>


ISCSI 操作类是 iSCSI 发起程序服务使用与 iSCSI 发起程序进行通信的内部、 未发布 WMI 类。 存储微型端口驱动程序必须实现这些类来与 iSCSI 发现库进行通信。 有关什么是微型端口驱动程序中支持这些类的详细信息，请参阅与类相关联的结构的参考页。 这些结构中定义*Iscsiop.h*。

ISCSI 操作类不是用户模式下 WMI 架构的一部分，WMI 管理应用程序必须尝试进行直接调用其方法。

发起方微型端口驱动程序必须支持以下 WMI 工具类：

[ISCSI\_持久\_登录 WMI 类](iscsi-persistent-login-wmi-class.md)

[MSiSCSI\_AdapterEvent WMI 类](msiscsi-adapterevent-wmi-class.md)

[MSiSCSI\_BootInformation WMI 类](msiscsi-bootinformation-wmi-class.md)

[MSiSCSI\_LUNMappingInformation WMI 类](msiscsi-lunmappinginformation-wmi-class.md)

[MSiSCSI\_操作 WMI 类](msiscsi-operations-wmi-class.md)

[MSiSCSI\_PersistentLogins WMI 类](msiscsi-persistentlogins-wmi-class.md)

[MSiSCSI\_SecurityConfigOperations WMI 类](msiscsi-securityconfigoperations-wmi-class.md)

[MSiSCSI\_TargetMappings WMI 类](msiscsi-targetmappings-wmi-class.md)

 

 





