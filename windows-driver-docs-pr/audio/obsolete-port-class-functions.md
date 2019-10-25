---
title: 已过时端口类函数
description: 已过时端口类函数
ms.assetid: 6fcb5ae6-81bc-423e-9757-34955a2de522
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e9ad4ea37508455ad714b870d286886a973b52c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830316"
---
# <a name="obsolete-port-class-functions"></a>已过时端口类函数


## <span id="ddk_obsolete_port_class_functions_ks"></span><span id="DDK_OBSOLETE_PORT_CLASS_FUNCTIONS_KS"></span>


标头文件 portcls. hdefines 宏，其中包含已被新的 PortCls 函数替换的过时 PortCls 函数的名称。 这些宏允许重新编译包含过时 PortCls 函数名称引用的旧源代码，以使用新的 PortCls 函数，而无需对源文件进行任何编辑。

在编译使用过时名称的源代码时，请将参数名称 PC 定义\_旧\_名称。 此参数可由编译器命令行参数 "-DPC\_旧的\_名称" 来定义，如果这比向源文件 `#define PC_OLD_NAMES` 引入语句更方便。

下表列出了左栏中已过时的 PortCls 函数名称。 对于每个过时名称，中间列都包含替换它的新 PortCls 函数的名称。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">过时的函数名称</th>
<th align="left">新函数名称</th>
<th align="left">参数是否更改？</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>AddAdapterDevice</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcaddadapterdevice" data-raw-source="[&lt;strong&gt;PcAddAdapterDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcaddadapterdevice)"><strong>PcAddAdapterDevice</strong></a></p></td>
<td align="left"><p>是</p></td>
</tr>
<tr class="even">
<td align="left"><p>CompletePendingPropertyRequest</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pccompletependingpropertyrequest" data-raw-source="[&lt;strong&gt;PcCompletePendingPropertyRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pccompletependingpropertyrequest)"><strong>PcCompletePendingPropertyRequest</strong></a></p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="odd">
<td align="left"><p>GetTimeInterval</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcgettimeinterval" data-raw-source="[&lt;strong&gt;PcGetTimeInterval&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcgettimeinterval)"><strong>PcGetTimeInterval</strong></a></p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="even">
<td align="left"><p>InitializeAdapterDriver</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcinitializeadapterdriver" data-raw-source="[&lt;strong&gt;PcInitializeAdapterDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcinitializeadapterdriver)"><strong>PcInitializeAdapterDriver</strong></a></p></td>
<td align="left"><p>是</p></td>
</tr>
<tr class="odd">
<td align="left"><p>NewDmaChannel</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewdmachannel" data-raw-source="[&lt;strong&gt;PcNewDmaChannel&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewdmachannel)"><strong>PcNewDmaChannel</strong></a></p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="even">
<td align="left"><p>NewMiniport</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewminiport" data-raw-source="[&lt;strong&gt;PcNewMiniport&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewminiport)"><strong>PcNewMiniport</strong></a></p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="odd">
<td align="left"><p>纽波特</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewport" data-raw-source="[&lt;strong&gt;PcNewPort&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewport)"><strong>PcNewPort</strong></a></p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="even">
<td align="left"><p>NewResourceList</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewresourcelist" data-raw-source="[&lt;strong&gt;PcNewResourceList&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewresourcelist)"><strong>PcNewResourceList</strong></a></p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="odd">
<td align="left"><p>NewResourceSublist</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewresourcesublist" data-raw-source="[&lt;strong&gt;PcNewResourceSublist&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewresourcesublist)"><strong>PcNewResourceSublist</strong></a></p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="even">
<td align="left"><p>NewServiceGroup</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewservicegroup" data-raw-source="[&lt;strong&gt;PcNewServiceGroup&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewservicegroup)"><strong>PcNewServiceGroup</strong></a></p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="odd">
<td align="left"><p>RegisterPhysicalConnection</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregisterphysicalconnection" data-raw-source="[&lt;strong&gt;PcRegisterPhysicalConnection&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregisterphysicalconnection)"><strong>PcRegisterPhysicalConnection</strong></a></p></td>
<td align="left"><p>是</p></td>
</tr>
<tr class="even">
<td align="left"><p>RegisterPhysicalConnectionFromExternal</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregisterphysicalconnectionfromexternal" data-raw-source="[&lt;strong&gt;PcRegisterPhysicalConnectionFromExternal&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregisterphysicalconnectionfromexternal)"><strong>PcRegisterPhysicalConnectionFromExternal</strong></a></p></td>
<td align="left"><p>是</p></td>
</tr>
<tr class="odd">
<td align="left"><p>RegisterPhysicalConnectionToExternal</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregisterphysicalconnectiontoexternal" data-raw-source="[&lt;strong&gt;PcRegisterPhysicalConnectionToExternal&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregisterphysicalconnectiontoexternal)"><strong>PcRegisterPhysicalConnectionToExternal</strong></a></p></td>
<td align="left"><p>是</p></td>
</tr>
<tr class="even">
<td align="left"><p>RegisterSubdevice</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregistersubdevice" data-raw-source="[&lt;strong&gt;PcRegisterSubdevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregistersubdevice)"><strong>PcRegisterSubdevice</strong></a></p></td>
<td align="left"><p>是</p></td>
</tr>
</tbody>
</table>

 

在某些情况下，更改量不会超过简单名称更改：在名称开头插入限定符 `Pc`，以指示函数是在 PortCls 中实现的。 但在其他情况下，除了函数名称外，自变量列表还发生了更改。 上表中的右列指示参数是否已更改。

在更改了这些参数的情况下，portcls. hconvert 中的宏会将过时 PortCls 函数的参数列出到新 PortCls 函数的等效参数中。 以下宏包含参数转换：

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

 

 





