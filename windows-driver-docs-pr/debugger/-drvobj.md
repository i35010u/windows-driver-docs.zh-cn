---
title: drvobj
description: Drvobj 扩展显示有关 DRIVER_OBJECT 详细的信息。
ms.assetid: 98f3cacf-311c-4000-8336-4964cc2cb9b0
keywords:
- drvobj Windows 调试
ms.date: 11/16/2018
topic_type:
- apiref
api_name:
- drvobj
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: dfebfb5d30d2005303cc2f6def4a297e733574e6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334540"
---
# <a name="drvobj"></a>!drvobj


**！ Drvobj**扩展显示有关驱动程序的详细的信息\_对象。

```dbgcmd
!drvobj DriverObject [Flags] 
```

## <a name="span-idddkdrvobjdbgspanspan-idddkdrvobjdbgspanparameters"></a><span id="ddk__drvobj_dbg"></span><span id="DDK__DRVOBJ_DBG"></span>参数


<span id="_______DriverObject______"></span><span id="_______driverobject______"></span><span id="_______DRIVEROBJECT______"></span> *DriverObject*   
指定的驱动程序对象。 这可以是驱动程序的十六进制地址\_对象结构或驱动程序的名称。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *标志*   
可以是以下位的任意组合。 （默认值为 0x01。）

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)  
将导致显示以包括驱动程序所拥有的设备对象。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)  
将导致显示以包括驱动程序的调度例程的入口点。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>位 2 (0x4)  
（需要位 0 (0x1)） 的驱动程序设备对象所拥有的详细信息的列表。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll


### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

请参阅[插调试](plug-and-play-debugging.md)有关示例和应用程序的此扩展命令。 有关驱动程序对象的信息，请参阅 Windows Driver Kit (WDK) 文档和*Microsoft Windows Internals*由 Mark Russinovich 和 David solomon 合著。

## <a name="remarks"></a>备注
-------

如果*DriverObject*指定的设备的名称，但提供没有前缀，前缀"\\驱动程序\\"假定。 请注意，此命令将检查以查看是否*DriverObject*表达式计算器在使用之前为有效的地址或设备名称。

如果*DriverObject*是一个地址，它必须是该驱动程序的地址\_对象结构。 这可以通过检查传递给驱动程序的参数来获取**DriverEntry**例程。

此扩展命令将显示创建的指定驱动程序的所有设备对象的列表。 它还将显示注册到此驱动程序对象的所有快速 I/O 例程。

下面是一个示例，用于 Symbios 逻辑 810 SCSI 微型端口驱动程序：

```dbgcmd
kd> bp DriverEntry          //  breakpoint at DriverEntry

kd> g
symc810!DriverEntry+0x40:    
80006a20: b07e0050 stl     t2,50(sp)

kd> r a0  //address of DevObj (the first parameter)
a0=809d5550

kd> !drvobj 809d5550   //  display the driver object
Driver object is for:
\Driver\symc810
Device Object list:
809d50d0
```

此外可以使用[ **！ devobj 809d50d0** ](-devobj.md)以获取有关设备对象的信息。

 

 





