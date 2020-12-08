---
title: devobj
description: Devobj 扩展显示 DEVICE_OBJECT 结构的详细信息。
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
ms.openlocfilehash: ee950d4811ae551a81a02b044ce40ecedc17f66b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805913"
---
# <a name="devobj"></a>!devobj


**！ Devobj** 扩展显示有关设备对象结构的详细信息 \_ 。

```dbgcmd
!devobj DeviceObject 
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______DeviceObject______"></span><span id="_______deviceobject______"></span><span id="_______DEVICEOBJECT______"></span>*DeviceObject*   
指定设备对象。 这可以是此结构的十六进制地址或设备的名称。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

请参阅 [即插即用调试](plug-and-play-debugging.md) ，了解此扩展命令的示例和应用程序。 有关设备对象的信息，请参阅 Windows 驱动程序工具包 (WDK) 文档和 *Microsoft Windows 内部机制* ，Mark Russinovich 和 David 所罗门群岛。

<a name="remarks"></a>备注
-------

如果 *DeviceObject* 指定设备的名称，但未提供前缀， \\ \\ 则假定为前缀 "device"。 请注意，在使用表达式计算器之前，此命令将检查 *DeviceObject* 是否为有效的地址或设备名称。

显示的信息包括对象的设备名称、有关设备的当前 IRP 的信息以及设备队列中任何挂起的 Irp 的地址列表。 它还包括有关在此对象顶层分层的设备对象 (列出为 "AttachedDevice" ) 的信息，以及此对象下的分层的信息 (列为 "AttachedTo" ) 。

可以使用 [**！ drvobj**](-drvobj.md) 或 [**！ devnode**](-devnode.md) 扩展来获取设备对象的地址。

其中一个示例如下：

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

 

 





