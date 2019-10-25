---
title: 获取特定错误源的错误源信息
description: 获取特定错误源的错误源信息
ms.assetid: 9979d654-8214-4e2d-9c6e-fc29a7f4ab40
keywords:
- 错误源 WDK WHEA，获取信息
- 错误 WDK WHEA，错误源
- WHEA WDK，获取错误源信息
- Windows 硬件错误体系结构 WDK，获取错误源信息
- 硬件错误源 WDK WHEA，获取信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 80bc564e6ed5e86556756bea5490480997df10e6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844421"
---
# <a name="getting-error-source-information-for-a-specific-error-source"></a>获取特定错误源的错误源信息


用户模式应用程序可以通过调用[**WHEAErrorSourceMethods：： GetErrorSourceInfoRtn**](https://docs.microsoft.com/windows-hardware/drivers/ddi/_whea/)方法获取有关硬件平台支持的特定[错误源](hardware-errors-and-error-sources.md)的信息。 此方法返回描述指定错误源的[**WHEA\_错误\_源\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_error_source_descriptor)结构。

下面的代码示例演示如何获取特定错误源的错误源信息。

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

 

 




