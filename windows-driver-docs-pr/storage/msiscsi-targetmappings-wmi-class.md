---
title: MSiSCSI\_TargetMappings WMI 类
description: MSiSCSI\_TargetMappings WMI 类
ms.assetid: 12bfe80a-8431-4607-99f5-ddd6815aecc6
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 106ace48cc639d24bbbc3d7c7679463e47801a17
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384666"
---
# <a name="msiscsitargetmappings-wmi-class"></a>MSiSCSI\_TargetMappings WMI 类


## <span id="ddk_msiscsi_targetmappings_wmi_class_kr"></span><span id="DDK_MSISCSI_TARGETMAPPINGS_WMI_CLASS_KR"></span>


MSiSCSI\_TargetMappings WMI 类包含一组与会话相关联的 iSCSI 逻辑单元号 (LUN) 映射。 没有公开由登录名会话发起方建立的每个 LUN 的映射。 每个会话的映射由的实例描述[ISCSI\_TargetMapping WMI 类](iscsi-targetmapping-wmi-class.md)MSiSCSI 内，它是嵌入的类\_TargetMappings WMI 类。

每个 iSCSI 发起程序必须实现 MSiSCSI\_TargetMappings 类。 ISCSI 发起程序服务依赖于此类与 HBA 发起程序进行通信。

应该有一个实例 MSiSCSI\_TargetMappings WMI 类为每个管理发起方 HBA 的微型端口驱动程序加载的实例。 微型端口驱动程序必须注册 MSiSCSI\_TargetMappings 类使用的微型端口驱动程序管理的特定的物理设备对象 (PDO) 名称。

MSiSCSI\_TargetMappings 类中定义，则不发布*Operations.mof*。

当 WMI 工具套件编译此类定义时，它会生成[ **MSiSCSI\_TargetMappings** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iscsiop/ns-iscsiop-_msiscsi_targetmappings)数据结构。

发起程序所需实现 MSiSCSI\_TargetMappings 类。

ISCSI 发起程序服务依赖于 MSiSCSI\_TargetMappings 类与 HBA 发起程序进行通信。 管理 HBA 发起程序的微型端口驱动程序必须实现一个实例 MSiSCSI\_TargetMappings 类每个 HBA。

发起程序必须注册 MSiSCSI\_TargetMappings 类使用的 HBA PDO 的名称。

 

 





