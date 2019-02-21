---
title: MSiSCSI\_LUNMappingInformation WMI 类
description: MSiSCSI\_LUNMappingInformation WMI 类
ms.assetid: 646add52-f946-4169-9f6b-974253ec30af
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8e40aa4b601feb670a4f2fb99fc42def75a57b31
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533423"
---
# <a name="msiscsilunmappinginformation-wmi-class"></a>MSiSCSI\_LUNMappingInformation WMI 类


## <span id="ddk_msiscsi_lunmappinginformation_wmi_class_kr"></span><span id="DDK_MSISCSI_LUNMAPPINGINFORMATION_WMI_CLASS_KR"></span>


MSiSCSI\_LUNMappingInformation 类公开操作系统将分配给特定的逻辑单元的 SCSI 地址信息。 SCSI 地址信息必须保持一致的信息的[MSiSCSI\_TargetMappings WMI 类](msiscsi-targetmappings-wmi-class.md)报表。

微型端口驱动程序必须创建一个实例 MSiSCSI\_LUNMappingInformation WMI 类的每个物理设备对象 (PDO) 与逻辑单元关联。

由于此类与特定 LUN，管理 HBA 的微型端口驱动程序必须注册此类为 LUN 使用 PDO 的名称。

MSiSCSI\_LUNMappingInformation 类中定义，则不发布*Operations.mof*。

当 WMI 工具套件编译此类定义时，它会生成[ **MSiSCSI\_LUNMappingInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff563065)数据结构。

SCSI 地址信息的该 MSiSCSI\_LUNMappingInformation 公开必须与发起方的微型端口驱动程序提供的信息一致的逻辑单元的枚举期间端口驱动程序。

发起程序所需实现 MSiSCSI\_LUNMappingInformation 类。

发起程序必须注册 MSiSCSI\_LUNMappingInformation 类使用的逻辑单元的 PDO 名称。

发起程序必须创建一个实例 MSiSCSI\_它枚举每个逻辑单元的 LUNMappingInformation 类。

 

 





