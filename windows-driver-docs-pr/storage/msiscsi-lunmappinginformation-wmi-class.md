---
title: MSiSCSI \_ LUNMAPPINGINFORMATION WMI 类
description: MSiSCSI \_ LUNMAPPINGINFORMATION WMI 类
ms.assetid: 646add52-f946-4169-9f6b-974253ec30af
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: bb12838d3c90357c9de3458b66dafff535bd1973
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188012"
---
# <a name="msiscsi_lunmappinginformation-wmi-class"></a>MSiSCSI \_ LUNMAPPINGINFORMATION WMI 类


## <span id="ddk_msiscsi_lunmappinginformation_wmi_class_kr"></span><span id="DDK_MSISCSI_LUNMAPPINGINFORMATION_WMI_CLASS_KR"></span>


MSiSCSI \_ LUNMappingInformation 类公开操作系统分配给特定逻辑单元的 SCSI 地址信息。 SCSI 地址信息必须与 [MSiSCSI \_ TargetMappings WMI 类](msiscsi-targetmappings-wmi-class.md) 报告的信息一致。

微型端口驱动程序必须 \_ 为每个 (PDO) 与一个逻辑单元关联的物理设备对象创建一个 MSiSCSI LUNMAPPINGINFORMATION WMI 类的实例。

由于此类与特定 LUN 相关联，因此管理 HBA 的微型端口驱动程序必须使用 LUN 的 PDO 名称注册此类。

MSiSCSI \_ LUNMappingInformation 类未发布，并在 *操作*中定义。

当 WMI 工具套件编译此类定义时，它会生成 [**MSiSCSI \_ LUNMappingInformation**](/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_msiscsi_lunmappinginformation) 数据结构。

MSiSCSI LUNMappingInformation 公开的 SCSI 地址信息 \_ 必须与发起程序的微型端口驱动程序在逻辑单元枚举过程中提供给端口驱动程序的信息一致。

发起程序需要执行 MSiSCSI \_ LUNMappingInformation 类。

发起 \_ 程序必须使用逻辑单元的 PDO 名称注册 MSiSCSI LUNMappingInformation 类。

发起 \_ 程序必须为它所枚举的每个逻辑单元创建一个 MSiSCSI LUNMappingInformation 类的实例。

 

