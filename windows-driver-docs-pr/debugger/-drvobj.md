---
title: drvobj
description: Drvobj 扩展显示有关 DRIVER_OBJECT 的详细信息。
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
ms.openlocfilehash: 7b79700500ccbfea5908e20b303fcd776e2a063f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817037"
---
# <a name="drvobj"></a>!drvobj


**！ Drvobj** 扩展显示有关驱动程序对象的详细信息 \_ 。

```dbgcmd
!drvobj DriverObject [Flags] 
```

## <a name="span-idddk__drvobj_dbgspanspan-idddk__drvobj_dbgspanparameters"></a><span id="ddk__drvobj_dbg"></span><span id="DDK__DRVOBJ_DBG"></span>参数


<span id="_______DriverObject______"></span><span id="_______driverobject______"></span><span id="_______DRIVEROBJECT______"></span>*DriverObject*   
指定驱动程序对象。 这可以是驱动程序对象结构的十六进制地址 \_ 或驱动程序的名称。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*标志*   
可以是以下位的任意组合。  (默认值为0x01。 ) 

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)   
使显示包含驱动程序所拥有的设备对象。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)   
使显示内容包括驱动程序的调度例程的入口点。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>位 2 (0x4)   
包含驱动程序所拥有的设备对象的详细信息的列表 (要求使用 0 (0x1) # A3。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Kdexts.dll


### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

请参阅 [即插即用调试](plug-and-play-debugging.md) ，了解此扩展命令的示例和应用程序。 有关驱动程序对象的信息，请参阅 Windows 驱动程序工具包 (WDK) 文档和 *Microsoft Windows 内部机制* ，Mark Russinovich 和 David 所罗门群岛。

## <a name="remarks"></a>备注
-------

如果 *DriverObject* 指定设备的名称，但未提供前缀， \\ \\ 则假定为前缀 "Driver"。 请注意，在使用表达式计算器之前，此命令将检查 *DriverObject* 是否为有效的地址或设备名称。

如果 *DriverObject* 是一个地址，则它必须是驱动程序 \_ 对象结构的地址。 这可以通过检查传递到驱动程序的 **DriverEntry** 例程的参数来获得。

此扩展命令将显示指定驱动程序创建的所有设备对象的列表。 它还将显示注册到此驱动程序对象的所有快速 i/o 例程。

下面是 Symbios 逻辑 810 SCSI 微型端口驱动程序的示例：

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

你还可以使用 [**！ devobj 809d50d0**](-devobj.md) 获取有关设备对象的信息。

 

 





