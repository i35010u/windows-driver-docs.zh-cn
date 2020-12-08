---
title: 操作系统提供的 PortCls 支持
description: 操作系统提供的 PortCls 支持
keywords:
- 音频微型端口驱动程序 WDK，端口类
- 微型端口驱动程序 WDK 音频，端口类
- 端口类库 WDK 音频
- PortCls WDK 音频，每个操作系统支持
- 音频电源管理接口 WDK
- 音频流对象接口 WDK
- 音频微型端口辅助接口 WDK
- 音频微型端口对象接口 WDK
- 音频端口对象接口 WDK
- 音频助手对象接口 WDK
- 音频端口类接口 WDK
- 接口 WDK 端口类
- 预提取偏移
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 98b82c2e4953398558924b269693fbb5b0b46b85
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800799"
---
# <a name="portcls-support-by-operating-system"></a>操作系统提供的 PortCls 支持


## <span id="portcls_support_by_operating_system"></span><span id="PORTCLS_SUPPORT_BY_OPERATING_SYSTEM"></span>


以下列表包含 PortCls 系统驱动程序 ( # A0) 支持的所有函数和接口。 如果列表项前面有一个星号 (\*) ，则 PortCls 仅在 WINDOWS XP 和更高版本中支持该项。 如果列表项前面有一个双星号 (\* \*) ，则 PortCls 仅在 Windows Vista 和更高版本中支持该项。 所有其他列表项都受 PortCls (Windows 2000 及更高版本以及 Windows Me/98) 的所有版本支持。

### <a name="span-idaudio_port_class_functionsspanspan-idaudio_port_class_functionsspanspan-idaudio_port_class_functionsspanaudio-port-class-functions"></a><span id="Audio_Port_Class_Functions"></span><span id="audio_port_class_functions"></span><span id="AUDIO_PORT_CLASS_FUNCTIONS"></span>音频端口类函数

[**PcAddAdapterDevice**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcaddadapterdevice)

\*[ **PcAddContentHandlers**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcaddcontenthandlers)

[**PcCompleteIrp**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pccompleteirp)

[**PcCompletePendingPropertyRequest**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pccompletependingpropertyrequest)

\*[ **PcCreateContentMixed**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pccreatecontentmixed)

\*[ **PcDestroyContent**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcdestroycontent)

[**PcDispatchIrp**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcdispatchirp)

\*[ **PcForwardContentToDeviceObject**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcforwardcontenttodeviceobject)

\*[ **PcForwardContentToFileObject**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcforwardcontenttofileobject)

\*[ **PcForwardContentToInterface**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcforwardcontenttointerface)

[**PcForwardIrpSynchronous**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcforwardirpsynchronous)

\*[ **PcGetContentRights**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcgetcontentrights)

[**PcGetDeviceProperty**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcgetdeviceproperty)

[**PcGetTimeInterval**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcgettimeinterval)

[**PcInitializeAdapterDriver**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcinitializeadapterdriver)

[**PcNewDmaChannel**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewdmachannel)

[**PcNewInterruptSync**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewinterruptsync)

[**PcNewMiniport**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewminiport)

[**PcNewPort**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewport)

[**PcNewRegistryKey**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewregistrykey)

[**PcNewResourceList**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewresourcelist)

[**PcNewResourceSublist**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewresourcesublist)

[**PcNewServiceGroup**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewservicegroup)

[**PcRegisterAdapterPowerManagement**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregisteradapterpowermanagement)

[**PcRegisterIoTimeout**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregisteriotimeout)

[**PcRegisterPhysicalConnection**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregisterphysicalconnection)

[**PcRegisterPhysicalConnectionFromExternal**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregisterphysicalconnectionfromexternal)

[**PcRegisterPhysicalConnectionToExternal**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregisterphysicalconnectiontoexternal)

[**PcRegisterSubdevice**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregistersubdevice)

[**PcRequestNewPowerState**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcrequestnewpowerstate)

[**PcUnregisterIoTimeout**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcunregisteriotimeout)

### <a name="span-idaudio_helper_object_interfacesspanspan-idaudio_helper_object_interfacesspanspan-idaudio_helper_object_interfacesspanaudio-helper-object-interfaces"></a><span id="Audio_Helper_Object_Interfaces"></span><span id="audio_helper_object_interfaces"></span><span id="AUDIO_HELPER_OBJECT_INTERFACES"></span>音频帮助程序对象接口

[IDmaChannel](/windows-hardware/drivers/ddi/portcls/nn-portcls-idmachannel)

[IDmaChannelSlave](/windows-hardware/drivers/ddi/portcls/nn-portcls-idmachannelslave)

\*[IDrmPort](/windows-hardware/drivers/ddi/portcls/nn-portcls-idrmport)

\*[IDrmPort2](/windows-hardware/drivers/ddi/portcls/nn-portcls-idrmport2)

[IInterruptSync](/windows-hardware/drivers/ddi/portcls/nn-portcls-iinterruptsync)

[IMasterClock](/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-imasterclock)

\*[IPortClsVersion](/windows-hardware/drivers/ddi/portcls/nn-portcls-iportclsversion)

[IPortEvents](/windows-hardware/drivers/ddi/portcls/nn-portcls-iportevents)

\*[IPreFetchOffset](/windows-hardware/drivers/ddi/portcls/nn-portcls-iprefetchoffset)

[IRegistryKey](/windows-hardware/drivers/ddi/portcls/nn-portcls-iregistrykey)

[IResourceList](/windows-hardware/drivers/ddi/portcls/nn-portcls-iresourcelist)

[IServiceGroup](/windows-hardware/drivers/ddi/portcls/nn-portcls-iservicegroup)

[IServiceSink](/windows-hardware/drivers/ddi/portcls/nn-portcls-iservicesink)

\*\*[IUnregisterPhysicalConnection](/windows-hardware/drivers/ddi/portcls/nn-portcls-iunregisterphysicalconnection)

\*\*[IUnregisterSubdevice](/windows-hardware/drivers/ddi/portcls/nn-portcls-iunregistersubdevice)

### <a name="span-idaudio_port_object_interfacesspanspan-idaudio_port_object_interfacesspanspan-idaudio_port_object_interfacesspanaudio-port-object-interfaces"></a><span id="Audio_Port_Object_Interfaces"></span><span id="audio_port_object_interfaces"></span><span id="AUDIO_PORT_OBJECT_INTERFACES"></span>音频端口对象接口

[IPort](/windows-hardware/drivers/ddi/portcls/nn-portcls-iport)

[IPortDMus](/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iportdmus)

[IPortMidi](/windows-hardware/drivers/ddi/portcls/nn-portcls-iportmidi)

[IPortTopology](/windows-hardware/drivers/ddi/portcls/nn-portcls-iporttopology)

[IPortWaveCyclic](/windows-hardware/drivers/ddi/portcls/nn-portcls-iportwavecyclic)

[IPortWavePci](/windows-hardware/drivers/ddi/portcls/nn-portcls-iportwavepci)

\*\*[IPortWaveRT](/windows-hardware/drivers/ddi/portcls/nn-portcls-iportwavert)

### <a name="span-idaudio_miniport_object_interfacesspanspan-idaudio_miniport_object_interfacesspanspan-idaudio_miniport_object_interfacesspanaudio-miniport-object-interfaces"></a><span id="Audio_Miniport_Object_Interfaces"></span><span id="audio_miniport_object_interfaces"></span><span id="AUDIO_MINIPORT_OBJECT_INTERFACES"></span>音频微型端口对象接口

[IMiniport](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiport)

[IMiniportDMus](/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iminiportdmus)

[IMiniportMidi](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportmidi)

[IMiniportTopology](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiporttopology)

[IMiniportWaveCyclic](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavecyclic)

[IMiniportWavePci](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavepci)

\*\*[IMiniportWaveRT](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavert)

### <a name="span-idaudio_miniport_auxiliary_interfacesspanspan-idaudio_miniport_auxiliary_interfacesspanspan-idaudio_miniport_auxiliary_interfacesspanaudio-miniport-auxiliary-interfaces"></a><span id="Audio_Miniport_Auxiliary_Interfaces"></span><span id="audio_miniport_auxiliary_interfaces"></span><span id="AUDIO_MINIPORT_AUXILIARY_INTERFACES"></span>音频微型端口辅助接口

\*[IMusicTechnology](/windows-hardware/drivers/ddi/portcls/nn-portcls-imusictechnology)

\*[IPinCount](/windows-hardware/drivers/ddi/portcls/nn-portcls-ipincount)

### <a name="span-idaudio_stream_object_interfacesspanspan-idaudio_stream_object_interfacesspanspan-idaudio_stream_object_interfacesspanaudio-stream-object-interfaces"></a><span id="Audio_Stream_Object_Interfaces"></span><span id="audio_stream_object_interfaces"></span><span id="AUDIO_STREAM_OBJECT_INTERFACES"></span>音频流对象接口

[IAllocatorMXF](/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iallocatormxf)

\*[IDrmAudioStream](/windows-hardware/drivers/ddi/drmk/nn-drmk-idrmaudiostream)

[IMiniportMidiStream](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportmidistream)

[IMiniportWaveCyclicStream](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavecyclicstream)

[IMiniportWavePciStream](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavepcistream)

\*\*[IMiniportWaveRTStream](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavertstream)

[IMXF](/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-imxf)

[IPortWavePciStream](/windows-hardware/drivers/ddi/portcls/nn-portcls-iportwavepcistream)

\*\*[IPortWaveRTStream](/windows-hardware/drivers/ddi/portcls/nn-portcls-iportwavertstream)

[ISynthSinkDMus](/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-isynthsinkdmus)

### <a name="span-idaudio_power_management_interfacesspanspan-idaudio_power_management_interfacesspanspan-idaudio_power_management_interfacesspanaudio-power-management-interfaces"></a><span id="Audio_Power_Management_Interfaces"></span><span id="audio_power_management_interfaces"></span><span id="AUDIO_POWER_MANAGEMENT_INTERFACES"></span>音频电源管理接口

[IAdapterPowerManagement](/windows-hardware/drivers/ddi/portcls/nn-portcls-iadapterpowermanagement)

[IPowerNotify](/windows-hardware/drivers/ddi/portcls/nn-portcls-ipowernotify)

 

