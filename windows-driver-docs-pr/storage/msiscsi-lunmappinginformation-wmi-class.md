---
title: MSiSCSI\_LUNMappingInformation WMI 类
description: MSiSCSI\_LUNMappingInformation WMI 类
ms.assetid: 646add52-f946-4169-9f6b-974253ec30af
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 35fa9621b173a2980b79736b5ae1423f4fbdd50a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845348"
---
# <a name="msiscsi_lunmappinginformation-wmi-class"></a>MSiSCSI\_LUNMappingInformation WMI 类


## <span id="ddk_msiscsi_lunmappinginformation_wmi_class_kr"></span><span id="DDK_MSISCSI_LUNMAPPINGINFORMATION_WMI_CLASS_KR"></span>


MSiSCSI\_LUNMappingInformation 类公开操作系统分配给特定逻辑单元的 SCSI 地址信息。 SCSI 地址信息必须与[MSiSCSI\_TARGETMAPPINGS WMI 类](msiscsi-targetmappings-wmi-class.md)报告的信息一致。

微型端口驱动程序必须为与逻辑单元关联的每个物理设备对象（PDO）创建一个 MSiSCSI\_LUNMappingInformation WMI 类的实例。

由于此类与特定 LUN 相关联，因此管理 HBA 的微型端口驱动程序必须使用 LUN 的 PDO 名称注册此类。

MSiSCSI\_LUNMappingInformation 类未发布，并在*操作*中定义。

当 WMI 工具套件编译此类定义时，它会生成[**MSiSCSI\_LUNMappingInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_msiscsi_lunmappinginformation)数据结构。

MSiSCSI\_LUNMappingInformation 公开的 SCSI 地址信息必须与发起程序的微型端口驱动程序在逻辑单元枚举过程中提供给端口驱动程序的信息一致。

发起方是实现 MSiSCSI\_LUNMappingInformation 类所必需的。

发起程序必须使用逻辑单元的 PDO 名称注册 MSiSCSI\_LUNMappingInformation 类。

发起程序必须为其枚举的每个逻辑单元创建一个 MSiSCSI\_LUNMappingInformation 类的实例。

 

 





