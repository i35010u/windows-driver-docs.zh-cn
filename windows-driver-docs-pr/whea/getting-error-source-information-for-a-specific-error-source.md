---
title: 获取特定错误源的错误源信息
description: 获取特定错误源的错误源信息
ms.assetid: 9979d654-8214-4e2d-9c6e-fc29a7f4ab40
keywords:
- 错误源 WDK WHEA，获取信息
- 错误 WDK WHEA，错误源
- WHEA WDK，获取错误的源代码信息
- Windows 硬件错误体系结构 WDK，获取错误的源代码信息
- 硬件错误源 WDK WHEA，获取信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba1322c3e352a31377af83d55635d1698ec7cf1f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568860"
---
# <a name="getting-error-source-information-for-a-specific-error-source"></a>获取特定错误源的错误源信息


在用户模式应用程序可以获取有关特定的信息[错误源](hardware-errors-and-error-sources.md)支持的硬件平台通过调用[ **WHEAErrorSourceMethods::GetErrorSourceInfoRtn**](https://msdn.microsoft.com/library/windows/hardware/ff559530)方法。 此方法返回[ **WHEA\_错误\_源\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff560505)描述指定的错误源的结构。

下面的代码示例演示如何获取特定的错误源的错误源信息。

```cpp
IWbemServices *pIWbemServices;
ULONG ErrorSourceID;
BSTR ClassName;
BSTR MethodName;
HRESULT Result;
IWbemClassObject *pClass;
IWbemClassObject *pInParametersClass;
IWbemClassObject *pInParameters;
IWbemClassObject *pOutParameters;
VARIANT Parameter;
ULONG Status;
ULONG Length;
SAFEARRAY *Array;
PWHEA_ERROR_SOURCE_DESCRIPTOR ErrorSourceInfo;

// The following example assumes that the application
// has previously connected to WMI on the local machine
// and that the pIWbemServices variable contains the
// pointer that was returned from the call to the
// IWbemLocator::ConnectServer method.

// The following also assumes that the ErrorSourceID
// variable has previously been initialized with the
// identifier of the error source to be queried.

// Specify the class and method to execute
ClassName = SysAllocString(L"WHEAErrorSourceMethods");
MethodName = SysAllocString(L"GetErrorSourceInfoRtn");

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

// Set the ErrorSourceId parameter
Parameter.vt = VT_UI4;
Parameter.ulVal = ErrorSourceId;
Result =
  pInParameters->Put(
    L"ErrorSourceId",
    0,
    &Parameter,
    0
    );
VariantClear(&Parameter);

// Call the GetErrorSourceInfoRtn method indirectly
// by calling the IWbemServices::ExecMethod method.
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
VariantClear(&Parameter);

// Get the length from the output parameters object
Result =
  pOutParameters->Get(
    L"Length",
    0,
    &Parameter,
    NULL,
    NULL
    );
Length = Parameter.ulval;
VariantClear(&Parameter);

// Get the data buffer from the output parameters object
Result =
  pOutParameters->Get(
    L"ErrorSourceInfo",
    0,
    &Parameter,
    NULL,
    NULL
    );
Array = Parameter.parray;

// Get access to the data buffer
Result =
  SafeArrayAccessData(
    Array,
    &ErrorSourceInfo
    );

// Process the error source information.
...

// If the error source information is to be saved
// for later use, the data in the ErrorSourceInfo
// structure must be copied to an application-allocated
// WHEA_ERROR_SOURCE_DESCRIPTOR structure before
// freeing up the resources.
...

// Free the array containing the error source information
SafeArrayUnaccessData(Array);
VariantClear(&Parameter);

// Free up resources
SysFreeString(ClassName);
SysFreeString(MethodName);
pInParameters->Release();
pInParametersClass->Release();
pClass->Release();
pOutParameters->Release();
```

 

 




