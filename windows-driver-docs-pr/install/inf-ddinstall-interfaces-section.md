---
title: INF DDInstall.Interfaces 节
description: 每个模型 DDInstall.Interfaces 部分可以具有一个或多个 AddInterface 指令，具体取决于特定设备/驱动程序支持多少个设备接口。
ms.assetid: 16904119-00a4-45d7-a32e-24ba4c8a3416
keywords:
- INF DDInstall.Interfaces 部分设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF DDInstall.Interfaces Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc11c9fd37f80773e9ba27e2381516f033d7a5a6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385910"
---
# <a name="inf-ddinstallinterfaces-section"></a>INF DDInstall.Interfaces 节


每个每个模型<em>DDInstall</em> **。接口**部分可以具有一个或多个[ **AddInterface** ](inf-addinterface-directive.md)指令，具体取决于特定设备/驱动程序支持多少个设备接口。

```ini
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

若要支持现有设备接口，例如任何系统的预定义内核流式处理接口，指定相应*InterfaceClassGUID*在本部分中的值。

若要安装的组件的类驱动程序，将导出的设备接口的新类，如 INF 必须还具有[ **INF InterfaceInstall32 部分**](inf-interfaceinstall32-section.md)。

有关设备接口的详细信息，请参阅[设备接口类](device-interface-classes.md)。

## <a name="entries"></a>条目


<a href="" id="addinterface--interfaceclassguid------reference-string-----add-interface-section----flags-------"></a>**AddInterface = {** <em>InterfaceClassGUID</em> **}** \[ **，** \[*引用字符串*\] \[ **，** \[*添加接口部分*\] \[ **，** <em>标志</em>\] \] \] ...  
此指令将安装设备接口类，指定由指定的支持*InterfaceClassGUID*驱动程序将导出到更高级的组件的值。 通常情况下，它还引用 INF 编写器的定义*添加接口部分*INF 文件中的其他位置。 有关如何指定此指令的详细信息，请参阅[ **INF AddInterface 指令**](inf-addinterface-directive.md)。

<a href="" id="include-filename-inf--filename2-inf----"></a>**Include=** <em>filename</em> **.inf**\[ **,** <em>filename2</em> **.inf**\]...  
此可选项指定一个或多个其他系统提供 INF 文件包含注册此设备/驱动程序支持的接口类所需的部分。 如果指定此项时，通常那么**需要**条目。

有关详细信息**Include**条目和限制其使用时，请参阅[设备文件中指定的源和目标位置](specifying-the-source-and-target-locations-for-device-files.md)。

<a href="" id="needs-inf-section-name--inf-section-name----"></a>**需要 =** <em>inf 部分名称</em>\[ **，** <em>inf 部分名称</em>\]...  
此可选项指定必须在此设备的安装过程中处理的特定部分。 通常情况下，此类指定的部分是<em>DDInstall</em> **。接口**中列出系统提供 INF 文件中的节**Include**条目。 但是，它可以是任何部分此类中被引用<em>DDInstall</em> **。接口**包含 INF 部分。

**需要**条目不能嵌套。 有关详细信息**需要**条目和限制其使用时，请参阅[设备文件中指定的源和目标位置](specifying-the-source-and-target-locations-for-device-files.md)。

<a name="remarks"></a>备注
-------

*DDInstall*节的名称必须由下每个制造商的特定于设备/模型的项引用*模型*INF 文件部分。 有关如何使用系统定义的信息 **.nt**， **.ntx86**， **.ntia64**， **.ntamd64**， **.ntarm**，并 **.ntarm64**扩展在跨平台的 INF 文件，请参阅[创建多个平台和操作系统的 INF 文件](creating-inf-files-for-multiple-platforms-and-operating-systems.md)。

如果指定 **{** <em>InterfaceClassGUID</em> **}** 未安装操作系统的安装程序代码，请在系统中安装该设备接口类。 如果一个 INF 文件将安装一个或多个新的设备接口类，它还具有 **\[InterfaceInstall32\]** 部分标识的 GUID 的新类...

有关如何创建 GUID 的详细信息，请参阅[驱动程序中使用 Guid](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-guids-in-drivers)。 有关系统定义的接口类 Guid，请参阅相应系统提供的标头，诸如*Ks.h*内核流式处理接口的类 GUID。

加载驱动程序时，它必须调用[ **IoSetDeviceInterfaceState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetdeviceinterfacestate)一次为每个 **{** <em>InterfaceClassGUID</em> **}** INF 中指定值<em>DDInstall</em> **。接口**的驱动程序支持对基础设备，通过更高级的组件启用运行时使用的接口上的部分。 设备驱动程序可以调用而不是 INF 中注册设备接口的支持， [ **IoRegisterDeviceInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioregisterdeviceinterface)之前进行到其初始调用**IoSetDeviceInterfaceState**. 通常情况下，即插即用的函数或筛选器驱动程序，可以从此调用其[ **AddDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)例程。

<a name="examples"></a>示例
--------

此示例演示<em>DDInstall</em> **.nt。接口**系统提供 WDM 音频设备/驱动程序的示例所示的 INF 文件中节[ **INF *DDInstall*部分**](inf-ddinstall-section.md)并[ **INF *DDInstall*。服务部分**](inf-ddinstall-services-section.md) 。

```ini
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

## <a name="see-also"></a>请参阅


[**AddInterface**](inf-addinterface-directive.md)

[***DDInstall***](inf-ddinstall-section.md)

[**InterfaceInstall32**](inf-interfaceinstall32-section.md)

[**IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioregisterdeviceinterface)

[**IoSetDeviceInterfaceState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetdeviceinterfacestate)

[***模型***](inf-models-section.md)

 

 






