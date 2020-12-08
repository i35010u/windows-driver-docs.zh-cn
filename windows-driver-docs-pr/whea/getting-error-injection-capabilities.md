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
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc4e1325519c498f7d943852677ce1eb41799dca
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802099"
---
# <a name="getting-error-injection-capabilities"></a>获取错误注入功能


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
Status = Parameter.ulval;
VariantClear(Parameter);

// Get the capabilities from the output parameters object
Result =
  pOutParameters->Get(
    L"Capabilities",
    0,
    &Parameter,
    NULL,
    NULL
    );
ErrorInjectionCapabilities.AsULONG = Parameter.ulval;
VariantClear(Parameter);

// Process the error injection capabilities data
...

// Free up resources
SysFreeString(ClassName);
SysFreeString(MethodName);
pOutParameters->Release();
```

 

