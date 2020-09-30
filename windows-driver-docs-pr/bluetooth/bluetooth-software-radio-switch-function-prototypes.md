---
title: 蓝牙软件无线电开关函数原型
description: 了解以前的 windows 版本中的蓝牙版本和配置文件支持。 请参阅要求、建议和代码示例。
ms.assetid: A5A81EAA-0DC7-4725-AA0D-5C4867DDE47C
ms.date: 02/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: f1254083fc3c202660add7a34a13a93a44c3b15b
ms.sourcegitcommit: 2aedb606f9f14e74687f0d3da60e14fc6ffffa7e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/29/2020
ms.locfileid: "91544332"
---
# <a name="bluetooth-software-radio-switch-function-prototypes"></a>蓝牙软件无线电开关函数原型

> 注意：从开始 Windows 8.1 供应商不再需要按照本主题中所述的软件 DLL 中的蓝牙4.0 无线电) 实现无线电开/关功能 (，因为操作系统现在会处理此功能。 Windows 8.1 将忽略任何此类 DLL （即使存在）。

对于 Windows 8，蓝牙无线收发器必须支持软件开启/关闭功能。 为了使供应商能够获得最大的灵活性，蓝牙 Media 收音机管理器支持一个插件，允许向用户公开此功能。

若要提供此 DLL 插件，必须完成两项操作。

必须创作一个 DLL，以便导出正确的函数。必须在计算机上注册该 DLL。 DLL 负责保存无线电状态，包括跨系统重启，DLL 必须导出两个函数：

- BluetoothEnableRadio：收音机支持 DLL 实现 BluetoothEnableRadio，使 Windows 能够打开或关闭无线电。

```cpp
C++
DWORD WINAPI BluetoothEnableRadio(
   BOOL fEnable
);
```

fEnable：设置为 TRUE 将打开无线电电源。 如果设置为 FALSE，则关闭无线电电源。

返回值：如果当前状态更改为 fEnable 的状态，则返回 ERROR_SUCCESS。 否则，如果当前状态为 "未更改"，则返回 WIN32 错误代码。

- IsBluetoothRadioEnabled：收音机支持 DLL 实现 IsBluetoothRadioEnabled，使 Windows 能够确定无线电设备的电源是打开还是关闭。

```cpp
C++
DWORD WINAPI IsBluetoothRadioEnabled(
   BOOL* pfEnabled
);
```

pfEnabled：指向缓冲区的指针，用于描述无线电是打开还是关闭。

返回值：如果获取了当前状态，则返回 ERROR_SUCCESS。 PfEnabled 指向的值现在包含状态。  (true 或 false) 。 否则，如果未获取当前状态，将返回 WIN32 错误代码。 PfEnabled 指向的值是未定义的，不应使用

DLL 注册

若要启用菜单和控制面板小程序中的软件单选钮控制，必须注册此支持 DLL。 将以下注册表值设置为完整路径 (可能包括) 到相关 DLL 的环境变量。

密钥： HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Services\BTHPORT\Parameters\Radio 支持

值名称： "SupportDLL"

值数据： (路径) 

示例：

[HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Services\BTHPORT\Parameters\Radio 支持]

"SupportDLL" = "C： \\ Program Files \\ Fabrikam \\BthSupport.dll"

需要在安全位置（如 C:\Program Files\Fabrikam.）中安装 DLL。

## <a name="requirements-and-recommendations"></a>要求和建议

虽然这种设计在如何控制硬件方面具有灵活性，但 "关" 状态要求 "关闭" 不会导致无线传输/接收。 此外，建议将无线电关闭到其最低电源状态以节省能量，并将其从总线中删除，以便能够卸载蓝牙堆栈。

BluetoothEnableRadio 只应在无线电状态发生更改后返回结果。 此外，由于此 DLL 扩展旨在在 Windows 中提供统一的无线电开/关基础结构，因此应该为 Windows 组件保留 DLL 的使用情况。 如果非 Windows 组件也使用 DLL，则 DLL 负责确保返回正确的结果，或者，如果实现了可关闭蓝牙 Media 无线电管理器上下文外部的无线电的硬件开关 (例如，硬编码开关关闭收音机) 的电源。

Windows 8 收音机管理要求 DLL 在本地服务帐户上下文中执行其指令。 在这种情况下，DLL 将在本地计算机上具有最小特权，这通常小于普通用户上下文。

无线电支持 DLL 应执行相应的检查，以确保在执行任何操作之前其对应的硬件是否存在。 如果在系统上找不到相应的硬件，则无线电支持 DLL 应返回相应的错误代码。

## <a name="bluetooth-software-radio-sample-sources"></a>蓝牙软件无线电示例源

注册表文件

Windows 注册表编辑器版本 5.00

[HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Services\BthServ]

[HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Services\BthServ\Parameters]

[HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Services\BthServ\Parameters\Radio 支持]

"SupportDLL" = hex (2) ：25，00，73，00，79，00，73，00，74，00，65，00，6d，00，72，00，6f，00，6f，\

00，74，00，25，00，5c，00，73，00，79，00，73，00，74，00，65，00，6d，00，33，00，32，00，5c，00，\

72，00，73，00，75，00，70，00，70，00，6f，00，72，00，74，00，2e，00，64，00，6c，00，6c，00，00，\

00

MAKEFILE

```cpp
###### --------------------------------------------------------------------

######

###### Copyright(c) Microsoft Corp., 2012

######

###### --------------------------------------------------------------------

!ifdef NTMAKEENV

!INCLUDE $(NTMAKEENV)\makefile.def

!else # NTMAKEENV

!error - You forgot to set your build environment

!endif

RSupport.cpp

/*++ Copyright (c) Microsoft Corporation. All rights reserved.

THIS CODE AND INFORMATION IS PROVIDED "AS IS" WITHOUT WARRANTY OF ANY

KIND, EITHER EXPRESSED OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE

IMPLIED WARRANTIES OF MERCHANTABILITY AND/OR FITNESS FOR A PARTICULAR

PURPOSE.

Module Name:

Rsupport.cpp

Abstract:

--*/

DWORD WINAPI IsBluetoothRadioEnabled(BOOL* pfEnabled)

{

// If the radio is enabled, set *pfEnabled = TRUE else set *pfEnabled = FALSE

return ERROR_SUCCESS;

}

DWORD WINAPI BluetoothEnableRadio(BOOL fEnable)

{

if (fEnabled)

{

// Enable the radio here

}

else

{

// Disable the radio here

}

return ERROR_SUCCESS;

}

RSupport.def

/*++

Copyright (c) Microsoft Corporation. All rights reserved.

THIS CODE AND INFORMATION IS PROVIDED "AS IS" WITHOUT WARRANTY OF ANY

KIND, EITHER EXPRESSED OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE

IMPLIED WARRANTIES OF MERCHANTABILITY AND/OR FITNESS FOR A PARTICULAR

PURPOSE.

Module Name:

Rsupport.def

Abstract:

--*/

LIBRARY rsupport.dll

EXPORTS

BluetoothEnableRadio

IsBluetoothRadioEnabled

Sample SOURCES

#

# Copyright 2012 - Microsoft Corporation

#

TARGETNAME=rsupport

TARGETPATH=obj

TARGETTYPE=DYNLINK

UMTYPE=windows

USE_MSVCRT=1

TARGETLIBS= \

$(SDK_LIB_PATH)\kernel32.lib \

$(SDK_LIB_PATH)\user32.lib \

C_DEFINES=-DWIN32 -DUNICODE -D_UNICODE

SOURCES = RSupport.cpp
```
