---
title: MSiSCSI \_ TARGETMAPPINGS WMI 类
description: MSiSCSI \_ TARGETMAPPINGS WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f7a4afa725687e0e9247a9336bc7052524ecee80
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804423"
---
# <a name="msiscsi_targetmappings-wmi-class"></a>MSiSCSI \_ TARGETMAPPINGS WMI 类


## <span id="ddk_msiscsi_targetmappings_wmi_class_kr"></span><span id="DDK_MSISCSI_TARGETMAPPINGS_WMI_CLASS_KR"></span>


MSiSCSI \_ TARGETMAPPINGS WMI 类包含一组 iSCSI 逻辑单元号 (LUN) 映射与会话关联。 由发起方建立的登录会话公开的每个 LUN 都有一个映射。 每个会话的映射由作为 MSiSCSI TargetMappings WMI 类中的嵌入类的 [ISCSI \_ TargetMapping wmi 类](iscsi-targetmapping-wmi-class.md) 的实例描述 \_ 。

每个 iSCSI 发起程序都必须实现 MSiSCSI \_ TargetMappings 类。 ISCSI 发起程序服务依赖于此类来与 HBA 发起程序通信。

\_对于管理发起方 HBA 的每个加载的微型端口驱动程序实例，都应该有一个 MSiSCSI TARGETMAPPINGS WMI 类的实例。 微型端口驱动程序必须 \_ 使用微型端口驱动程序管理 (PDO) 的特定物理设备对象的名称注册 MSiSCSI TargetMappings 类。

MSiSCSI \_ TargetMappings 类未发布，并在 *操作* 中定义。

当 WMI 工具套件编译此类定义时，它会生成 [**MSiSCSI \_ TargetMappings**](/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_msiscsi_targetmappings) 数据结构。

发起程序需要执行 MSiSCSI \_ TargetMappings 类。

ISCSI 发起程序服务依赖于 MSiSCSI \_ TargetMappings 类来与 HBA 发起程序通信。 管理 HBA 发起程序的微型端口驱动程序必须 \_ 针对每个 HBA 实现 MSiSCSI TargetMappings 类的一个实例。

发起 \_ 程序必须使用用于 HBA 的 PDO 名称注册 MSiSCSI TargetMappings 类。

 

