---
title: 获取所有错误源的错误源信息
description: 获取所有错误源的错误源信息
ms.assetid: 78e3a015-128d-44d1-b0ec-4da43c359090
keywords:
- 错误源 WDK WHEA，获取信息
- 错误 WDK WHEA，错误源
- WHEA WDK，获取错误的源代码信息
- Windows 硬件错误体系结构 WDK，获取错误的源代码信息
- 硬件错误源 WDK WHEA，获取了
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a021928b8b7bd6420443b5f3df96d0bcb41c6c1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340813"
---
# <a name="getting-error-source-information-for-all-error-sources"></a>获取所有错误源的错误源信息


在用户模式应用程序可以获取有关的所有信息[错误源](hardware-errors-and-error-sources.md)中通过调用系统[ **WHEAErrorSourceMethods::GetAllErrorSourcesRtn** ](https://msdn.microsoft.com/library/windows/hardware/ff559527)方法。 此方法返回的数组[ **WHEA\_错误\_源\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff560505)介绍的所有受支持的错误源的结构硬件平台。

下面的代码示例演示如何获取错误源信息的错误源的所有系统中。

```cpp
IWbemServices *pIWbemServices;
BSTR ClassName;
BSTR MethodName;
HRESULT Result;
IWbemClassObject *pOutParameters;
VARIANT Parameter;
ULONG Status;
ULONG Count;
ULONG Length;
SAFEARRAY *Array;
PWHEA_ERROR_SOURCE_DESCRIPTOR ErrorSourceList;

// The following example assumes that the application
// has previously connected to WMI on the local machine
// and that the pIWbemServices variable contains the
// pointer that was returned from the call to the
// IWbemLocator::ConnectServer method.

// Specify the class and method to execute
ClassName = SysAllocString(L"WHEAErrorSourceMethods");
MethodName = SysAllocString(L"GetAllErrorSourcesRtn");

// Call the GetAllErrorSourcesRtn method indirectly
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
VariantClear(&Parameter);

// Get the count from the output parameters object
Result =
  pOutParameters->Get(
    L"Count",
    0,
    &Parameter,
    NULL,
    NULL
    );
Count = Parameter.ulval;
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
    L"ErrorSourceArray",
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
    &ErrorSourceList
    );

// Process the error source information.
...

// If the error source information is to be saved
// for later use, the data in the ErrorSourceList
// array must be copied to an application-allocated
// array of WHEA_ERROR_SOURCE_DESCRIPTOR structures
// before freeing up the resources.
...

// Free the array containing the error source information
SafeArrayUnaccessData(Array);
VariantClear(&Parameter);

// Free up resources
SysFreeString(ClassName);
SysFreeString(MethodName);
pOutParameters->Release();
```

 

 




