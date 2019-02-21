---
title: 设置错误源信息
description: 设置错误源信息
ms.assetid: 87c61c3e-768a-4784-b9ec-1ec85d65ea81
keywords:
- 错误源 WDK WHEA，设置信息
- 错误 WDK WHEA，错误源
- WHEA WDK，设置错误源信息
- Windows 硬件错误体系结构 WDK，设置错误源信息
- 硬件错误源 WDK WHEA，设置信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5fae1553ec7358460cca21634c1c0b25345ef079
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546665"
---
# <a name="setting-error-source-information"></a>设置错误源信息


在用户模式应用程序可以设置为特定的信息[错误源](hardware-errors-and-error-sources.md)支持的硬件平台通过调用[ **WHEAErrorSourceMethods::SetErrorSourceInfoRtn**](https://msdn.microsoft.com/library/windows/hardware/ff559531)方法。 在此情况下，该应用程序提供[ **WHEA\_错误\_源\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff560505)结构描述要为设置的信息指定的错误源。

下面的代码示例演示如何设置特定的错误源的错误源信息。

```cpp
IWbemServices *pIWbemServices;
WHEA_ERROR_SOURCE_DESCRIPTOR ErrorSourceInfo;
BSTR ClassName;
BSTR MethodName;
HRESULT Result;
IWbemClassObject *pClass;
IWbemClassObject *pInParametersClass;
IWbemClassObject *pInParameters;
IWbemClassObject *pOutParameters;
VARIANT Parameter;
SAFEARRAY *Array;
PVOID ArrayData;
ULONG Status;

// The following example assumes that the application
// has previously connected to WMI on the local machine
// and that the pIWbemServices variable contains the
// pointer that was returned from the call to the
// IWbemLocator::ConnectServer method.

// The following also assumes that the ErrorSourceInfo
// contains the error source information to be set.

// Note that the SetErrorSourceInfoRtn method determines
// the identifier of the error source for which the
// information is being set from the ErrorSourceId
// member of the WHEA_ERROR_SOURCE_DESCRIPTOR structure.

// Specify the class and method to execute
ClassName = SysAllocString(L"WHEAErrorSourceMethods");
MethodName = SysAllocString(L"SetErrorSourceInfoRtn");

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

// Create a safe array for the error source information
Array =
  SafeArrayCreateVector(
    VT_UI1,
    0,
    sizeof(WHEA_ERROR_SOURCE_DESCRIPTOR)
    );

// Get access to the data buffer
Result =
  SafeArrayAccessData(
    Array,
    &ArrayData
    );

// Copy the error source information
*(PWHEA_ERROR_SOURCE_DESCRIPTOR)ArrayData =
  ErrorSourceInfo;

// Release access to the data buffer
SafeArrayUnaccessData(Array);

// Set the ErrorSourceInfo parameter
Parameter.vt = VT_ARRAY | VT_UI1;
Parameter.parray = Array;
Result =
  pInParameters->Put(
    L"ErrorSourceInfo",
    0,
    &Parameter,
    0
    );
VariantClear(&Parameter);

// Set the Length parameter
Parameter.vt = VT_UI4;
Parameter.ulVal = sizeof(WHEA_ERROR_SOURCE_DESCRIPTOR);
Result =
  pInParameters->Put(
    L"Length",
    0,
    &Parameter,
    0
    );
VariantClear(&Parameter);

// Call the SetErrorSourceInfoRtn method indirectly
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

// Free up resources
SysFreeString(ClassName);
SysFreeString(MethodName);
pInParameters->Release();
pInParametersClass->Release();
pClass->Release();
pOutParameters->Release();
```

修改错误源的配置时，应用程序通常设置错误源的信息。 应用程序可以通过执行以下步骤来修改错误源的配置：

1.  检索 WHEA\_错误\_源\_描述符结构，描述特定错误源。

    有关如何获取有关的所有信息的详细信息[错误源](hardware-errors-and-error-sources.md)在系统中，请参阅[的所有错误源获取错误的源信息](getting-error-source-information-for-all-error-sources.md)。

    在系统中获得有关特定错误源的信息的详细信息，请参阅[特定的错误源获取错误的源信息](getting-error-source-information-for-a-specific-error-source.md)。

2.  修改内容 WHEA\_错误\_源\_描述符结构更改错误源的配置。

3.  通过调用设置错误源的错误源信息[ **WHEAErrorSourceMethods::SetErrorSourceInfoRtn** ](https://msdn.microsoft.com/library/windows/hardware/ff559531)方法

重新启动系统后，对错误源的配置进行任何更改才会生效之前。

 

 




