---
title: 检索设备关系
description: 检索设备关系
ms.assetid: 2b0ead69-1fda-4024-a7c2-d6350060b5fb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e9c49578c327e10ce8f8c404f3dbb49d1f8b03a
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715092"
---
# <a name="retrieving-device-relations"></a>检索设备关系


在 Windows Vista 和更高版本的 Windows 中， [统一设备属性模型](unified-device-property-model--windows-vista-and-later-.md) 包括 [设备关系属性](/previous-versions/ff541498(v=vs.85))。 统一设备属性模型使用 [属性键](property-keys.md) 来表示这些属性。

Windows Server 2003、Windows XP 和 Windows 2000 不支持统一属性模型的属性键，也不支持表示这些属性的相应注册表项值。 不过，你可以通过调用即插即用 (PnP) 配置管理器功能来检索相应的信息。 为了保持与早期 Windows 版本的兼容性，Windows Vista 及更高版本还支持调用 PnP 配置管理器功能来检索设备关系属性。 但是，您应该使用统一设备属性模型的属性键来访问设备关系属性。

有关如何使用属性键访问设备驱动程序属性的信息，请参阅 [访问 Windows Vista 和更高版本的设备实例属性 () ](accessing-device-instance-properties--windows-vista-and-later-.md)。

有关如何在 Windows Server 2003、Windows XP 和 Windows 2000 上访问设备关系属性的信息，请参阅以下主题：

[检索弹出关系、删除关系、电源关系和总线关系](#retrieving-ejection-relations--removal-relations--and-power-relations-)

[检索设备实例的父项](#retrieving-the-parent-of-a-device-inst)

[检索设备实例的子级](#retrieving-the-children-of-a-device-inst)

[检索设备实例的同级](#retrieving-the-siblings-of-a-device-inst)

### <a name="retrieving-ejection-relations-removal-relations-and-power-relations-and-bus-relations"></a><a href="" id="retrieving-ejection-relations--removal-relations--and-power-relations-"></a> 检索弹出关系、删除关系、电源关系和总线关系

若要在 Windows Server 2003、Windows XP 和 Windows 2000 上检索设备关系信息，请调用 **CM_Get_Device_ID_List** 并提供以下参数值：

-   将 *pszFilter* 设置为指向以 NULL 结尾的字符串的指针，该字符串指定要为其检索关系信息的设备实例标识符。

-   将 *缓冲区* 设置为指向缓冲区的指针，该缓冲区接收以 NULL 结尾的设备实例标识符的列表。 此列表以其他 NULL 字符结尾。 可以通过调用 **CM_Get_Device_ID_List_Size** 函数获取所需的缓冲区大小。

-   将 *BufferLen* 设置为 *缓冲区* 缓冲区的大小（以字符为字符）。

-   将 *ulFlags* 设置为以下标志之一，以检索相应的关系信息：
    -   CM_GETIDLIST_FILTER_EJECTIONRELATIONS

        CM_GETIDLIST_FILTER_EJECTIONRELATIONS 标志检索 [**弹出关系**](../kernel/irp-mn-query-device-relations.md)，这与 Windows Vista 和更高版本中 [**DEVPKEY_Device_EjectionRelations**](./devpkey-device-ejectionrelations.md) 设备属性提供的信息相同。

    -   CM_GETIDLIST_FILTER_REMOVALRELATIONS

        CM_GETIDLIST_FILTER_REMOVALRELATIONS 标志检索 [**删除关系**](../kernel/irp-mn-query-device-relations.md)，这与 Windows Vista 和更高版本中 [**DEVPKEY_Device_RemovalRelations**](./devpkey-device-removalrelations.md) 设备属性提供的信息相同。

    -   CM_GETIDLIST_FILTER_POWERRELATIONS

        CM_GETIDLIST_FILTER_POWERRELATIONS 标志检索电源关系，它与 Windows Vista 和更高版本中 [**DEVPKEY_Device_PowerRelations**](./devpkey-device-powerrelations.md) 设备属性提供的信息相同。

    -   CM_GETIDLIST_FILTER_BUSRELATIONS

        CM_GETIDLIST_FILTER_BUSRELATIONS 标志检索 [**总线关系**](../kernel/irp-mn-query-device-relations.md)，这与 Windows Vista 和更高版本中 [**DEVPKEY_Device_BusRelations**](./devpkey-device-busrelations.md) 设备属性提供的信息相同。

如果对 **CM_Get_Device_ID_List** 的调用成功，则 **CM_Get_Device_ID_List** 检索请求的关系信息并返回 CR_SUCCESS。 否则， **CM_Get_Device_ID_List** 将返回一个错误代码，其中包含 *Cfgmgr32*中定义的前缀 "CR_"。

### <a name="retrieving-the-parent-of-a-device-instance"></a><a href="" id="retrieving-the-parent-of-a-device-inst"></a> 检索设备实例的父项

若要在 Windows Server 2003、Windows XP 和 Windows 2000 上检索父设备的设备实例标识符，请执行以下步骤：

1.  调用 [**CM_Get_Parent**](/windows/win32/api/cfgmgr32/nf-cfgmgr32-cm_get_parent) 函数可检索设备实例的父设备的设备实例句柄。

2.  调用 [**CM_Get_Device_ID**](/windows/win32/api/cfgmgr32/nf-cfgmgr32-cm_get_device_idw) 检索与由先前对 **CM_Get_Parent**的调用检索到的父设备的设备实例句柄关联的设备实例标识符。

使用此过程检索到的信息与 Windows Vista 和更高版本的统一设备属性模型中的 DEVPKEY_Device_Parent 属性表示的信息相同。

### <a name="retrieving-the-children-of-a-device-instance"></a><a href="" id="retrieving-the-children-of-a-device-inst"></a>检索设备实例的子级

若要检索 Windows Server 2003、Windows XP 和 Windows 2000 上的设备实例的子设备的设备实例标识符，请执行以下步骤：

1.  调用 [**CM_Get_Child**](/windows/win32/api/cfgmgr32/nf-cfgmgr32-cm_get_child) 函数检索与设备实例关联的第一个子设备的设备实例句柄。

2.  调用 [**CM_Get_Sibling**](/windows/win32/api/cfgmgr32/nf-cfgmgr32-cm_get_sibling) 多次，因为需要枚举通过调用 **CM_Get_Child**检索到的第一个子设备的所有同级设备。

3.  调用 **CM_Get_Device_ID** 检索与 **CM_Get_Child** 和 **CM_Get_Sibling**的调用返回的设备实例句柄关联的设备实例标识符。

使用此过程检索到的信息与 Windows Vista 和更高版本的统一设备属性模型中的 DEVPKEY_Device_Children 属性表示的信息相同。

### <a name="retrieving-the-siblings-of-a-device-instance"></a><a href="" id="retrieving-the-siblings-of-a-device-inst"></a>检索设备实例的同级

若要检索 Windows Server 2003、Windows XP 和 Windows 2000 上 device instance Abc 设备的设备实例标识符，请执行以下步骤：

1.  调用 [**CM_Get_Parent**](/windows/win32/api/cfgmgr32/nf-cfgmgr32-cm_get_parent) 函数检索设备实例 *Abc*的父设备的设备实例句柄。

2.  调用 [**CM_Get_Child**](/windows/win32/api/cfgmgr32/nf-cfgmgr32-cm_get_child) 函数可检索设备实例 *Abc*的父设备的第一个子设备的设备实例句柄。

3.  根据需要调用 [**CM_Get_Sibling**](/windows/win32/api/cfgmgr32/nf-cfgmgr32-cm_get_sibling) 多次，以枚举父设备的第一个子设备的所有同级设备。 此枚举还将返回设备实例 *Abc*的句柄。

4.  调用 [**CM_Get_Device_ID**](/windows/win32/api/cfgmgr32/nf-cfgmgr32-cm_get_device_idw) 检索与之前对 **CM_Get_Sibling**的调用返回的设备实例句柄关联的设备实例标识符。 从父设备的第一个子设备的同级设备列表中删除 device instance *Abc* 的句柄。

使用此过程检索到的信息与 Windows Vista 和更高版本的统一设备属性模型中的 DEVPKEY_Device_Siblings 属性表示的信息相同。 如果此部分中列出的**CM_<em>Xxx</em> **函数调用成功，则**CM_<em>Xxx</em> **函数将检索请求的信息并返回 CR_SUCCESS。 否则， **CM_<em>Xxx</em> **函数返回一个错误代码，其中包含*Cfgmgr32*中定义的前缀 "CR_"。

 

