---
title: 注入硬件错误
description: 注入硬件错误
keywords:
- 注入硬件错误 WDK WHEA
- 错误 WDK WHEA，注入，WHEA WDK，注入
- Windows 硬件错误体系结构 WDK，注入
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 021dc8808a1d92165b79934b092fb6c96d3c67ba
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837597"
---
# <a name="injecting-a-hardware-error"></a>注入硬件错误


用户模式应用程序可以通过调用 [**WHEAErrorInjectionMethods：： InjectError**](/windows-hardware/drivers/ddi/_whea/) 方法将硬件错误注入硬件平台。 应用程序将硬件错误注入硬件平台，以测试和验证系统的硬件错误处理功能。

下面的代码示例演示如何注入硬件错误。

```cpp
IWbemServices *pIWbemServices;
ULONG ErrorType;
BSTR ClassName;
BSTR MethodName;
HRESULT Result;
IWbemClassObject *pClass;
IWbemClassObject *pInParametersClass;
IWbemClassObject *pInParameters;
IWbemClassObject *pOutParameters;
VARIANT Parameter;
ULONG Status;

// The following example assumes that the application
// has previously connected to WMI on the local machine
// and that the pIWbemServices variable contains the
// pointer that was returned from the call to the
// IWbemLocator::ConnectServer method.

// The following also assumes that ErrorType has
// previously been initialized with the type of error
// to be injected into the hardware platform.

// Specify the class and method to execute
ClassName = SysAllocString(L"WHEAErrorInjectionMethods");
MethodName = SysAllocString(L"InjectErrorRtn");

// Get the class object for the method definition
Result =
  pIWbemServices->GetObject(
    ClassName,
    0,
    NULL,
    &pClass,
    NULL
    );

// Get the input parameter class object for the method
Result =
  pClass->GetMethod(
    MethodName,
    0,
    &pInParametersClass,
    NULL
    );

// Create an instance of the input parameter class
Result =
  pInParametersClass->SpawnInstance(
    0,
    &pInParameters
    );

// Set the ErrorType parameter
Parameter.vt = VT_UI4;
Parameter.ulVal = ErrorType;
Result =
  pInParameters->Put(
    L"ErrorType",
    0,
    &Parameter,
    0
    );
VariantClear(&Parameter);

// Set the additional parameters - in this case
// they are all set to zero. If additional data
// is required by the PSHED plug-in to perform
// the error injection operation, these parameters
// should be set with the necessary data.
Parameter.vt = VT_UI8;
Parameter.ullVal = (ULONGLONG)0;
Result =
  pInParameters->Put(
    L"Parameter1",
    0,
    &Parameter,
    0
    );
Result =
  pInParameters->Put(
    L"Parameter2",
    0,
    &Parameter,
    0
    );
Result =
  pInParameters->Put(
    L"Parameter3",
    0,
    &Parameter,
    0
    );
Result =
  pInParameters->Put(
    L"Parameter4",
    0,
    &Parameter,
    0
    );
VariantClear(&Parameter);

// Call the InjectErrorRtn method indirectly by
// calling the IWbemServices::ExecMethod method.
Result =
  pIWbemServices->ExecMethod(
    ClassName,
    MethodName,
    0,
    NULL,
    &pInParameters,
 &pOutParameters,
    NULL
    );

// For injected errors that are fatal or otherwise
// unrecoverable, the call to the InjectErrorRtn method
// might not return before the Windows kernel generates
// a bug check in response to the error condition.

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

// Free up resources
SysFreeString(ClassName);
SysFreeString(MethodName);
pInParameters->Release();
pInParametersClass->Release();
pClass->Release();
pOutParameters->Release();
```

 

