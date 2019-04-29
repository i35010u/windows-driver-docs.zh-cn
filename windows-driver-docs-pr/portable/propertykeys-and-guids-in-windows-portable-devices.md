---
Description: Windows 便携设备中的 PROPERTYKEY 和 GUID
title: Windows 便携设备中的 PROPERTYKEY 和 GUID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba408fa498b0e543d8de61c16571e77d86ee9c69
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376231"
---
# <a name="propertykeys-and-guids-in-windows-portable-devices"></a>Windows 便携设备中的 PROPERTYKEY 和 GUID


由标识的属性或命令**PROPERTYKEY**结构。 一个**PROPERTYKEY**结构由两部分组成： 一个 GUID ( *fmtid*成员) 和一个 dword 值 ( *pid*成员)。 GUID 部分用于指示该属性的类别或命令都属于 (即，相关的属性属于同一类别和相关的命令属于同一类别; 因此，它们将具有相同*fmtid*)。 DWORD 部分表示的属性或命令的 ID，和用于区分单个属性或命令类别中的命令 (即*pid*属性或在同一类别中的命令的值将为不同）。

本文档的参考部分描述了由 WPD 定义的所有 PROPERTYKEY 值。 这些值对应于命令、 属性和资源。 如果创建自定义 PROPERTYKEY 值，则应定义一个新的 GUID 类别;WPD GUID 值或您与现有和未来 WPD 指定 PROPERTYKEYs 冲突的风险，不要重复使用。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[**WPD\_内容\_类型\_功能\_对象**](https://msdn.microsoft.com/library/windows/hardware/ff597845)

[**对于对象的要求**](requirements-for-objects.md)

[**对象格式 Guid**](https://msdn.microsoft.com/library/windows/hardware/ff597651)

[**对资源的要求**](https://msdn.microsoft.com/library/windows/hardware/ff597663)

[**命令**](https://msdn.microsoft.com/library/windows/hardware/ff597554)

[**属性和特性**](https://msdn.microsoft.com/library/windows/hardware/ff597900)

[**WPD 驱动程序概述**](wpd-drivers-overview.md)

 

 





