---
title: 已过时端口类函数
description: 已过时端口类函数
ms.assetid: 6fcb5ae6-81bc-423e-9757-34955a2de522
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e609a1f78e86e964a6e72eb2d1d6f05b9bf71dd1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363196"
---
# <a name="obsolete-port-class-functions"></a>已过时端口类函数


## <span id="ddk_obsolete_port_class_functions_ks"></span><span id="DDK_OBSOLETE_PORT_CLASS_FUNCTIONS_KS"></span>


包含新 PortCls 函数替换为已过时 PortCls 函数的名称的标头文件 portcls.hdefines 宏。 这些宏允许旧包含引用已过时 PortCls 函数名称来重新编译，而无需对源代码文件的任何编辑使用新的 PortCls 函数的源代码。

当编译使用过时的名称的源代码，定义的参数名称 PC\_旧\_名称。 此参数可以由编译器命令行参数"-DPC\_旧\_名称"这是比简介语句更方便`#define PC_OLD_NAMES`到源文件本身。

下表列出了左侧列中的过时 PortCls 函数名称。 对于每个已过时的名称，中心列包含替换为新 PortCls 函数的名称。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">已过时的函数名称</th>
<th align="left">新的函数名称</th>
<th align="left">未更改的参数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>AddAdapterDevice</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcaddadapterdevice" data-raw-source="[&lt;strong&gt;PcAddAdapterDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcaddadapterdevice)"><strong>PcAddAdapterDevice</strong></a></p></td>
<td align="left"><p>是</p></td>
</tr>
<tr class="even">
<td align="left"><p>CompletePendingPropertyRequest</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pccompletependingpropertyrequest" data-raw-source="[&lt;strong&gt;PcCompletePendingPropertyRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pccompletependingpropertyrequest)"><strong>PcCompletePendingPropertyRequest</strong></a></p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="odd">
<td align="left"><p>GetTimeInterval</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcgettimeinterval" data-raw-source="[&lt;strong&gt;PcGetTimeInterval&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcgettimeinterval)"><strong>PcGetTimeInterval</strong></a></p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="even">
<td align="left"><p>InitializeAdapterDriver</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcinitializeadapterdriver" data-raw-source="[&lt;strong&gt;PcInitializeAdapterDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcinitializeadapterdriver)"><strong>PcInitializeAdapterDriver</strong></a></p></td>
<td align="left"><p>是</p></td>
</tr>
<tr class="odd">
<td align="left"><p>NewDmaChannel</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcnewdmachannel" data-raw-source="[&lt;strong&gt;PcNewDmaChannel&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcnewdmachannel)"><strong>PcNewDmaChannel</strong></a></p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="even">
<td align="left"><p>NewMiniport</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcnewminiport" data-raw-source="[&lt;strong&gt;PcNewMiniport&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcnewminiport)"><strong>PcNewMiniport</strong></a></p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="odd">
<td align="left"><p>NewPort</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcnewport" data-raw-source="[&lt;strong&gt;PcNewPort&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcnewport)"><strong>PcNewPort</strong></a></p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="even">
<td align="left"><p>NewResourceList</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcnewresourcelist" data-raw-source="[&lt;strong&gt;PcNewResourceList&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcnewresourcelist)"><strong>PcNewResourceList</strong></a></p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="odd">
<td align="left"><p>NewResourceSublist</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcnewresourcesublist" data-raw-source="[&lt;strong&gt;PcNewResourceSublist&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcnewresourcesublist)"><strong>PcNewResourceSublist</strong></a></p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="even">
<td align="left"><p>NewServiceGroup</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcnewservicegroup" data-raw-source="[&lt;strong&gt;PcNewServiceGroup&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcnewservicegroup)"><strong>PcNewServiceGroup</strong></a></p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="odd">
<td align="left"><p>RegisterPhysicalConnection</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcregisterphysicalconnection" data-raw-source="[&lt;strong&gt;PcRegisterPhysicalConnection&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcregisterphysicalconnection)"><strong>PcRegisterPhysicalConnection</strong></a></p></td>
<td align="left"><p>是</p></td>
</tr>
<tr class="even">
<td align="left"><p>RegisterPhysicalConnectionFromExternal</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcregisterphysicalconnectionfromexternal" data-raw-source="[&lt;strong&gt;PcRegisterPhysicalConnectionFromExternal&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcregisterphysicalconnectionfromexternal)"><strong>PcRegisterPhysicalConnectionFromExternal</strong></a></p></td>
<td align="left"><p>是</p></td>
</tr>
<tr class="odd">
<td align="left"><p>RegisterPhysicalConnectionToExternal</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcregisterphysicalconnectiontoexternal" data-raw-source="[&lt;strong&gt;PcRegisterPhysicalConnectionToExternal&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcregisterphysicalconnectiontoexternal)"><strong>PcRegisterPhysicalConnectionToExternal</strong></a></p></td>
<td align="left"><p>是</p></td>
</tr>
<tr class="even">
<td align="left"><p>RegisterSubdevice</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcregistersubdevice" data-raw-source="[&lt;strong&gt;PcRegisterSubdevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcregistersubdevice)"><strong>PcRegisterSubdevice</strong></a></p></td>
<td align="left"><p>是</p></td>
</tr>
</tbody>
</table>

 

在某些情况下，更改相当于不会有超过一个简单名称更改：限定符`Pc`在名称以指示在 PortCls 中实现函数的开头处插入。 在其他情况下，但是，自变量列表已更改以及函数的名称。 右侧列前面表中的指示的参数已更改。

在参数已更改的情况下，portcls.hconvert 中的宏的自变量列表到新的 PortCls 函数的等效参数已过时的 PortCls 函数。 下列宏包含自变量转换：

```cpp
#define InitializeAdapterDriver(c1,c2,a) \
    PcInitializeAdapterDriver(PDRIVER_OBJECT(c1),PUNICODE_STRING(c2),PDRIVER_ADD_DEVICE(a))
#define AddAdapterDevice(c1,c2,s,m) \
    PcAddAdapterDevice(PDRIVER_OBJECT(c1),PDEVICE_OBJECT(c2),s,m,0)
#define RegisterSubdevice(c1,c2,n,u) \
    PcRegisterSubdevice(PDEVICE_OBJECT(c1),n,u)
#define RegisterPhysicalConnection(c1,c2,fs,fp,ts,tp) \
    PcRegisterPhysicalConnection(PDEVICE_OBJECT(c1),fs,fp,ts,tp)
#define RegisterPhysicalConnectionToExternal(c1,c2,fs,fp,ts,tp) \
    PcRegisterPhysicalConnectionToExternal(PDEVICE_OBJECT(c1),fs,fp,ts,tp)
#define RegisterPhysicalConnectionFromExternal(c1,c2,fs,fp,ts,tp) \
    PcRegisterPhysicalConnectionFromExternal(PDEVICE_OBJECT(c1),fs,fp,ts,tp)
```

 

 





