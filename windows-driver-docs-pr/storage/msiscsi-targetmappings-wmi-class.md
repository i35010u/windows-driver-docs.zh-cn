---
title: MSiSCSI\_TargetMappings WMI 类
description: MSiSCSI\_TargetMappings WMI 类
ms.assetid: 12bfe80a-8431-4607-99f5-ddd6815aecc6
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 73aeb9a6f69518a8b8775ce96ac69c5c383437e6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838872"
---
# <a name="msiscsi_targetmappings-wmi-class"></a>MSiSCSI\_TargetMappings WMI 类


## <span id="ddk_msiscsi_targetmappings_wmi_class_kr"></span><span id="DDK_MSISCSI_TARGETMAPPINGS_WMI_CLASS_KR"></span>


MSiSCSI\_TargetMappings WMI 类包含一组与会话关联的 iSCSI 逻辑单元号（LUN）映射。 由发起方建立的登录会话公开的每个 LUN 都有一个映射。 每个会话的映射由作为 MSiSCSI\_TargetMappings WMI 类中的嵌入类的[TARGETMAPPING WMI 类的\_](iscsi-targetmapping-wmi-class.md)实例描述。

每个 iSCSI 发起程序都必须实现 MSiSCSI\_TargetMappings 类。 ISCSI 发起程序服务依赖于此类来与 HBA 发起程序通信。

对于管理发起方 HBA 的每个加载的微型端口驱动程序实例，都应有一个 MSiSCSI\_TargetMappings WMI 类的实例。 微型端口驱动程序必须使用微型端口驱动程序管理的特定物理设备对象（PDO）的名称注册 MSiSCSI\_TargetMappings 类。

MSiSCSI\_TargetMappings 类未发布，并在*操作*中定义。

当 WMI 工具套件编译此类定义时，它会生成[**MSiSCSI\_TargetMappings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_msiscsi_targetmappings)数据结构。

发起方是实现 MSiSCSI\_TargetMappings 类所必需的。

ISCSI 发起程序服务依赖于 MSiSCSI\_TargetMappings 类来与 HBA 发起程序通信。 管理 HBA 发起程序的微型端口驱动程序必须针对每个 HBA 实现 MSiSCSI\_TargetMappings 类的一个实例。

发起程序必须使用用于 HBA 的 PDO 名称注册 MSiSCSI\_TargetMappings 类。

 

 





