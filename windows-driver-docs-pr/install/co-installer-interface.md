---
title: 辅助安装程序界面
description: 辅助安装程序界面
keywords:
- 共同安装程序 WDK 设备安装，接口
- 接口 WDK 共同安装程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d668ec4dcf86f498846dfb0f8ba8b5d2f0d8cd0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783001"
---
# <a name="co-installer-interface"></a>辅助安装程序界面


共同安装程序的接口包含一个导出的入口点函数和一个关联的数据结构。

### <a name="co-installer-entry-point"></a><a href="" id="co-installer-entry-point"></a> 共同安装程序入口点

共同安装程序必须导出具有以下原型的入口点函数：

```cpp
typedef DWORD 
  (CALLBACK* COINSTALLER_PROC) (
    IN DI_FUNCTION  InstallFunction,
    IN HDEVINFO  DeviceInfoSet,
    IN PSP_DEVINFO_DATA  DeviceInfoData  OPTIONAL,
    IN OUT PCOINSTALLER_CONTEXT_DATA  Context
    );
```

<a href="" id="installfunction"></a>*InstallFunction*  
指定正在处理的设备安装请求，在该请求中，共同安装程序具有参与的选项。 这些请求是使用 DIF 代码（如 DIF_INSTALLDEVICE）指定的。 有关详细信息，请参阅 [设备安装功能代码](/previous-versions/ff541307(v=vs.85))。

<a href="" id="deviceinfoset"></a>*DeviceInfoSet*  
提供 [设备信息集](device-information-sets.md)的句柄。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
（可选）确定作为设备安装请求的目标的设备。 如果此参数为非 **NULL**，则它将标识设备信息集中的设备信息元素。 当 [**SetupDiCallClassInstaller**](/windows/win32/api/setupapi/nf-setupapi-setupdicallclassinstaller)调用设备特定的共同安装程序时， *DeviceInfoData* 为非 **NULL** 。 使用具有 **NULL**_DeviceInfoData_（如 DIF_DETECT 或 DIF_FIRSTTIMESETUP）的 DIF 请求可以调用类特定的共同安装程序。

<a href="" id="context"></a>*快捷*  
指向 [**COINSTALLER_CONTEXT_DATA**](#coinstaller-context-data) 结构。

设备共同安装程序返回下列值之一：

<a href="" id="no-error"></a>NO_ERROR  
共同安装程序针对指定的 *InstallFunction* 执行了相应的操作，或共同安装程序确定无需对请求执行任何操作。

如果辅助安装程序收到无法识别的 DIF 代码，还必须返回 NO_ERROR。  (请注意，类安装程序为无法识别的 DIF 代码返回 ERROR_DI_DO_DEFAULT。 ) 

<a href="" id="error-di-postprocessing-required"></a>ERROR_DI_POSTPROCESSING_REQUIRED  
共同安装程序针对指定的 *InstallFunction* 执行了任何适当的操作，并请求在类安装程序处理请求后再次调用。

<a href="" id="a-win32-error"></a>*Win32 错误*  
共同安装程序遇到错误。

共同安装程序不会将返回状态设置为 ERROR_DI_DO_DEFAULT。 此状态只能由类安装程序使用。 如果共同安装程序返回此状态， **SetupDiCallClassInstaller** 将不会正确处理 DIF_ *Xxx* 请求。 共同安装程序可能会将 ERROR_DI_DO_DEFAULT 的返回状态 *传播* 到其后处理过程中，但它永远不会 *设置* 此值。

### <a name="coinstaller_context_data"></a><a href="" id="coinstaller-context-data"></a> COINSTALLER_CONTEXT_DATA

COINSTALLER_CONTEXT_DATA 是描述安装请求的特定于安装程序的上下文结构。 结构的格式为：

```cpp
typedef struct 
  _COINSTALLER_CONTEXT_DATA {
      BOOLEAN  PostProcessing;
      DWORD    InstallResult;
      PVOID    PrivateData;
  } COINSTALLER_CONTEXT_DATA, *PCOINSTALLER_CONTEXT_DATA;
```

以下列表描述了此结构的成员：

-   如果在适当的类安装程序（如果有）处理了 *InstallFunction* 所指定的 DIF 代码，则在适当的类安装程序调用后，**后处理** 为 **TRUE** 。 **后处理** 对于共同安装程序是只读的。

-   如果 **后处理** 为 **FALSE**，则 **InstallResult** 不相关。 如果 **后处理** 为 **TRUE**，则 **InstallResult** 是安装请求的当前状态。 此值为 NO_ERROR 或以前的组件为此安装请求返回的错误状态。 共同安装程序可以通过为其函数返回返回此值来传播状态，也可以返回其他状态。 **InstallResult** 对共同安装程序是只读的。

-   **PrivateData** 指向由安装程序分配的一个缓冲区。 如果共同安装程序设置了此指针并请求后处理，则在调用共同安装程序进行后处理时， **SetupDiCallClassInstaller** 会将指针传递到共同安装程序。

 

