---
title: INF AddInterface 指令
description: INF DDInstall.Interfaces 部分中，可以指定一个或多个 AddInterface 指令。
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
ms.openlocfilehash: e9edcdba0c1ee776f8613b3c151f6b79337957ab
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385924"
---
# <a name="inf-addinterface-directive"></a>INF AddInterface 指令


一个或多个**AddInterface**内，可以指定指令[ **INF DDInstall.Interfaces 部分**](inf-ddinstall-interfaces-section.md)。 此指令将安装对特定于设备的支持[设备接口类](device-interface-classes.md)导出到更高级的组件，如其他驱动程序或应用程序。 通常，该指令引用*添加接口部分*，这将设置设备接口类的特定于设备的实例的注册表信息。

```ini
[DDInstall.Interfaces]
  
AddInterface={InterfaceClassGUID} [,[reference-string] [,[add-interface-section][,flags]]] 
```

导出的设备接口类可以是一个系统定义的设备接口类，例如那些由内核流式处理，或通过指定了一个新的设备接口类[ **INF InterfaceInstall32 部分**](inf-interfaceinstall32-section.md).

## <a name="entries"></a>条目


<a href="" id="interfaceclassguid"></a>*InterfaceClassGUID*  
指定标识设备接口类的 GUID 值。 这可以表示为一个显式的 GUID 值的窗体 **{** <em>nnnnnnnn</em> **-***nnnn***-***nnnn *-* nnnn***-** <em>nnnnnnnnnnnn</em> **}** 或作为 %*strkey*%令牌到定义 **"{** <em>nnnnnnnn</em> **-***nnnn***-***nnnn *-* nnnn***-** <em>nnnnnnnnnnnn</em> **}"** 中[**字符串**](inf-strings-section.md) INF 文件部分。

有关如何创建 GUID 的详细信息，请参阅[驱动程序中使用 Guid](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-guids-in-drivers)。 有关系统定义的接口类 GUID，请参阅相应的标头，诸如*Ks.h*内核流接口的 Guid。

<a href="" id="reference-string"></a>*reference-string*  
此可选值，与特定于设备的类的实例指定的接口，关联可以表示为 **"** <em>带引号的字符串</em> **"** 或作为 %*strkey*中定义的 %令牌[ **INF 字符串部分**](inf-strings-section.md)。

即插即用的函数和筛选器驱动程序通常省略此值从**AddInterface =** 其 INF 文件中的条目。 一个*引用字符串*由*swenum*驱动程序，因为软件通过使用单个接口类的多个实例创建按需的设备的占位符。 相同*InterfaceClassGUID*值可以是具有两个 INF 条目中指定或多个唯一*引用字符串*s。 因为 I/O 管理器将传递*引用字符串*作为路径组件的接口实例的名称，只要打开它的值，已安装的驱动程序可以区分的同一个类的一个接口实例设备。

<a href="" id="add-interface-section"></a>*add-interface-section*  
引用其他位置中的 INF 文件节的名称。 这通常包含[ **INF AddReg 指令**](inf-addreg-directive.md)若要将导出的驱动程序支持的注册表项设置[设备接口类](device-interface-classes.md)。 有关详细信息，请参阅以下**备注**部分。

<a href="" id="flags"></a>*flags*  
如果指定，则此项必须为零。

<a name="remarks"></a>备注
-------

如果[设备接口类](device-interface-classes.md)通过指定标识 **{** <em>InterfaceClassGUID</em> **}** 是未安装，请在系统设置代码在系统中安装此类。 任何 INF 文件来安装一个新类还具有[ **INF InterfaceInstall32 部分**](inf-interfaceinstall32-section.md)。 本部分包含指定 **{** <em>InterfaceClassGUID</em> **}** 并引用*接口安装部分*的设置此类的特定于接口的安装操作。

若要启用更高级的组件运行时使用的设备接口类的实例，请将设备驱动程序必须先调用[ **IoRegisterDeviceInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioregisterdeviceinterface)要检索的符号链接名称若要启用的设备接口实例。  通常情况下，即插即用的函数或筛选器驱动程序，可以从此调用其[ **AddDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)例程。  若要启用 INF 中预配的设备接口的实例，该设备驱动程序必须提供 **{** <em>InterfaceClassGUID</em> **}** 和*引用字符串*时，它调用 INF 中指定[ **IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioregisterdeviceinterface)。  然后，该驱动程序调用[ **IoSetDeviceInterfaceState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetdeviceinterfacestate)若要启用使用返回的符号链接名称的接口[ **IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioregisterdeviceinterface). 

每个**AddInterface**指令[ **INF DDInstall.Interfaces 部分**](inf-ddinstall-interfaces-section.md) INF 编写器的定义可以引用*添加-接口-部分* INF 文件中的其他位置。 每个 INF 编写器定义的节名称必须是唯一的 INF 文件中的和必须遵从常规规则，用于定义的节名称。 有关这些规则的详细信息，请参阅[INF 文件的常规语法规则](general-syntax-rules-for-inf-files.md)。

*添加接口部分*所引用的**AddInterface**指令具有以下形式：

```ini
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

从 Windows Vista 开始，你可以通过包含设置设备接口的属性[ **INF AddProperty 指令**](inf-addproperty-directive.md)添加接口部分中。 此外可以通过包括删除设备接口属性[ **INF DelProperty 指令**](inf-delproperty-directive.md)中*添加接口部分*。 但是，应使用**AddProperty**或**DelProperty**指令仅以修改设备接口属性的新 Windows Vista 或更高版本的 Windows 操作系统。 对于设备接口属性中引入的 Windows Server 2003、 Windows XP 或 Windows 2000 上且具有相应的注册表值项，应继续使用[ **INF AddReg 指令**](inf-addreg-directive.md)并[ **INF DelReg 指令**](inf-delreg-directive.md)设置和删除设备接口属性。 这些准则适用于系统定义的属性和自定义属性。 有关如何使用详细信息**AddProperty**指令并**DelProperty**指令，请参阅[INF AddProperty 指令和 INF DelProperty 指令](using-the-inf-addproperty-directive-and-the-inf-delproperty-directive.md).

通常情况下，*添加接口部分*仅包含[ **INF AddReg 指令**](inf-addreg-directive.md) ，反过来，引用单个*将添加的注册表-部分*. *添加注册表部分*用于存储有关设备驱动程序供后续使用的主管更高级别驱动程序和应用程序支持的接口注册表中的信息。

*添加注册表部分*内引用*添加接口部分*是特定于设备、 驱动程序和接口的实例。 它可能具有值项定义导出的设备接口实例的友好名称，以便仍然更高级的组件可以引用该接口由其用户界面中的友好名称。

**HKR**中此类指定*添加注册表部分*部分指定设备接口的运行时可访问状态注册表项。  该驱动程序可以访问存储在此注册表项在运行时通过调用状态[ **IoOpenDeviceInterfaceRegistryKey** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioopendeviceinterfaceregistrykey)要检索的句柄状态注册表项。  用户模式组件可以通过调用查询的状态[ **CM_Open_Device_Interface_Key**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_open_device_interface_keyw)。

<a name="examples"></a>示例
--------

此示例显示了一些扩展*DDInstall*。**接口**支持系统定义内核流式处理接口的特定音频设备的部分。

```ini
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

[***DDInstall *。接口**](inf-ddinstall-interfaces-section.md)

[**DelFiles**](inf-delfiles-directive.md)

[**DelProperty**](inf-delproperty-directive.md)

[**DelReg**](inf-delreg-directive.md)

[**Ini2Reg**](inf-ini2reg-directive.md)

[**InterfaceInstall32**](inf-interfaceinstall32-section.md)

[**IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioregisterdeviceinterface)

[**IoSetDeviceInterfaceState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetdeviceinterfacestate)

[**RenFiles**](inf-renfiles-directive.md)

[**UpdateIniFields**](inf-updateinifields-directive.md)

[**UpdateInis**](inf-updateinis-directive.md)

 

 






