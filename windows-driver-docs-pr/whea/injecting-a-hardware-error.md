---
title: 注入硬件错误
description: 注入硬件错误
ms.assetid: c27c79d9-c0b2-433b-b3f4-7674c361f1aa
keywords:
- 注入硬件错误 WDK WHEA
- 错误 WDK WHEA，注入，WHEA WDK，注入
- Windows 硬件错误体系结构 WDK 注入
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3715863ceb38fb03afcb3d8a4cf0fc8b9c74e046
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340781"
---
# <a name="injecting-a-hardware-error"></a>注入硬件错误


在用户模式应用程序可以注入硬件错误的硬件平台通过调用[ **WHEAErrorInjectionMethods::InjectError** ](https://msdn.microsoft.com/library/windows/hardware/ff559518)方法。 应用程序将硬件错误注入测试和验证系统的硬件错误处理功能的硬件平台。

下面的代码示例演示如何插入硬件错误。

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

 

 




