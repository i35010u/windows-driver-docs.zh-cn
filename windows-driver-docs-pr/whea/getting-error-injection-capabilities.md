---
title: 获取错误注入功能
description: 获取错误注入功能
keywords:
- 错误注入功能 WDK WHEA
- 检索错误注入功能 WDK WHEA
- 错误 WDK WHEA，错误注入
- WHEA WDK，错误注入
- Windows 硬件错误体系结构 WDK，错误注入
- 注入硬件错误 WDK WHEA
ms.date: 03/01/2021
ms.localizationpriority: medium
ms.openlocfilehash: 0d36ef594b744174101b9811bd3053fb74ff49f5
ms.sourcegitcommit: ac28dd2a921c25796d19572a180b88e460420488
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/02/2021
ms.locfileid: "101682242"
---
# <a name="getting-error-injection-capabilities"></a>获取错误注入功能

> [!NOTE]
> WHEA 错误注入接口要求具有 EINJ ACPI 表的计算机或实现 [错误注入功能区域](./error-injection.md)的 PSHED Plug-In。 大多数消费者系统不包括 EINJ 实现，并且 Windows 没有内置的 PSHED Plug-In 来启用错误注入。 对于这两种情况，错误注入接口都将返回错误。

用户模式应用程序可以通过调用 [**WHEAErrorInjectionMethods：： GetErrorInjectionCapabilitiesRtn**](/windows-hardware/drivers/ddi/_whea/) 方法获取有关硬件平台的错误注入功能的信息。 此方法返回一个 [**WHEA \_ 错误 \_ 注入 \_ 功能**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_error_injection_capabilities) 结构，该结构描述硬件平台支持的错误注入功能。

下面的代码示例演示如何检索错误注入功能信息。

```cpp
IWbemServices *pIWbemServices;
BSTR ClassName;
BSTR MethodName;
HRESULT Result;
IWbemClassObject *pOutParameters;
VARIANT Parameter;
ULONG Status;
WHEA_ERROR_INJECTION_CAPABILITIES ErrorInjectionCapabilities;

// The following example assumes that the application
// has previously connected to WMI on the local machine
// and that the pIWbemServices variable contains the
// pointer that was returned from the call to the
// IWbemLocator::ConnectServer method.

// Specify the class and method to execute
ClassName = SysAllocString(L"WHEAErrorInjectionMethods");
MethodName = SysAllocString(L"GetErrorInjectionCapabilitiesRtn");

// Call the GetErrorInjectionCapabilitiesRtn method indirectly
// by calling the IWbemServices::ExecMethod method.
Result =
  pIWbemServices->ExecMethod(
    ClassName,
    MethodName,
    0,
    NULL,
    NULL,
    &pOutParameters,
    NULL
    );

// Get the status from the output parameters object
Result =
  pOutParameters->Get(
    L"Status",
    0,
    &Parameter,
    NULL,
    NULL
    );
Status = Parameter.ulVal;
VariantClear(&Parameter);

// Get the capabilities from the output parameters object
Result =
  pOutParameters->Get(
    L"Capabilities",
    0,
    &Parameter,
    NULL,
    NULL
    );
ErrorInjectionCapabilities.AsULONG = Parameter.ulVal;
VariantClear(&Parameter);

// Process the error injection capabilities data
...

// Free up resources
SysFreeString(ClassName);
SysFreeString(MethodName);
pOutParameters->Release();
```

 

