---
title: devobj
description: Devobj 扩展显示有关 DEVICE_OBJECT 结构的详细的信息。
ms.assetid: cf722d95-fbd3-4d80-8679-f8fb348ab4b0
keywords:
- devobj Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- devobj
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 58357319ee5561ae646e9cb55c95b7064a0ba4b7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336809"
---
# <a name="devobj"></a>!devobj


**！ Devobj**扩展插件都会显示有关设备的详细的信息\_对象结构。

```dbgcmd
!devobj DeviceObject 
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______DeviceObject______"></span><span id="_______deviceobject______"></span><span id="_______DEVICEOBJECT______"></span> *DeviceObject*   
指定的设备对象。 这可以是十六进制此结构的地址或设备的名称。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

请参阅[插调试](plug-and-play-debugging.md)有关示例和应用程序的此扩展命令。 有关设备对象的信息，请参阅 Windows Driver Kit (WDK) 文档和*Microsoft Windows Internals*由 Mark Russinovich 和 David solomon 合著。

<a name="remarks"></a>备注
-------

如果*DeviceObject*指定的设备的名称，但提供没有前缀，前缀"\\设备\\"假定。 请注意，此命令将检查以查看是否*DeviceObject*表达式计算器在使用之前为有效的地址或设备名称。

显示的信息包括设备的队列中的对象、 有关设备的当前 IRP，设备名称和任何挂起的 Irp 的地址的列表。 它还包括有关设备对象之上 （列为"AttachedDevice"） 此对象和那些在此对象 （列为"附到"） 下分层信息。

可以使用获取的设备对象的地址[ **！ drvobj** ](-drvobj.md)或[ **！ devnode** ](-devnode.md)扩展。

下面是一个示例：

```dbgcmd
kd> !devnode
Dumping IopRootDeviceNode (= 0x80e203b8)
DevNode 0x80e203b8 for PDO 0x80e204f8
 Parent 0000000000   Sibling 0000000000   Child 0x80e56dc8
  InstancePath is "HTREE\ROOT\0"
  State = DeviceNodeStarted (0x308)
  Previous State = DeviceNodeEnumerateCompletion (0x30d)
  StateHistory[04] = DeviceNodeEnumerateCompletion (0x30d)
  StateHistory[03] = DeviceNodeStarted (0x308)
  StateHistory[02] = DeviceNodeEnumerateCompletion (0x30d)
  StateHistory[01] = DeviceNodeStarted (0x308)
  StateHistory[00] = DeviceNodeUninitialized (0x301)
  StateHistory[19] = Unknown State (0x0)
  .....
  StateHistory[05] = Unknown State (0x0)
  Flags (0x00000131)  DNF_MADEUP, DNF_ENUMERATED, 
                      DNF_IDS_QUERIED, DNF_NO_RESOURCE_REQUIRED
  DisableableDepends = 11 (from children)

kd> !devobj 80e204f8
Device object (80e204f8) is for:
  \Driver\PnpManager DriverObject 80e20610
Current Irp 00000000 RefCount 0 Type 00000004 Flags 00001000
DevExt 80e205b0 DevObjExt 80e205b8 DevNode 80e203b8 
ExtensionFlags (0000000000)  
Device queue is not busy.
```

 

 





