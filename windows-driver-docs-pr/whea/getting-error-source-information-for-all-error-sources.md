---
title: 获取所有错误源的错误源信息
description: 获取所有错误源的错误源信息
keywords:
- 错误源 WDK WHEA，获取信息
- 错误 WDK WHEA，错误源
- WHEA WDK，获取错误源信息
- Windows 硬件错误体系结构 WDK，获取错误源信息
- 硬件错误源 WDK WHEA，获取学生
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5121192597584963cc02b9c0e8b2c59d208971d0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811311"
---
# <a name="getting-error-source-information-for-all-error-sources"></a>获取所有错误源的错误源信息


用户模式应用程序可以通过调用 [**WHEAErrorSourceMethods：： GetAllErrorSourcesRtn**](/windows-hardware/drivers/ddi/_whea/)方法获取有关系统中所有 [错误源](hardware-errors-and-error-sources.md)的信息。 此方法返回一个 [**WHEA \_ 错误 \_ 源 \_ 描述符**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_error_source_descriptor) 结构的数组，这些结构描述硬件平台支持的所有错误源。

下面的代码示例演示如何获取系统中所有错误源的错误源信息。

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

 

