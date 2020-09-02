---
description: Windows 便携设备中的 PROPERTYKEY 和 GUID
title: Windows 便携设备中的 PROPERTYKEY 和 GUID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1578ff9596e3939a8d43c89199d13af43a590d26
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382305"
---
# <a name="propertykeys-and-guids-in-windows-portable-devices"></a>Windows 便携设备中的 PROPERTYKEY 和 GUID


属性或命令由 **PROPERTYKEY** 结构标识。 **PROPERTYKEY**结构由两部分组成： *FMTID*成员的 GUID () ，以及*pid*成员)  (DWORD。 GUID 部分用于指示属性或命令所属的类别 (也就是说，相关属性属于同一类别，而相关命令属于同一类别;因此，它们具有相同的 *fmtid*) 。 DWORD 部分指示属性或命令 ID，并用于区分属性或命令类别中的单个属性或命令 (也就是说，同一类别中的属性或命令的 *pid* 值将不同) 。

本文档的 "参考" 部分介绍了 WPD 定义的所有 PROPERTYKEY 值。 这些值对应于命令、属性和资源。 如果创建自定义 PROPERTYKEY 值，则应定义新的 GUID 类别;请勿重复使用 WPD GUID 值，或者存在与现有和未来 WPD 指定的 PROPERTYKEYs 冲突的风险。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[**WPD \_ 内容 \_ 类型 \_ 功能 \_ 对象**](/previous-versions/windows/hardware/drivers/ff597845(v=vs.85))

[**对于对象的要求**](requirements-for-objects.md)

[**对象格式 Guid**](/previous-versions/windows/hardware/drivers/ff597651(v=vs.85))

[**资源的要求**](/previous-versions/windows/hardware/drivers/ff597663(v=vs.85))

[**命令**](/previous-versions/windows/hardware/drivers/ff597554(v=vs.85))

[**属性和属性**](/previous-versions/windows/hardware/drivers/ff597900(v=vs.85))

[**WPD 驱动程序概述**](wpd-drivers-overview.md)

 

