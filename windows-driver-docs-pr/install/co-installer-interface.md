---
title: 辅助安装程序界面
description: 辅助安装程序界面
ms.assetid: affcf2a5-5dbb-49bd-916c-bc99302b5bd8
keywords:
- 共同安装程序 WDK 设备安装，接口
- 接口 WDK 共同安装程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1eafe9d061dbffd91c29910e7f6ea3bf3db547c5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375327"
---
# <a name="co-installer-interface"></a>辅助安装程序界面


Co-安装程序的接口包含已导出的入口点函数和关联的数据结构。

### <a href="" id="co-installer-entry-point"></a> 辅助安装程序入口点

辅助安装程序必须导出某个入口点函数具有以下原型：

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
指定设备安装处理的请求，其中辅助安装程序具有的参与选项。 这些请求是使用 DIF 代码 （如 DIF_INSTALLDEVICE） 指定的。 有关详细信息，请参阅[设备安装函数代码](https://docs.microsoft.com/previous-versions/ff541307(v=vs.85))。

<a href="" id="deviceinfoset"></a>*DeviceInfoSet*  
提供的句柄[设备信息集](device-information-sets.md)。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
（可选） 标识的设备安装请求的目标设备。 如果此参数为非**NULL**，它标识设备信息元素中的设备信息集。 *DeviceInfoData*为非**NULL**时[ **SetupDiCallClassInstaller** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicallclassinstaller)调用特定于设备的共同安装程序。 可以使用具有一个 DIF 请求调用的特定于类共同安装程序 **NULL * * * DeviceInfoData*，例如 DIF_DETECT 或 DIF_FIRSTTIMESETUP。

<a href="" id="context"></a>*上下文*  
指向[ **COINSTALLER_CONTEXT_DATA** ](#coinstaller-context-data)结构。

设备共同安装程序将返回以下值之一：

<a href="" id="no-error"></a>NO_ERROR  
辅助安装程序为指定执行相应的措施*InstallFunction*，或者辅助安装程序确定不需要执行任何操作请求。

如果收到无法识别的 DIF 代码，辅助安装程序也必须返回 NO_ERROR。 （请注意类安装程序无法识别 DIF 代码返回 ERROR_DI_DO_DEFAULT。）

<a href="" id="error-di-postprocessing-required"></a>ERROR_DI_POSTPROCESSING_REQUIRED  
辅助安装程序执行任何适当的操作为指定*InstallFunction*并请求要在类安装程序处理完请求之后再次调用。

<a href="" id="a-win32-error"></a>*Win32 错误*  
辅助安装程序遇到错误。

辅助安装程序不会设置 ERROR_DI_DO_DEFAULT 返回状态。 此状态仅类安装程序使用。 如果共同安装程序将返回此状态，请**SetupDiCallClassInstaller**不会处理 DIF_*Xxx*正确请求。 共同安装程序可能会*传播*返回状态为 ERROR_DI_DO_DEFAULT 在其后续处理阶段中，但永远不会*设置*此值。

### <a href="" id="coinstaller-context-data"></a> COINSTALLER_CONTEXT_DATA

COINSTALLER_CONTEXT_DATA 是描述安装请求的共同 installer 特定的上下文结构。 结构的格式为：

```cpp
typedef struct 
  _COINSTALLER_CONTEXT_DATA {
      BOOLEAN  PostProcessing;
      DWORD    InstallResult;
      PVOID    PrivateData;
  } COINSTALLER_CONTEXT_DATA, *PCOINSTALLER_CONTEXT_DATA;
```

以下列表介绍了此结构的成员：

-   **后续处理**是**TRUE**当共同安装程序后调用适当的类安装程序中，如果任何，已处理指定的 DIF 代码*InstallFunction*。 **后续处理**是只读的辅助安装程序。

-   如果**后续处理**是**FALSE**， **InstallResult**不相关。 如果**后续处理**是**TRUE**， **InstallResult**是安装请求的当前状态。 此值为 NO_ERROR 或错误状态返回为此调用前一组件的安装请求。 辅助安装程序可通过返回其函数返回时，此值将传播状态或它可以返回另一个状态。 **InstallResult**是只读的辅助安装程序。

-   **PrivateData**指向共同 installer 分配的缓冲区。 如果共同安装程序将设置此指针和后续处理，请求**SetupDiCallClassInstaller**时它调用共同安装程序的后续处理将指针传递到共同安装程序。

 

 





