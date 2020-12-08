---
title: MSiSCSI \_ PERSISTENTLOGINS WMI 类
description: MSiSCSI \_ PERSISTENTLOGINS WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f0c78cef6cb0e64c5a05e9b76a55b9159c37b856
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796473"
---
# <a name="msiscsi_persistentlogins-wmi-class"></a>MSiSCSI \_ PERSISTENTLOGINS WMI 类


## <span id="ddk_msiscsi_persistentlogins_wmi_class_kr"></span><span id="DDK_MSISCSI_PERSISTENTLOGINS_WMI_CLASS_KR"></span>


MSiSCSI \_ PERSISTENTLOGINS WMI 类报告指定发起方实例的持久目标登录会话的列表。 与每个特定的持久性登录会话关联的信息由 [ISCSI \_ 永久性 \_ 登录 WMI 类](iscsi-persistent-login-wmi-class.md)定义。

需要管理 HBA 发起程序的微型端口驱动程序才能实现 MSiSCSI \_ PERSISTENTLOGINS WMI 类。

MSiSCSI \_ PersistentLogins 类未发布，并在 *操作* 中定义。

当 WMI 工具套件编译此类定义时，它会生成 [**MSiSCSI \_ PersistentLogins**](/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_msiscsi_persistentlogins) 数据结构。

 

