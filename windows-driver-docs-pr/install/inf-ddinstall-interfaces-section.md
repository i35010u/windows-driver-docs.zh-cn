---
title: INF DDInstall.Interfaces 节
description: 根据特定设备/驱动程序支持的设备接口数量，每个模型的 DDInstall 部分可以具有一个或多个 AddInterface 指令。
ms.assetid: 16904119-00a4-45d7-a32e-24ba4c8a3416
keywords:
- INF DDInstall 设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF DDInstall.Interfaces Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5600f34c5dde18bed03ea1b4bb5a3bee0091b6b
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223241"
---
# <a name="inf-ddinstallinterfaces-section"></a>INF DDInstall.Interfaces 节


每个模型<em>DDInstall</em>**。接口**部分可以具有一个或多个[**AddInterface**](inf-addinterface-directive.md)指令，具体取决于特定设备/驱动程序支持的设备接口数量。

```inf
[install-section-name.Interfaces] |
[install-section-name.nt.Interfaces] | 
[install-section-name.ntx86.Interfaces] |
[install-section-name.ntarm.Interfaces] | (Windows 8 and later versions of Windows)
[install-section-name.ntarm64.Interfaces] | (Windows 10 version 1709 and later versions of Windows)
[install-section-name.ntia64.Interfaces] |  (Windows XP and later versions of Windows)
[install-section-name.ntamd64.Interfaces]  (Windows XP and later versions of Windows)
 
AddInterface={InterfaceClassGUID} [, [reference string] [,[add-interface-section] [,flags]]] ...
[Include=filename.inf[,filename2.inf]...]
[Needs=inf-section-name[,inf-section-name]...] 
```

若要支持现有设备接口（如任何系统预定义内核流式处理接口），请在此部分中指定适当的*InterfaceClassGUID*值。

若要安装一个组件（如类驱动程序）以导出新的设备接口类，INF 还必须有一个[**Inf InterfaceInstall32 部分**](inf-interfaceinstall32-section.md)。

有关设备接口的详细信息，请参阅[设备接口类](device-interface-classes.md)。

## <a name="entries"></a>条目


<a href="" id="addinterface--interfaceclassguid------reference-string-----add-interface-section----flags-------"></a>**AddInterface = {**<em>InterfaceClassGUID</em>**}** \[ **，** \[*引用字符串*\] \[ **，** \[ **,**<em>flags</em> *add-interface-section* \] \]添加接口部分，\]标志\] ...\[  
此指令安装对设备接口类的支持，由驱动程序导出到更高级别的组件的指定*InterfaceClassGUID*值指定。 通常，它还在 INF 文件中的其他位置引用 INF 写入器定义的*添加接口部分*。 有关如何指定此指令的详细信息，请参阅[**INF AddInterface 指令**](inf-addinterface-directive.md)。

<a href="" id="include-filename-inf--filename2-inf----"></a>**Include =**<em>filename</em>**.inf**\[**，**<em>filename2</em>\]...**.inf**  
此可选条目指定一个或多个系统提供的其他 INF 文件，其中包含注册此设备/驱动程序所支持的接口类所需的部分。 如果指定此项，则通常是**需要**输入。

有关其用法的**包含**项和限制的详细信息，请参阅[指定设备文件的源位置和目标位置](specifying-the-source-and-target-locations-for-device-files.md)。

<a href="" id="needs-inf-section-name--inf-section-name----"></a>**需求 =**<em>inf-名称</em>\[**，**<em>inf-节名称</em>\].。。  
此可选条目指定在安装此设备过程中必须处理的特定部分。 通常，此类命名部分是<em>DDInstall</em>**。** 在**包含**项中列出的系统提供的 INF 文件内的接口部分。 但是，它可以是在此类<em>DDInstall</em>中引用的任何部分 **。** 包含的 INF 的接口部分。

不能嵌套**需求**条目。 有关其用法的**需求**条目和限制的详细信息，请参阅[指定设备文件的源位置和目标位置](specifying-the-source-and-target-locations-for-device-files.md)。

<a name="remarks"></a>备注
-------

在 INF 文件的 "每制造商"*型号*部分下， *DDInstall*节名称必须由特定于设备/模型的条目引用。 有关如何使用跨平台 INF 文件中的**ntx86** **、.** **ntia64**、 **. ntamd64**、 **ntarm**和**ntarm64**扩展的信息，请参阅为[多个平台和操作系统创建 INF 文件](creating-inf-files-for-multiple-platforms-and-operating-systems.md)。

如果尚未安装指定的 **{**<em>InterfaceClassGUID</em>**}** ，操作系统的安装代码将在系统中安装该设备接口类。 如果 INF 文件安装一个或多个新的设备接口类，则它还具有标识新类的 GUID 的** \[InterfaceInstall32\] **部分。

有关如何创建 GUID 的详细信息，请参阅[在驱动程序中使用 guid](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-guids-in-drivers)。 对于系统定义的接口类 Guid，请参阅相应的系统提供的标头，如内核流式处理接口类 GUID 的*Ks。*

加载驱动程序时，必须为 INF 的<em>DDInstall</em>中指定的每个 **{**<em>InterfaceClassGUID</em>**}** 值调用[**IoSetDeviceInterfaceState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetdeviceinterfacestate)一次 **。接口**部分，驱动程序在基础设备上支持该接口，以实现更高级别的组件的运行时使用。 设备驱动程序可以在初始调用**IoSetDeviceInterfaceState**之前调用[**IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface) ，而不是在 INF 中注册对设备接口的支持。 通常，PnP 函数或筛选器驱动程序从其[**AddDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程进行此调用。

<a name="examples"></a>示例
--------

此示例显示了<em>DDInstall</em>**。** 系统提供的 WDM 音频设备/驱动程序的 INF 文件中的 "接口" 部分显示为[**inf *DDInstall*部分**](inf-ddinstall-section.md)和[**inf *DDInstall*的示例。服务部分**](inf-ddinstall-services-section.md)。

```inf
;
; following AddInterface= are all single lines (without 
; backslash line continuators) in the system-supplied INF file
;
[WDMPNPB003_Device.NT.Interfaces]
AddInterface=%KSCATEGORY_AUDIO%,%KSNAME_Wave%,\
  WDM_SB16.Interface.Wave
AddInterface=%KSCATEGORY_AUDIO%,%KSNAME_Topology%,\
  WDM_SB16.Interface.Topology
AddInterface=%KSCATEGORY_AUDIO%,%KSNAME_UART%,\
  WDM_SB16.Interface.UART
AddInterface=%KSCATEGORY_AUDIO%,%KSNAME_FMSynth%,\
  WDM_SB16.Interface.FMSynth
; ...

[Strings] ; only immediately preceding %strkey% tokens shown here
%KSCATEGORY_AUDIO% = "{6994ad04-93ef-11d0-a3cc-00a0c9223196}"
KSNAME_Wave = "Wave"
KSNAME_UART = "UART"
KSNAME_FMSynth = "FMSynth" 
KSNAME_Topology = "Topology"
; ...
```

## <a name="see-also"></a>另请参阅


[**AddInterface**](inf-addinterface-directive.md)

[***DDInstall***](inf-ddinstall-section.md)

[**InterfaceInstall32**](inf-interfaceinstall32-section.md)

[**IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface)

[**IoSetDeviceInterfaceState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetdeviceinterfacestate)

[***模型***](inf-models-section.md)

 

 






