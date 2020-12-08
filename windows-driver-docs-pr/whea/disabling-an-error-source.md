---
title: 禁用错误源
description: 禁用错误源
keywords:
- 错误源 WDK WHEA，禁用
- Windows 硬件错误体系结构 WDK，禁用错误源
- WHEA WDK，禁用错误源
- 错误 WDK WHEA，禁用错误源
- 硬件错误源 WDK WHEA，禁用
- 禁用错误 sourc
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 098f5e37209610a1d5c03a97248a85c5021f586e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822681"
---
# <a name="disabling-an-error-source"></a>禁用错误源


用户模式应用程序可以通过调用 [**WHEAErrorSourceMethods：:D isableerrorsourcertn**](/windows-hardware/drivers/ddi/_whea/)方法来禁用 [错误源](hardware-errors-and-error-sources.md)。

下面的代码示例演示如何禁用错误源。

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

用户模式应用程序可以通过调用 [**WHEAErrorSourceMethods：： EnableErrorSourceRtn**](/windows-hardware/drivers/ddi/_whea/)方法重新启用 [错误源](hardware-errors-and-error-sources.md)。 有关如何启用错误源的详细信息，请参阅 [启用错误源](enabling-an-error-source.md)。

 

