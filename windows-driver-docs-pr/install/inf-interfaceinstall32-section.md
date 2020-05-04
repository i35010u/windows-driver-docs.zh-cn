---
title: INF InterfaceInstall32 节
description: 本部分创建一个或多个新的设备接口类。
ms.assetid: 7cd576a7-aa5b-486c-a622-cdcb9e7448b5
keywords:
- INF InterfaceInstall32 部分设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF InterfaceInstall32 Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: df390106f4f2ecd3246e41072553b6902ad28345
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223283"
---
# <a name="inf-interfaceinstall32-section"></a>INF InterfaceInstall32 节


本部分创建一个或多个新的[设备接口类](device-interface-classes.md)。 创建新类后，可以使用 INF DDInstall 注册以后安装的设备/驱动程序，以支持新的设备接口[**类*DDInstall*。**](inf-ddinstall-interfaces-section.md)在各自的 INF 文件中或通过调用[**IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface)的接口部分。

```inf
[InterfaceInstall32]
 
{InterfaceClassGUID}=install-interface-section[,flags]
...
```

## <a name="entries"></a>条目


<a href="" id="interfaceclassguid"></a>*InterfaceClassGUID*  
指定标识新导出[设备接口类](device-interface-classes.md)的 GUID 值。

若要注册 interface 类的实例，必须由 Inf DDInstall 中的[**Inf AddInterface 指令**](inf-addinterface-directive.md)引用此部分中的指定 GUID 值[** *DDInstall*。接口 "部分**](inf-ddinstall-interfaces-section.md)，或者新安装的设备的驱动程序必须通过此 GUID 调用[**IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface) 。

有关如何创建 GUID 的详细信息，请参阅[在驱动程序中使用 guid](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-guids-in-drivers)。 对于系统定义的接口类 GUID，请参阅相应的标头，如用于内核流式处理接口的*Ks。*

<a href="" id="install-interface-section"></a>*安装界面-部分*  
引用一个 INF 写入器定义的部分，该部分可能包含此 INF 中其他任何系统定义的扩展。

<a href="" id="flags"></a>*随意*  
如果指定此项，则此项必须为零。

<a name="remarks"></a>备注
-------

如果系统中尚未安装指定的*InterfaceClassGUID* ，则会将该接口类安装为相应的<em>DDInstall</em>**。接口**部分在设备安装过程中或设备的驱动程序对**IoRegisterDeviceInterface**进行初始调用时由[setupapi.log](setupapi.md)函数进行处理。

每个*安装接口节*名称在 INF 文件中必须唯一，并且必须遵循用于定义节名称的常规规则。 有关这些规则的详细信息，请参阅[INF 文件的一般语法规则](general-syntax-rules-for-inf-files.md)。

任何指定的*安装界面部分*都具有以下通用格式：

```inf
[interface-install-section] | 
[interface-install-section.nt] | 
[interface-install-section.ntx86] | 
[interface-install-section.ntia64] | (Windows XP and later versions of Windows)
[interface-install-section.ntamd64] (Windows XP and later versions of Windows)
[interface-install-section.ntarm] (Windows 8 and later versions of Windows)
[interface-install-section.ntarm64] (Windows 10 and later versions of Windows)


 
AddReg=add-registry-section[, add-registry-section] ...
[AddProperty=add-property-section[, add-property-section] ...]  (Windows Vista and later versions of Windows)
[Copyfiles=@filename | file-list-section[, file-list-section] ...]
[DelReg=del-registry-section[, del-registry-section] ...]
[DelProperty=del-property-section[, del-property-section] ...]  (Windows Vista and later versions of Windows)
[BitReg=bit-registry-section[,bit-registry-section]...]
[Delfiles=file-list section[, file-list-section] ...]
[Renfiles=file-list-section[, file-list-section] ...]
[UpdateInis=update-ini-section[,update-ini-section]...]
[UpdateIniFields=update-inifields-section[,update-inifields-section]...]
[Ini2Reg=ini-to-registry-section[,ini-to-registry-section]...]
...
```

有关*接口安装部分*中条目的详细信息，请参阅[**INF DDInstall 部分**](inf-ddinstall-section.md)。

从 Windows Vista 开始，可以通过在接口安装部分中包括[**INF AddProperty 指令**](inf-addproperty-directive.md)来设置[设备接口类](device-interface-classes.md)属性。 还可以通过在接口安装部分中包含[**INF DelProperty 指令**](inf-delproperty-directive.md)来删除设备接口类属性。 但是，只应使用**AddProperty**或**DelProperty**指令来修改 windows Vista 或更高版本的 windows 操作系统的新设备接口类属性。 对于在 Windows Server 2003、Windows XP 或 Windows 2000 上引入的设备接口类属性以及具有相应注册表值条目的设备接口类属性，应继续使用[**Inf AddReg 指令**](inf-addreg-directive.md)和[**inf DelReg 指令**](inf-delreg-directive.md)来设置和删除设备接口类属性。 这些准则适用于系统定义的属性和自定义属性。 有关如何使用**AddProperty**指令和**DelProperty**指令的详细信息，请参阅[使用 Inf AddProperty 指令和 inf DelProperty 指令](using-the-inf-addproperty-directive-and-the-inf-delproperty-directive.md)。

**AddReg**指令将引用一个或多个在安装此接口的过程中设置注册表中特定于设备接口的信息的添加注册表部分。 在此类 "外接程序" 部分中指定的**HKR**指定 **。DeviceClasses\\{**<em>InterfaceClassGUID</em>**}** 键。

有关此接口类的注册表信息应该至少包含新[设备接口类](device-interface-classes.md)的友好名称，以及打开和使用此接口时更高级别组件所需的任何信息。

此外，此类*安装界面部分*可能会使用此处所示的任何可选指令来指定接口特定的安装操作。

若要详细了解如何使用**系统定义的** **ntx86**、 **ntia64**、 **ntamd64**、 **Ntarm**、 **Ntarm64**扩展，请参阅[为多个平台和操作系统创建 INF 文件](creating-inf-files-for-multiple-platforms-and-operating-systems.md)。

## <a name="see-also"></a>另请参阅


[**AddProperty**](inf-addproperty-directive.md)

[**AddReg**](inf-addreg-directive.md)

[**BitReg**](inf-bitreg-directive.md)

[**ClassInstall32**](inf-classinstall32-section.md)

[**CopyFiles**](inf-copyfiles-directive.md)

[***DDInstall***](inf-ddinstall-section.md)

[***DDInstall*.接口**](inf-ddinstall-interfaces-section.md)

[**DelFiles**](inf-delfiles-directive.md)

[**DelProperty**](inf-delproperty-directive.md)

[**DelReg**](inf-delreg-directive.md)

[**Ini2Reg**](inf-ini2reg-directive.md)

[**IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface)

[**RenFiles**](inf-renfiles-directive.md)

[**UpdateIniFields**](inf-updateinifields-directive.md)

[**UpdateInis**](inf-updateinis-directive.md)

 

 






