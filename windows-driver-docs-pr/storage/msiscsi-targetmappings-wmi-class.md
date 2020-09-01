---
title: MSiSCSI \_ TARGETMAPPINGS WMI 类
description: MSiSCSI \_ TARGETMAPPINGS WMI 类
ms.assetid: 12bfe80a-8431-4607-99f5-ddd6815aecc6
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d41c4812e40a0a4c92b8498a018d78407cc798d7
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188921"
---
# <a name="msiscsi_targetmappings-wmi-class"></a>MSiSCSI \_ TARGETMAPPINGS WMI 类


## <span id="ddk_msiscsi_targetmappings_wmi_class_kr"></span><span id="DDK_MSISCSI_TARGETMAPPINGS_WMI_CLASS_KR"></span>


MSiSCSI \_ TARGETMAPPINGS WMI 类包含一组 iSCSI 逻辑单元号 (LUN) 映射与会话关联。 由发起方建立的登录会话公开的每个 LUN 都有一个映射。 每个会话的映射由作为 MSiSCSI TargetMappings WMI 类中的嵌入类的 [ISCSI \_ TargetMapping wmi 类](iscsi-targetmapping-wmi-class.md) 的实例描述 \_ 。

每个 iSCSI 发起程序都必须实现 MSiSCSI \_ TargetMappings 类。 ISCSI 发起程序服务依赖于此类来与 HBA 发起程序通信。

\_对于管理发起方 HBA 的每个加载的微型端口驱动程序实例，都应该有一个 MSiSCSI TARGETMAPPINGS WMI 类的实例。 微型端口驱动程序必须 \_ 使用微型端口驱动程序管理 (PDO) 的特定物理设备对象的名称注册 MSiSCSI TargetMappings 类。

MSiSCSI \_ TargetMappings 类未发布，并在 *操作*中定义。

当 WMI 工具套件编译此类定义时，它会生成 [**MSiSCSI \_ TargetMappings**](/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_msiscsi_targetmappings) 数据结构。

发起程序需要执行 MSiSCSI \_ TargetMappings 类。

ISCSI 发起程序服务依赖于 MSiSCSI \_ TargetMappings 类来与 HBA 发起程序通信。 管理 HBA 发起程序的微型端口驱动程序必须 \_ 针对每个 HBA 实现 MSiSCSI TargetMappings 类的一个实例。

发起 \_ 程序必须使用用于 HBA 的 PDO 名称注册 MSiSCSI TargetMappings 类。

 

