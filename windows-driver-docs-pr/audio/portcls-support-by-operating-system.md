---
title: 操作系统提供的 PortCls 支持
description: 操作系统提供的 PortCls 支持
ms.assetid: 87291410-41fa-49d2-a1e2-6d5d9b90deaf
keywords:
- 音频的微型端口驱动程序 WDK，端口类
- 微型端口驱动程序 WDK 音频，端口类
- 端口类库 WDK 音频
- PortCls WDK 音频，每个操作系统的支持
- 音频的电源管理界面 WDK
- 音频流对象接口 WDK
- 音频的微型端口 auxillary 接口 WDK
- 音频的微型端口对象接口 WDK
- 音频端口对象接口 WDK
- 音频的帮助程序对象接口 WDK
- 音频端口类接口 WDK
- 接口 WDK 端口类
- 预提取偏移量
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38785ac24513143a8dffb72b323c53f57bc7c8ac
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328761"
---
# <a name="portcls-support-by-operating-system"></a>操作系统提供的 PortCls 支持


## <span id="portcls_support_by_operating_system"></span><span id="PORTCLS_SUPPORT_BY_OPERATING_SYSTEM"></span>


以下列表包含所有函数和 PortCls 系统驱动程序 (Portcls.sys) 支持的接口。 如果列表项的前面有一个星号 (\*)，然后 PortCls 支持该项仅在 Windows XP 及更高版本。 如果列表项的前面有双星号 (\*\*)，然后 PortCls 支持该项仅在 Windows Vista 和更高版本。 所有其他列表项支持的所有版本的 PortCls (Windows 2000 和更高版本、 和 Windows Me / 98)。

### <a name="span-idaudioportclassfunctionsspanspan-idaudioportclassfunctionsspanspan-idaudioportclassfunctionsspanaudio-port-class-functions"></a><span id="Audio_Port_Class_Functions"></span><span id="audio_port_class_functions"></span><span id="AUDIO_PORT_CLASS_FUNCTIONS"></span>音频端口类函数

[**PcAddAdapterDevice**](https://msdn.microsoft.com/library/windows/hardware/ff537683)

\* [**PcAddContentHandlers**](https://msdn.microsoft.com/library/windows/hardware/ff537684)

[**PcCompleteIrp**](https://msdn.microsoft.com/library/windows/hardware/ff537686)

[**PcCompletePendingPropertyRequest**](https://msdn.microsoft.com/library/windows/hardware/ff537687)

\* [**PcCreateContentMixed**](https://msdn.microsoft.com/library/windows/hardware/ff537689)

\* [**PcDestroyContent**](https://msdn.microsoft.com/library/windows/hardware/ff537690)

[**PcDispatchIrp**](https://msdn.microsoft.com/library/windows/hardware/ff537691)

\* [**PcForwardContentToDeviceObject**](https://msdn.microsoft.com/library/windows/hardware/ff537696)

\* [**PcForwardContentToFileObject**](https://msdn.microsoft.com/library/windows/hardware/ff537697)

\* [**PcForwardContentToInterface**](https://msdn.microsoft.com/library/windows/hardware/ff537698)

[**PcForwardIrpSynchronous**](https://msdn.microsoft.com/library/windows/hardware/ff537699)

\* [**PcGetContentRights**](https://msdn.microsoft.com/library/windows/hardware/ff537700)

[**PcGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff537701)

[**PcGetTimeInterval**](https://msdn.microsoft.com/library/windows/hardware/ff537702)

[**PcInitializeAdapterDriver**](https://msdn.microsoft.com/library/windows/hardware/ff537703)

[**PcNewDmaChannel**](https://msdn.microsoft.com/library/windows/hardware/ff537712)

[**PcNewInterruptSync**](https://msdn.microsoft.com/library/windows/hardware/ff537713)

[**PcNewMiniport**](https://msdn.microsoft.com/library/windows/hardware/ff537714)

[**PcNewPort**](https://msdn.microsoft.com/library/windows/hardware/ff537715)

[**PcNewRegistryKey**](https://msdn.microsoft.com/library/windows/hardware/ff537716)

[**PcNewResourceList**](https://msdn.microsoft.com/library/windows/hardware/ff537717)

[**PcNewResourceSublist**](https://msdn.microsoft.com/library/windows/hardware/ff537718)

[**PcNewServiceGroup**](https://msdn.microsoft.com/library/windows/hardware/ff537719)

[**PcRegisterAdapterPowerManagement**](https://msdn.microsoft.com/library/windows/hardware/ff537724)

[**PcRegisterIoTimeout**](https://msdn.microsoft.com/library/windows/hardware/ff537725)

[**PcRegisterPhysicalConnection**](https://msdn.microsoft.com/library/windows/hardware/ff537726)

[**PcRegisterPhysicalConnectionFromExternal**](https://msdn.microsoft.com/library/windows/hardware/ff537728)

[**PcRegisterPhysicalConnectionToExternal**](https://msdn.microsoft.com/library/windows/hardware/ff537729)

[**PcRegisterSubdevice**](https://msdn.microsoft.com/library/windows/hardware/ff537731)

[**PcRequestNewPowerState**](https://msdn.microsoft.com/library/windows/hardware/ff537733)

[**PcUnregisterIoTimeout**](https://msdn.microsoft.com/library/windows/hardware/ff537736)

### <a name="span-idaudiohelperobjectinterfacesspanspan-idaudiohelperobjectinterfacesspanspan-idaudiohelperobjectinterfacesspanaudio-helper-object-interfaces"></a><span id="Audio_Helper_Object_Interfaces"></span><span id="audio_helper_object_interfaces"></span><span id="AUDIO_HELPER_OBJECT_INTERFACES"></span>音频的帮助程序对象接口

[IDmaChannel](https://msdn.microsoft.com/library/windows/hardware/ff536547)

[IDmaChannelSlave](https://msdn.microsoft.com/library/windows/hardware/ff536548)

\* [IDrmPort](https://msdn.microsoft.com/library/windows/hardware/ff536571)

\* [IDrmPort2](https://msdn.microsoft.com/library/windows/hardware/ff536573)

[IInterruptSync](https://msdn.microsoft.com/library/windows/hardware/ff536590)

[IMasterClock](https://msdn.microsoft.com/library/windows/hardware/ff536696)

\* [IPortClsVersion](https://msdn.microsoft.com/library/windows/hardware/ff536877)

[IPortEvents](https://msdn.microsoft.com/library/windows/hardware/ff536884)

\* [IPreFetchOffset](https://msdn.microsoft.com/library/windows/hardware/ff536951)

[IRegistryKey](https://msdn.microsoft.com/library/windows/hardware/ff536965)

[IResourceList](https://msdn.microsoft.com/library/windows/hardware/ff536976)

[IServiceGroup](https://msdn.microsoft.com/library/windows/hardware/ff536994)

[IServiceSink](https://msdn.microsoft.com/library/windows/hardware/ff537006)

\*\* [IUnregisterPhysicalConnection](https://msdn.microsoft.com/library/windows/hardware/ff537022)

\*\* [IUnregisterSubdevice](https://msdn.microsoft.com/library/windows/hardware/ff537030)

### <a name="span-idaudioportobjectinterfacesspanspan-idaudioportobjectinterfacesspanspan-idaudioportobjectinterfacesspanaudio-port-object-interfaces"></a><span id="Audio_Port_Object_Interfaces"></span><span id="audio_port_object_interfaces"></span><span id="AUDIO_PORT_OBJECT_INTERFACES"></span>音频端口对象接口

[IPort](https://msdn.microsoft.com/library/windows/hardware/ff536842)

[IPortDMus](https://msdn.microsoft.com/library/windows/hardware/ff536879)

[IPortMidi](https://msdn.microsoft.com/library/windows/hardware/ff536891)

[IPortTopology](https://msdn.microsoft.com/library/windows/hardware/ff536896)

[IPortWaveCyclic](https://msdn.microsoft.com/library/windows/hardware/ff536899)

[IPortWavePci](https://msdn.microsoft.com/library/windows/hardware/ff536905)

\*\* [IPortWaveRT](https://msdn.microsoft.com/library/windows/hardware/ff536920)

### <a name="span-idaudiominiportobjectinterfacesspanspan-idaudiominiportobjectinterfacesspanspan-idaudiominiportobjectinterfacesspanaudio-miniport-object-interfaces"></a><span id="Audio_Miniport_Object_Interfaces"></span><span id="audio_miniport_object_interfaces"></span><span id="AUDIO_MINIPORT_OBJECT_INTERFACES"></span>音频微型端口对象接口

[IMiniport](https://msdn.microsoft.com/library/windows/hardware/ff536698)

[IMiniportDMus](https://msdn.microsoft.com/library/windows/hardware/ff536699)

[IMiniportMidi](https://msdn.microsoft.com/library/windows/hardware/ff536703)

[IMiniportTopology](https://msdn.microsoft.com/library/windows/hardware/ff536712)

[IMiniportWaveCyclic](https://msdn.microsoft.com/library/windows/hardware/ff536714)

[IMiniportWavePci](https://msdn.microsoft.com/library/windows/hardware/ff536724)

\*\* [IMiniportWaveRT](https://msdn.microsoft.com/library/windows/hardware/ff536737)

### <a name="span-idaudiominiportauxiliaryinterfacesspanspan-idaudiominiportauxiliaryinterfacesspanspan-idaudiominiportauxiliaryinterfacesspanaudio-miniport-auxiliary-interfaces"></a><span id="Audio_Miniport_Auxiliary_Interfaces"></span><span id="audio_miniport_auxiliary_interfaces"></span><span id="AUDIO_MINIPORT_AUXILIARY_INTERFACES"></span>音频微型端口辅助接口

\* [IMusicTechnology](https://msdn.microsoft.com/library/windows/hardware/ff536778)

\* [IPinCount](https://msdn.microsoft.com/library/windows/hardware/ff536832)

### <a name="span-idaudiostreamobjectinterfacesspanspan-idaudiostreamobjectinterfacesspanspan-idaudiostreamobjectinterfacesspanaudio-stream-object-interfaces"></a><span id="Audio_Stream_Object_Interfaces"></span><span id="audio_stream_object_interfaces"></span><span id="AUDIO_STREAM_OBJECT_INTERFACES"></span>音频 Stream 对象接口

[IAllocatorMXF](https://msdn.microsoft.com/library/windows/hardware/ff536491)

\* [IDrmAudioStream](https://msdn.microsoft.com/library/windows/hardware/ff536568)

[IMiniportMidiStream](https://msdn.microsoft.com/library/windows/hardware/ff536704)

[IMiniportWaveCyclicStream](https://msdn.microsoft.com/library/windows/hardware/ff536715)

[IMiniportWavePciStream](https://msdn.microsoft.com/library/windows/hardware/ff536725)

\*\* [IMiniportWaveRTStream](https://msdn.microsoft.com/library/windows/hardware/ff536738)

[IMXF](https://msdn.microsoft.com/library/windows/hardware/ff536782)

[IPortWavePciStream](https://msdn.microsoft.com/library/windows/hardware/ff536907)

\*\* [IPortWaveRTStream](https://msdn.microsoft.com/library/windows/hardware/ff536922)

[ISynthSinkDMus](https://msdn.microsoft.com/library/windows/hardware/ff537011)

### <a name="span-idaudiopowermanagementinterfacesspanspan-idaudiopowermanagementinterfacesspanspan-idaudiopowermanagementinterfacesspanaudio-power-management-interfaces"></a><span id="Audio_Power_Management_Interfaces"></span><span id="audio_power_management_interfaces"></span><span id="AUDIO_POWER_MANAGEMENT_INTERFACES"></span>音频的电源管理界面

[IAdapterPowerManagement](https://msdn.microsoft.com/library/windows/hardware/ff536485)

[IPowerNotify](https://msdn.microsoft.com/library/windows/hardware/ff536947)

 

 




