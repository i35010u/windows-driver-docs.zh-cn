---
title: 检索设备的关系
description: 检索设备的关系
ms.assetid: 2b0ead69-1fda-4024-a7c2-d6350060b5fb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47f51fbb5d270610e2cbc83ffcdfb36e8ac788de
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526156"
---
# <a name="retrieving-device-relations"></a>检索设备的关系


在 Windows Vista 和更高版本的 Windows，[统一的设备属性模型](unified-device-property-model--windows-vista-and-later-.md)包括[设备的关系属性](https://msdn.microsoft.com/library/windows/hardware/ff541498)。 统一的设备属性模型使用[属性键](property-keys.md)来表示这些属性。

Windows Server 2003、 Windows XP 和 Windows 2000 不支持属性键的属性的统一的模型，也不支持表示这些属性的相应注册表项值。 但是，您可以通过调用插即用 (PnP) 配置管理器函数来检索相应信息。 为了保持与早期 Windows 版本的兼容性，Windows Vista 和更高版本还支持调用即插即用的配置管理器函数来检索设备的关系属性。 但是，应使用统一的设备属性模型属性键来访问设备的关系属性。

有关如何使用属性键来访问设备驱动程序属性的信息，请参阅[访问设备实例属性 （Windows Vista 和更高版本）](accessing-device-instance-properties--windows-vista-and-later-.md)。

有关如何访问 Windows Server 2003、 Windows XP 和 Windows 2000 上的设备的关系属性的信息，请参阅以下主题：

[检索弹出关系、 删除关系和电源关系和总线关系](#retrieving-ejection-relations--removal-relations--and-power-relations-)

[检索设备实例的父级](#retrieving-the-parent-of-a-device-inst)

[检索设备实例的子级](#retrieving-the-children-of-a-device-inst)

[检索设备实例的同级](#retrieving-the-siblings-of-a-device-inst)

### <a href="" id="retrieving-ejection-relations--removal-relations--and-power-relations-"></a> 检索弹出关系、 删除关系和电源关系和总线关系

若要检索在 Windows Server 2003、 Windows XP 和 Windows 2000 上的设备的关系信息，请调用**CM_Get_Device_ID_List**并提供以下参数值：

-   设置*pszFilter*为指向一个以 NULL 结尾的字符串，指定要为其检索关系信息的设备实例标识符。

-   设置*缓冲区*为指向该缓冲区用于接收的以 NULL 结尾的设备实例标识符的列表。 由其他的 NULL 字符终止列表。 可以通过调用获取所需的缓冲区大小**CM_Get_Device_ID_List_Size**函数。

-   设置*BufferLen*大小，以字符为单位的*缓冲区*缓冲区。

-   设置*ulFlags*要检索的相应关系信息的以下标志之一：
    -   CM_GETIDLIST_FILTER_EJECTIONRELATIONS

        CM_GETIDLIST_FILTER_EJECTIONRELATIONS 标记检索[**弹出关系**](https://msdn.microsoft.com/library/windows/hardware/ff551670)，这是由提供的相同信息[ **DEVPKEY_Device_EjectionRelations** ](https://msdn.microsoft.com/library/windows/hardware/ff542482) Windows Vista 和更高版本中的设备属性。

    -   CM_GETIDLIST_FILTER_REMOVALRELATIONS

        CM_GETIDLIST_FILTER_REMOVALRELATIONS 标记检索[**删除关系**](https://msdn.microsoft.com/library/windows/hardware/ff551670)，这是由提供的相同信息[ **DEVPKEY_Device_RemovalRelations** ](https://msdn.microsoft.com/library/windows/hardware/ff542614) Windows Vista 和更高版本中的设备属性。

    -   CM_GETIDLIST_FILTER_POWERRELATIONS

        CM_GETIDLIST_FILTER_POWERRELATIONS 标志检索 power 关系，这是由提供的相同信息[ **DEVPKEY_Device_PowerRelations** ](https://msdn.microsoft.com/library/windows/hardware/ff542588) Windows Vista 中的设备属性和更高版本。

    -   CM_GETIDLIST_FILTER_BUSRELATIONS

        CM_GETIDLIST_FILTER_BUSRELATIONS 标记检索[**总线关系**](https://msdn.microsoft.com/library/windows/hardware/ff551670)，这是由提供的相同信息[ **DEVPKEY_Device_BusRelations**](https://msdn.microsoft.com/library/windows/hardware/ff542368) Windows Vista 和更高版本中的设备属性。

如果在调用**CM_Get_Device_ID_List**成功， **CM_Get_Device_ID_List**检索请求的关系信息，并返回 CR_SUCCESS。 否则为**CM_Get_Device_ID_List**返回一个具有前缀"CR_"中定义的错误代码*Cfgmgr32.h*。

### <a href="" id="retrieving-the-parent-of-a-device-inst"></a> 检索设备实例的父级

若要检索的 Windows Server 2003、 Windows XP 和 Windows 2000 上的父设备的设备实例标识符，请按照下列步骤：

1.  调用[ **CM_Get_Parent** ](https://msdn.microsoft.com/library/windows/hardware/ff538610)函数以检索设备实例的父设备的设备实例句柄。

2.  调用[ **CM_Get_Device_ID** ](https://msdn.microsoft.com/library/windows/hardware/ff538405)可检索与通过以前调用检索到的父设备的设备实例句柄相关联的设备实例标识符**CM_Get_Parent**。

使用此过程来检索此信息是由 Windows Vista 和更高版本的统一的设备属性模型中的 DEVPKEY_Device_Parent 属性相同。

### <a href="" id="retrieving-the-children-of-a-device-inst"></a>检索设备实例的子级

若要检索的 Windows Server 2003、 Windows XP 和 Windows 2000 上的设备实例的子设备的设备实例标识符，请按照下列步骤：

1.  调用[ **CM_Get_Child** ](https://msdn.microsoft.com/library/windows/hardware/ff538074)函数以检索与设备实例相关联的第一个子设备的设备实例句柄。

2.  调用[ **CM_Get_Sibling** ](https://msdn.microsoft.com/library/windows/hardware/ff538674)多次按需枚举通过调用检索到的第一个子设备的所有同级设备**CM_Get_Child**。

3.  调用**CM_Get_Device_ID**来检索与已返回到调用的设备实例句柄相关联的设备实例标识符**CM_Get_Child**和**CM_Get_同级**。

使用此过程来检索此信息是由 Windows Vista 和更高版本的统一的设备属性模型中的 DEVPKEY_Device_Children 属性相同。

### <a href="" id="retrieving-the-siblings-of-a-device-inst"></a>检索设备实例的同级

若要检索的设备实例在 Windows Server 2003、 Windows XP 和 Windows 2000 的 Abc 的同级设备的设备实例标识符，请按照下列步骤：

1.  调用[ **CM_Get_Parent** ](https://msdn.microsoft.com/library/windows/hardware/ff538610)函数可检索的设备实例句柄的父设备的设备实例*Abc*。

2.  调用[ **CM_Get_Child** ](https://msdn.microsoft.com/library/windows/hardware/ff538074)函数可检索的设备实例句柄的父设备的设备实例的第一个子设备*Abc*。

3.  调用[ **CM_Get_Sibling** ](https://msdn.microsoft.com/library/windows/hardware/ff538674)多次按需枚举父设备的第一个子设备的所有同级设备。 此枚举还将向设备实例返回一个句柄*Abc*。

4.  调用[ **CM_Get_Device_ID** ](https://msdn.microsoft.com/library/windows/hardware/ff538405)来检索与已由以前调用的返回设备实例句柄相关联的设备实例标识符**CM_Get_Sibling**. 删除设备实例的句柄*Abc*从同级的父设备的第一个子设备的设备的列表。

使用此过程来检索到的信息是由 Windows Vista 和更高版本的统一的设备属性模型中的 DEVPKEY_Device_Siblings 属性相同。 如果**CM_ * Xxx*** 本部分中列出的函数调用成功， **CM_ * Xxx*** 函数检索所需的信息，并返回 CR_SUCCESS。 否则为**CM_ * Xxx*** 函数返回一个具有前缀"CR_"中定义的错误代码*Cfgmgr32.h*。

 

 





