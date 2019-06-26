---
title: 禁用错误源
description: 禁用错误源
ms.assetid: a481ac98-0ff1-4583-a81a-1d2e4f968111
keywords:
- 错误源 WDK WHEA，禁用
- Windows 硬件错误体系结构 WDK，禁用错误源
- WHEA WDK，禁用错误源
- 错误 WDK WHEA，禁用错误源
- 硬件错误源 WDK WHEA，禁用
- 禁用错误源代码
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8fddf8ae85f646b20b28ece20c801fae47678ebc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362595"
---
# <a name="disabling-an-error-source"></a>禁用错误源


在用户模式应用程序可以禁用[错误源](hardware-errors-and-error-sources.md)通过调用[ **WHEAErrorSourceMethods::DisableErrorSourceRtn** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_whea/)方法。

下面的代码示例显示了如何禁用错误源。

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

// The following example assumes that the application
// has previously connected to WMI on the local machine
// and that the pIWbemServices variable contains the
// pointer that was returned from the call to the
// IWbemLocator::ConnectServer method.

// The following also assumes that the ErrorSourceID
// variable has previously been initialized with the
// identifier of the error source to be disabled.

// Specify the class and method to execute
ClassName = SysAllocString(L"WHEAErrorSourceMethods");
MethodName = SysAllocString(L"DisableErrorSourceRtn");

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

// Call the DisableErrorSourceRtn method indirectly by
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

// Free up resources
SysFreeString(ClassName);
SysFreeString(MethodName);
pInParameters->Release();
pInParametersClass->Release();
pClass->Release();
pOutParameters->Release();
```

在用户模式应用程序可以重新启用[错误源](hardware-errors-and-error-sources.md)通过调用[ **WHEAErrorSourceMethods::EnableErrorSourceRtn** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_whea/)方法。 有关如何启用错误源的详细信息，请参阅[启用错误源](enabling-an-error-source.md)。

 

 




