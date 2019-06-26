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
ms.openlocfilehash: ae04865cfdc6086e145245928ea13e85d7208a6c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362555"
---
# <a name="portcls-support-by-operating-system"></a>操作系统提供的 PortCls 支持


## <span id="portcls_support_by_operating_system"></span><span id="PORTCLS_SUPPORT_BY_OPERATING_SYSTEM"></span>


以下列表包含所有函数和 PortCls 系统驱动程序 (Portcls.sys) 支持的接口。 如果列表项的前面有一个星号 (\*)，然后 PortCls 支持该项仅在 Windows XP 及更高版本。 如果列表项的前面有双星号 (\*\*)，然后 PortCls 支持该项仅在 Windows Vista 和更高版本。 所有其他列表项支持的所有版本的 PortCls (Windows 2000 和更高版本、 和 Windows Me / 98)。

### <a name="span-idaudioportclassfunctionsspanspan-idaudioportclassfunctionsspanspan-idaudioportclassfunctionsspanaudio-port-class-functions"></a><span id="Audio_Port_Class_Functions"></span><span id="audio_port_class_functions"></span><span id="AUDIO_PORT_CLASS_FUNCTIONS"></span>音频端口类函数

[**PcAddAdapterDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcaddadapterdevice)

\* [**PcAddContentHandlers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcaddcontenthandlers)

[**PcCompleteIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pccompleteirp)

[**PcCompletePendingPropertyRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pccompletependingpropertyrequest)

\* [**PcCreateContentMixed**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pccreatecontentmixed)

\* [**PcDestroyContent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcdestroycontent)

[**PcDispatchIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcdispatchirp)

\* [**PcForwardContentToDeviceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcforwardcontenttodeviceobject)

\* [**PcForwardContentToFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcforwardcontenttofileobject)

\* [**PcForwardContentToInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcforwardcontenttointerface)

[**PcForwardIrpSynchronous**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcforwardirpsynchronous)

\* [**PcGetContentRights**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcgetcontentrights)

[**PcGetDeviceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcgetdeviceproperty)

[**PcGetTimeInterval**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcgettimeinterval)

[**PcInitializeAdapterDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcinitializeadapterdriver)

[**PcNewDmaChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcnewdmachannel)

[**PcNewInterruptSync**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcnewinterruptsync)

[**PcNewMiniport**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcnewminiport)

[**PcNewPort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcnewport)

[**PcNewRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcnewregistrykey)

[**PcNewResourceList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcnewresourcelist)

[**PcNewResourceSublist**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcnewresourcesublist)

[**PcNewServiceGroup**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcnewservicegroup)

[**PcRegisterAdapterPowerManagement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcregisteradapterpowermanagement)

[**PcRegisterIoTimeout**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcregisteriotimeout)

[**PcRegisterPhysicalConnection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcregisterphysicalconnection)

[**PcRegisterPhysicalConnectionFromExternal**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcregisterphysicalconnectionfromexternal)

[**PcRegisterPhysicalConnectionToExternal**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcregisterphysicalconnectiontoexternal)

[**PcRegisterSubdevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcregistersubdevice)

[**PcRequestNewPowerState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcrequestnewpowerstate)

[**PcUnregisterIoTimeout**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcunregisteriotimeout)

### <a name="span-idaudiohelperobjectinterfacesspanspan-idaudiohelperobjectinterfacesspanspan-idaudiohelperobjectinterfacesspanaudio-helper-object-interfaces"></a><span id="Audio_Helper_Object_Interfaces"></span><span id="audio_helper_object_interfaces"></span><span id="AUDIO_HELPER_OBJECT_INTERFACES"></span>音频的帮助程序对象接口

[IDmaChannel](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-idmachannel)

[IDmaChannelSlave](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-idmachannelslave)

\* [IDrmPort](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-idrmport)

\* [IDrmPort2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-idrmport2)

[IInterruptSync](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iinterruptsync)

[IMasterClock](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-imasterclock)

\* [IPortClsVersion](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportclsversion)

[IPortEvents](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportevents)

\* [IPreFetchOffset](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iprefetchoffset)

[IRegistryKey](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iregistrykey)

[IResourceList](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iresourcelist)

[IServiceGroup](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iservicegroup)

[IServiceSink](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iservicesink)

\*\* [IUnregisterPhysicalConnection](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iunregisterphysicalconnection)

\*\* [IUnregisterSubdevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iunregistersubdevice)

### <a name="span-idaudioportobjectinterfacesspanspan-idaudioportobjectinterfacesspanspan-idaudioportobjectinterfacesspanaudio-port-object-interfaces"></a><span id="Audio_Port_Object_Interfaces"></span><span id="audio_port_object_interfaces"></span><span id="AUDIO_PORT_OBJECT_INTERFACES"></span>音频端口对象接口

[IPort](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iport)

[IPortDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-iportdmus)

[IPortMidi](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportmidi)

[IPortTopology](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iporttopology)

[IPortWaveCyclic](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportwavecyclic)

[IPortWavePci](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536905(v=vs.85))

\*\* [IPortWaveRT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportwavert)

### <a name="span-idaudiominiportobjectinterfacesspanspan-idaudiominiportobjectinterfacesspanspan-idaudiominiportobjectinterfacesspanaudio-miniport-object-interfaces"></a><span id="Audio_Miniport_Object_Interfaces"></span><span id="audio_miniport_object_interfaces"></span><span id="AUDIO_MINIPORT_OBJECT_INTERFACES"></span>音频微型端口对象接口

[IMiniport](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiport)

[IMiniportDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-iminiportdmus)

[IMiniportMidi](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportmidi)

[IMiniportTopology](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiporttopology)

[IMiniportWaveCyclic](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavecyclic)

[IMiniportWavePci](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavepci)

\*\* [IMiniportWaveRT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavert)

### <a name="span-idaudiominiportauxiliaryinterfacesspanspan-idaudiominiportauxiliaryinterfacesspanspan-idaudiominiportauxiliaryinterfacesspanaudio-miniport-auxiliary-interfaces"></a><span id="Audio_Miniport_Auxiliary_Interfaces"></span><span id="audio_miniport_auxiliary_interfaces"></span><span id="AUDIO_MINIPORT_AUXILIARY_INTERFACES"></span>音频微型端口辅助接口

\* [IMusicTechnology](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-imusictechnology)

\* [IPinCount](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-ipincount)

### <a name="span-idaudiostreamobjectinterfacesspanspan-idaudiostreamobjectinterfacesspanspan-idaudiostreamobjectinterfacesspanaudio-stream-object-interfaces"></a><span id="Audio_Stream_Object_Interfaces"></span><span id="audio_stream_object_interfaces"></span><span id="AUDIO_STREAM_OBJECT_INTERFACES"></span>音频 Stream 对象接口

[IAllocatorMXF](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-iallocatormxf)

\* [IDrmAudioStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/drmk/nn-drmk-idrmaudiostream)

[IMiniportMidiStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportmidistream)

[IMiniportWaveCyclicStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavecyclicstream)

[IMiniportWavePciStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavepcistream)

\*\* [IMiniportWaveRTStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavertstream)

[IMXF](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-imxf)

[IPortWavePciStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportwavepcistream)

\*\* [IPortWaveRTStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportwavertstream)

[ISynthSinkDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-isynthsinkdmus)

### <a name="span-idaudiopowermanagementinterfacesspanspan-idaudiopowermanagementinterfacesspanspan-idaudiopowermanagementinterfacesspanaudio-power-management-interfaces"></a><span id="Audio_Power_Management_Interfaces"></span><span id="audio_power_management_interfaces"></span><span id="AUDIO_POWER_MANAGEMENT_INTERFACES"></span>音频的电源管理界面

[IAdapterPowerManagement](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iadapterpowermanagement)

[IPowerNotify](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-ipowernotify)

 

 




