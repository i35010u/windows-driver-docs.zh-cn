---
title: INF InterfaceInstall32 节
description: 本部分将创建一个或多个新的设备接口类。
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
ms.openlocfilehash: 8bfef471012a1dd3d67c6318995a3ced70d0b035
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561585"
---
# <a name="inf-interfaceinstall32-section"></a>INF InterfaceInstall32 节


本部分将创建一个或多个新[设备接口类](device-interface-classes.md)。 创建一个新类后，可以注册随后安装的设备/驱动程序支持的新设备接口类，通过使用[ **INF *DDInstall*。接口部分**](inf-ddinstall-interfaces-section.md)在其各自的 INF 文件，或通过调用[ **IoRegisterDeviceInterface**](https://msdn.microsoft.com/library/windows/hardware/ff549506)。

```ini
[InterfaceInstall32]
 
{InterfaceClassGUID}=install-interface-section[,flags]
...
```

## <a name="entries"></a>条目


<a href="" id="interfaceclassguid"></a>*InterfaceClassGUID*  
指定一个 GUID 值，标识新导出[设备接口类](device-interface-classes.md)。

若要注册接口类的实例，在本部分中指定的 GUID 值必须由引用[ **INF AddInterface 指令**](inf-addinterface-directive.md)中[ **INF *DDInstall*。接口部分**](inf-ddinstall-interfaces-section.md)，或新安装的设备驱动程序必须调用其他[ **IoRegisterDeviceInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff549506)具有此 GUID。

有关如何创建 GUID 的详细信息，请参阅[驱动程序中使用 Guid](https://msdn.microsoft.com/library/windows/hardware/ff565392)。 有关系统定义的接口类 GUID，请参阅相应的标头，诸如*Ks.h*内核流式处理接口。

<a href="" id="install-interface-section"></a>*install-interface-section*  
引用 INF 编写器定义部分，也可能包含任何系统定义的扩展，此 INF 中的其他位置。

<a href="" id="flags"></a>*flags*  
如果指定，则此项必须为零。

<a name="remarks"></a>备注
-------

当指定*InterfaceClassGUID*尚未安装在系统中，接口类是否安装了与相应<em>DDInstall</em>**。接口**由处理部分[SetupAPI](setupapi.md)期间设备安装，或者该设备驱动程序时进行首次调用函数**IoRegisterDeviceInterface**.

每个*安装接口部分*名称必须是唯一的 INF 文件中的和必须遵从常规规则，用于定义的节名称。 有关这些规则的详细信息，请参阅[INF 文件的常规语法规则](general-syntax-rules-for-inf-files.md)。

指定任何*安装接口部分*具有以下常规形式：

```ini
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

有关中的条目的详细信息*接口安装部分*，请参阅[ **INF DDInstall 部分**](inf-ddinstall-section.md)。

从 Windows Vista 开始，你可以设置[设备接口类](device-interface-classes.md)通过包括的属性[ **INF AddProperty 指令**](inf-addproperty-directive.md)接口安装部分中。 此外可以删除设备接口类属性，通过包括[ **INF DelProperty 指令**](inf-delproperty-directive.md)接口安装部分中。 但是，应使用**AddProperty**或**DelProperty**指令仅修改不熟悉 Windows Vista 或更高版本的 Windows 操作系统的设备接口类属性。 对于设备接口类属性中引入的 Windows Server 2003、 Windows XP 或 Windows 2000 上且具有相应的注册表值项，应继续使用[ **INF AddReg 指令**](inf-addreg-directive.md)并[ **INF DelReg 指令**](inf-delreg-directive.md)设置和删除设备接口的类属性。 这些准则适用于系统定义的属性和自定义属性。 有关如何使用详细信息**AddProperty**指令并**DelProperty**指令，请参阅[INF AddProperty 指令和 INF DelProperty 指令](using-the-inf-addproperty-directive-and-the-inf-delproperty-directive.md).

**AddReg**指令引用在此接口的安装过程中在注册表中设置特定于设备的接口的信息的一个或多个添加注册表部分。 **HKR**指定在此类添加注册表部分指定 **...DeviceClasses\\{**<em>InterfaceClassGUID</em>**}** 密钥。

有关此接口类的注册表信息应包括至少一个友好名称的新[设备接口类](device-interface-classes.md)和它们打开和使用此接口时更高级的组件需要的任何信息。

此外，此类*安装接口部分*可能会使用任何可选指令如下所示指定特定于接口的安装操作。

有关如何使用系统定义的详细信息 **.nt**， **.ntx86**， **.ntia64**， **.ntamd64**， **.ntarm**， **.ntarm64**扩展，请参阅[创建多个平台和操作系统的 INF 文件](creating-inf-files-for-multiple-platforms-and-operating-systems.md)。

## <a name="see-also"></a>请参阅


[**AddProperty**](inf-addproperty-directive.md)

[**AddReg**](inf-addreg-directive.md)

[**BitReg**](inf-bitreg-directive.md)

[**ClassInstall32**](inf-classinstall32-section.md)

[**CopyFiles**](inf-copyfiles-directive.md)

[***DDInstall***](inf-ddinstall-section.md)

[***DDInstall *。接口**](inf-ddinstall-interfaces-section.md)

[**DelFiles**](inf-delfiles-directive.md)

[**DelProperty**](inf-delproperty-directive.md)

[**DelReg**](inf-delreg-directive.md)

[**Ini2Reg**](inf-ini2reg-directive.md)

[**IoRegisterDeviceInterface**](https://msdn.microsoft.com/library/windows/hardware/ff549506)

[**RenFiles**](inf-renfiles-directive.md)

[**UpdateIniFields**](inf-updateinifields-directive.md)

[**UpdateInis**](inf-updateinis-directive.md)

 

 






