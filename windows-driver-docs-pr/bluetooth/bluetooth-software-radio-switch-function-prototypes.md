---
title: 以前的 Windows 版本中的蓝牙版本和配置文件支持
description: 以前的 Windows 版本中的蓝牙版本和配置文件支持
ms.assetid: A5A81EAA-0DC7-4725-AA0D-5C4867DDE47C
ms.date: 02/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: ce02d9d590e14f1cbff085c8f403e6f83aca5306
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328247"
---
# <a name="bluetooth-software-radio-switch-function-prototypes"></a>蓝牙软件无线电开关函数原型

> 注意：从 Windows 8.1 开始供应商不再需要软件本主题中所述的 DLL 中实现功能 （适用于蓝牙 4.0 无线电收发器） 打开/关闭无线电，因为操作系统现在可处理此功能。 Windows 8.1 将忽略任何此类 DLL，即使存在。

对于 Windows 8，Bluetooth 无线电收发器必须支持打开/关闭功能的软件。 若要允许供应商最大的灵活性，蓝牙 Media 单选管理器支持插件以允许使用此功能以向用户公开。

若要提供此 DLL 插件，必须完成两件事情。

DLL 必须编写该导出必须在计算机注册的 DLL 的正确函数。 DLL 都负责保持单选状态，包括跨系统重新启动的 DLL 必须导出两个函数：

-    BluetoothEnableRadio:单选支持 DLL 实现 BluetoothEnableRadio 若要启用 Windows 以启用或禁用单选的电源。

```cpp
C++ 
DWORD WINAPI BluetoothEnableRadio(
   BOOL fEnable
);
``` 

fEnable:设置为 TRUE 以启用单选电源。 设置为 FALSE 来关闭单选电源。

返回值：如果当前状态更改为 fEnable 的状态，则返回 ERROR_SUCCESS。 如果未更改当前状态，否则，返回一个 WIN32 错误代码。

-    IsBluetoothRadioEnabled:单选支持 DLL 实现 IsBluetoothRadioEnabled 若要启用 Windows 来确定广播的电源是开还是关。

```cpp
C++ 
DWORD WINAPI IsBluetoothRadioEnabled(
   BOOL* pfEnabled
);
```
pfEnabled:如果电源的单选对于描述缓冲区的指针是开还是关。

返回值：如果在获取当前状态，则返回 ERROR_SUCCESS。 现在指向由 pfEnabled 的值包含状态。 （true 或 false）。 如果不获取的当前状态，否则，返回一个 WIN32 错误代码。 通过 pfEnabled 指向的值未定义，不应使用

DLL 注册

若要启用软件单选开关控件的菜单中和在控制控制面板小程序，必须注册此支持 DLL。 以下注册表值设置为 DLL 的完整路径 （可能包括环境变量） 有问题。

注册表项：HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\BTHPORT\Parameters\Radio Support

值名称："SupportDLL"

值数据: （路径）

例如：

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\BTHPORT\Parameters\Radio Support]

"SupportDLL"="C:\\Program Files\\Fabrikam\\BthSupport.dll"

它需要在一个安全位置，例如 C:\Program Files\Fabrikam 安装此 DLL。

要求和建议

尽管此设计允许灵活地可以如何控制硬件，也需要关闭状态，导致无线电设备发出的任何传输/接收。 此外，建议关闭其最低的电源状态，以节约能源并将其删除从总线单选允许蓝牙堆栈卸载。

单选状态的更改发生后，BluetoothEnableRadio 应只返回结果。 此外，因为此 DLL 扩展旨在提供统一的单选打开/关闭 Windows 的基础结构，则应该为 Windows 组件中保留的 dll 的使用情况。 它负责 DLL 以确保非 Windows 组件，还使用该 DLL 是否实现的硬件交换机返回正确的结果，可以关闭外部蓝牙媒体单选管理器的上下文 （例如交换机广播硬编码到关闭无线电）。

Windows 8 单选管理需要在本地服务帐户上下文中执行其指令的 DLL。 在此上下文中，DLL 将具有最小特权是通常小于正常用户上下文在本地计算机上。

单选支持 DLL 应执行相应的检查，以确保其相应的硬件在执行任何操作之前存在。 如果在系统上找不到相应的硬件，单选支持 DLL 应返回相应的错误代码。

## <a name="bluetooth-software-radio-sample-sources"></a>蓝牙软件无线电示例源
注册表文件

Windows Registry Editor 版本 5.00

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\BthServ]

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\BthServ\Parameters]

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\BthServ\Parameters\Radio Support]

"SupportDLL"=hex(2):25,00,73,00,79,00,73,00,74,00,65,00,6d,00,72,00,6f,00,6f,\

00,74,00,25,00、 5 c、 00、 73、 00、 79、 00、 73、 00、 74、 00、 65、 00、 d、 6 00、 33、 00、 32、 00、 5 c，00，\

72,00,73,00,75,00,70,00,70,00，6f，00、 72、 00、 74、 00，2e，00、 64、 00、 6 c、 00、 6 c、 00、 00，\

00


生成文件
```cpp
###### --------------------------------------------------------------------

######

###### Copyright(c) Microsoft Corp., 2012

######

###### --------------------------------------------------------------------
```

！ ifdef NTMAKEENV

!包括 $(NTMAKEENV)\makefile.def

！ else # NTMAKEENV

！ 错误-你忘记设置生成环境

！ endif 


RSupport.cpp

/ * + + 版权所有 （c) Microsoft Corporation。 保留所有权利。

此代码和信息是"按原样"提供的任何担保

类型、 明示的或默示保证，包括但不仅限于

有关适销性和/或针对特定的适用性的暗示的担保

目的。

模块名称：

Rsupport.cpp

Abstract:

--*/

DWORD WINAPI IsBluetoothRadioEnabled(BOOL* pfEnabled)

{

如果已启用，设置 * pfEnabled = TRUE 其他 set * pfEnabled = FALSE

返回 ERROR_SUCCESS;

}

DWORD WINAPI BluetoothEnableRadio(BOOL fEnable)

{

如果 (fEnabled)

{

启用单选此处

}

else

{

禁用单选此处

}

返回 ERROR_SUCCESS;

}


RSupport.def

/*++

版权所有 (c) Microsoft Corporation。 保留所有权利。

此代码和信息是"按原样"提供的任何担保

类型、 明示的或默示保证，包括但不仅限于

有关适销性和/或针对特定的适用性的暗示的担保

目的。

模块名称：

Rsupport.def

Abstract:

--*/

库 rsupport.dll

EXPORTS

BluetoothEnableRadio

IsBluetoothRadioEnabled 


示例源

#

# <a name="copyright-2012---microsoft-corporation"></a>Copyright 2012 - Microsoft Corporation

#

TARGETNAME=rsupport

TARGETPATH = obj

TARGETTYPE = DYNLINK

UMTYPE=windows

USE_MSVCRT=1

TARGETLIBS = \

$(SDK_LIB_PATH)\kernel32.lib \

$(SDK_LIB_PATH)\user32.lib \

C_DEFINES=-DWIN32 -DUNICODE -D_UNICODE

SOURCES = RSupport.cpp 




