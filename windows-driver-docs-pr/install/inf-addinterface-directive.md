---
title: INF AddInterface 指令
description: 可在 INF DDInstall 部分中指定一个或多个 AddInterface 指令。
ms.assetid: 9bd3e051-51f9-4624-802b-b841b25d6616
keywords:
- INF AddInterface 指令设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF AddInterface Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 595e71bf39b6056442a9421bfefd125d044faa93
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716186"
---
# <a name="inf-addinterface-directive"></a>INF AddInterface 指令


可在[**INF DDInstall 部分**](inf-ddinstall-interfaces-section.md)中指定一个或多个**AddInterface**指令。 此指令将为导出到更高级别的组件（如其他驱动程序或应用程序）的 [设备接口类](./overview-of-device-interface-classes.md) 安装特定于设备的支持。 指令通常引用 *添加接口部分* ，该部分用于设置设备接口类的设备特定实例的注册表信息。

```inf
[DDInstall.Interfaces]
  
AddInterface={InterfaceClassGUID} [,[reference-string] [,[add-interface-section][,flags]]] 
```

导出的设备接口类可以是系统定义的设备接口类之一（如内核流定义的接口类），也可以是由 [**INF InterfaceInstall32 部分**](inf-interfaceinstall32-section.md)指定的新设备接口类。

## <a name="entries"></a>项


<a href="" id="interfaceclassguid"></a>*InterfaceClassGUID*  
指定标识设备接口类的 GUID 值。 这可以表示为以下形式的显式 GUID 值： **{**<em>nnnnnnnn</em>** - ***nnnn*** - *** *-* *** - **nnnn<em>nnnnnnnnnnnn</em>**}** <em>nnnnnnnnnnnn</em>*strkey*<em>nnnnnnnn</em>** - ***nnnn*** - *** *-* ***} - **，或在 INF 文件的[**字符串**](inf-strings-section.md)部分中定义为 **"{** nnnnnnnn nnnn nnnn nnnnnnnnnnnn **}"** 的% strkey% 令牌。

有关如何创建 GUID 的详细信息，请参阅 [在驱动程序中使用 guid](../kernel/using-guids-in-drivers.md)。 对于系统定义的接口类 GUID，请参阅相应的标头，如用于内核流式处理接口 Guid 的*Ks。*

<a href="" id="reference-string"></a>*reference-string*  
与指定接口类的特定于设备的实例关联的此可选值可以表示为 **"**<em>带引号的字符串</em>**"** 或作为[**INF 字符串部分**](inf-strings-section.md)中定义的%*strkey*% 令牌。

PnP 函数和筛选器驱动程序通常会在其 INF 文件中的 **AddInterface =** 条目中省略此值。 *Swenum*驱动程序使用*引用字符串*作为通过使用单个接口类的多个实例按需创建的软件设备的占位符。 可以在具有两个或多个唯一*引用字符串*s 的 INF 条目中指定相同的*InterfaceClassGUID*值。 由于在打开时，i/o 管理器会将 *引用字符串* 值作为接口实例的名称的路径部分进行传递，因此，已安装的驱动程序可以区分单个设备相同类的接口实例。

<a href="" id="add-interface-section"></a>*添加接口部分*  
引用 INF 文件中其他位置的节的名称。 这通常包含一个 [**INF AddReg 指令**](inf-addreg-directive.md) ，用于设置用于导出驱动程序对此 [设备接口类](./overview-of-device-interface-classes.md)的支持的注册表项。 有关详细信息，请参阅下面的 " **备注** " 部分。

<a href="" id="flags"></a>*随意*  
如果指定此项，则此项必须为零。

<a name="remarks"></a>备注
-------

如果尚未安装由指定的 **{**<em>InterfaceClassGUID</em>**}** 标识的[设备接口类](./overview-of-device-interface-classes.md)，系统安装代码会在系统中安装该类。 安装新类的任何 INF 文件还具有一个 [**Inf InterfaceInstall32 部分**](inf-interfaceinstall32-section.md)。 本部分包含指定的 **{**<em>InterfaceClassGUID</em>**}** 并引用 *接口安装部分* ，该部分将为该类设置接口特定的安装操作。

若要启用设备接口类的实例以供更高级组件的运行时使用，则设备驱动程序必须首先调用 [**IoRegisterDeviceInterface**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface) 以检索要启用的设备接口实例的符号链接名称。  通常，PnP 函数或筛选器驱动程序从其 [**AddDevice**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) 例程进行此调用。  若要启用在 inf 中预配的设备接口的实例，设备驱动程序必须在调用[**IoRegisterDeviceInterface**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface)时提供 InterfaceClassGUID 中指定的 **{**<em>InterfaceClassGUID</em>**}** 和*引用字符串*。  然后，驱动程序调用 [**IoSetDeviceInterfaceState**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetdeviceinterfacestate) ，以使用 [**IoRegisterDeviceInterface**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface)返回的符号链接名称启用接口。 

[**Inf DDInstall 部分**](inf-ddinstall-interfaces-section.md)中的每个**AddInterface**指令都可以引用 inf 文件中其他位置的 inf 写入器定义的*添加接口部分*。 每个 INF 写入方定义的部分名称在 INF 文件中必须唯一，并且必须遵循用于定义节名称的常规规则。 有关这些规则的详细信息，请参阅 [INF 文件的一般语法规则](general-syntax-rules-for-inf-files.md)。

**AddInterface**指令引用的*添加接口部分*具有以下格式：

```inf
[add-interface-section]
 
AddReg=add-registry-section[, add-registry-section]...
[AddProperty=add-property-section[, add-property-section] ...]  (Windows Vista and later versions of Windows)
[DelReg=del-registry-section[, del-registry-section] ...]
[DelProperty=del-property-section[, del-property-section] ...]  (Windows Vista and later versions of Windows)
[BitReg=bit-registry-section[,bit-registry-section] ...]
[CopyFiles=@filename | file-list-section[,file-list-section]...]
[DelFiles=file-list-section[,file-list-section]...]
[RenFiles=file-list-section[,file-list-section]...]
[UpdateInis=update-ini-section[, update-ini-section] ...]
[UpdateIniFields=update-inifields-section[, update-inifields-section] ...]
[Ini2Reg=ini-to-registry-section[, ini-to-registry-section] ...]
```

从 Windows Vista 开始，可以通过在添加接口部分中包括 [**INF AddProperty 指令**](inf-addproperty-directive.md) 来设置设备接口属性。 还可以通过在*添加接口部分*中包括[**INF DelProperty 指令**](inf-delproperty-directive.md)来删除设备接口属性。 但是，只应使用 **AddProperty** 或 **DelProperty** 指令来修改对 windows Vista 或更高版本的 windows 操作系统不熟悉的设备接口属性。 对于在 Windows Server 2003、Windows XP 或 Windows 2000 上引入的设备接口属性以及具有相应注册表值条目的设备接口属性，应继续使用 [**Inf AddReg 指令**](inf-addreg-directive.md) 和 [**inf DelReg 指令**](inf-delreg-directive.md) 来设置和删除设备接口属性。 这些准则适用于系统定义的属性和自定义属性。 有关如何使用 **AddProperty** 指令和 **DelProperty** 指令的详细信息，请参阅 [使用 Inf AddProperty 指令和 inf DelProperty 指令](using-the-inf-addproperty-directive-and-the-inf-delproperty-directive.md)。

通常， *添加接口部分* 只包含一个 [**INF AddReg 指令**](inf-addreg-directive.md) ，而后者又引用单个 *添加注册表部分*。 " *外接* 程序" 部分用于在注册表中存储有关设备驱动程序支持的接口的信息，以便以后仍更高级别的驱动程序和应用程序使用。

在*添加接口部分*中引用的*添加注册表部分*特定于设备、驱动程序和接口的实例。 它可能具有定义导出设备接口实例的友好名称的值输入，以便仍更高级的组件可以通过其在用户界面中的友好名称引用该接口。

在此类 "*外接*程序" 部分中指定的**HKR**为设备接口指定运行时可访问状态注册表项。  在运行时，驱动程序可以通过调用 [**IoOpenDeviceInterfaceRegistryKey**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceinterfaceregistrykey) 来检索状态注册表项的句柄，来访问此注册表项中存储的状态。  用户模式组件可以通过调用 [**CM_Open_Device_Interface_Key**](/windows/win32/api/cfgmgr32/nf-cfgmgr32-cm_open_device_interface_keyw)来查询状态。

<a name="examples"></a>示例
--------

此示例演示了 *DDInstall*的一些扩展。支持系统定义的内核流接口的特定音频设备的**接口** 部分。

```inf
; ...
[ESS6881.Device.Interfaces]
AddInterface=%KSCATEGORY_AUDIO%,%KSNAME_Wave%,ESSAud.Interface.Wave
AddInterface=%KSCATEGORY_RENDER%,%KSNAME_Wave%,ESSAud.Interface.Wave
AddInterface=%KSCATEGORY_CAPTURE%,%KSNAME_Wave%,ESSAud.Interface.Wave
AddInterface=%KSCATEGORY_AUDIO%,%KSNAME_Topology%,\
ESSAud.Interface.Topology
AddInterface=%KSCATEGORY_AUDIO%,%KSNAME_UART%,WDM.Interface.UART
AddInterface=%KSCATEGORY_RENDER%,%KSNAME_UART%,WDM.Interface.UART
AddInterface=%KSCATEGORY_CAPTURE%,%KSNAME_UART%,WDM.Interface.UART
AddInterface=%KSCATEGORY_AUDIO%,%KSNAME_FMSynth%,WDM.Interface.FMSynth
AddInterface=%KSCATEGORY_RENDER%,%KSNAME_FMSynth%,\
WDM.Interface.FMSynth

[ESSAud.Interface.Wave]
AddReg=ESSAud.Interface.Wave.AddReg

[ESSAud.Interface.Wave.AddReg]
HKR,,CLSID,,%Proxy.CLSID%
HKR,,FriendlyName,,%ESSAud.Wave.szPname%
; ... 
[WDM.Interface.UART]
AddReg=WDM.Interface.UART.AddReg

[WDM.Interface.UART.AddReg]
HKR,,CLSID,,%Proxy.CLSID%
HKR,,FriendlyName,,%WDM.UART.szPname%
; ...
[Strings]
KSCATEGORY_AUDIO="{6994ad04-93ef-11d0-a3cc-00a0c9223196}"
KSCATEGORY_RENDER="{65e8773e-8f56-11d0-a3b9-00a0c9223196}"
KSCATEGORY_CAPTURE="{65e8773d-8f56-11d0-a3b9-00a0c9223196}"
; ...
KSNAME_WAVE="Wave"
KSNAME_UART="UART"
; ...
Proxy.CLSID="{17cca71b-ecd7-11d0-b908-00a0c9223196}"
; ... 
ESSAud.Wave.szPname="ESS AudioDrive" 
; ... 
```

## <a name="see-also"></a>请参阅


[**AddProperty**](inf-addproperty-directive.md)

[**AddReg**](inf-addreg-directive.md)

[**BitReg**](inf-bitreg-directive.md)

[**CopyFiles**](inf-copyfiles-directive.md)

[***DDInstall*.接口**](inf-ddinstall-interfaces-section.md)

[**DelFiles**](inf-delfiles-directive.md)

[**DelProperty**](inf-delproperty-directive.md)

[**DelReg**](inf-delreg-directive.md)

[**Ini2Reg**](inf-ini2reg-directive.md)

[**InterfaceInstall32**](inf-interfaceinstall32-section.md)

[**IoRegisterDeviceInterface**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface)

[**IoSetDeviceInterfaceState**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetdeviceinterfacestate)

[**RenFiles**](inf-renfiles-directive.md)

[**UpdateIniFields**](inf-updateinifields-directive.md)

[**UpdateInis**](inf-updateinis-directive.md)

 

