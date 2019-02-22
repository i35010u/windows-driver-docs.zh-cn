---
title: 获取函数实例对象
description: 获取函数实例对象
ms.assetid: 2c750281-031b-4b9f-9012-3b341ebe1cd9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 68243e112354ce8faeaf63dd41ddd1b814bb5eff
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541314"
---
# <a name="obtaining-a-function-instance-object"></a>获取函数实例对象


当前的硬件设备和服务上运行，必须标识 WIA 微型驱动程序。 若要标识这些项，微型驱动程序在运行时函数实例对象从获取该函数发现服务，并读取设备属性。

若要使用函数发现 COM 接口，微型驱动程序代码必须包括*FunctionDiscovery.h*主标头文件，位于 Windows Vista SDK，如以下示例所示。

```cpp
//
// Web Services Function Discovery main header:
//
#include <FunctionDiscovery.h>
```

在初始化期间，为可能发生这种情况中[ **IStiUSD::Initialize** ](https://msdn.microsoft.com/library/windows/hardware/ff543824)方法，微型驱动程序应查询函数查询，以获取相应的函数实例对象，表示硬件设备。 若要完成此查询，请使用以下过程 （和关联的代码示例）：

### <a name="step-1-create-the-function-discovery-object"></a>第 1 步：创建函数发现对象

```cpp
//
// Function Discovery object
//
IFunctionDiscovery *pFunctionDiscovery = NULL;
CoCreateInstance(__uuidof(FunctionDiscovery),
                 NULL,
                 CLSCTX_INPROC_SERVER,
                 __uuidof(IFunctionDiscovery),
  (void**)&pFunctionDiscovery);
```

### <a name="step-2-create-an-instance-collection-query-object"></a>步骤 2：创建实例集合查询对象

```cpp
IFunctionInstanceCollectionQuery *pfiCollectionQuery = NULL;
pFunctionDiscovery->CreateInstanceCollectionQuery(FCTN_CATEGORY_PNP,
   NULL,
   FALSE,
   NULL,
   NULL,
   &pfiCollectionQuery);
```

### <a href="" id="step-3--add-a-constraint-to-the-instance-collection-query-object-to-sp"></a>步骤 3:将作为查询约束的约束添加到实例集合查询对象来指定 PNPX ID （与 IStiDeviceControl::GetMyDevicePortName 检索其值）

```cpp
PROPVARIANT PropVar = {0};
//
// Note that the wszDevicePath value is obtained by the WIA minidriver 
// calling IStiDeviceControl::GetMyDevicePortName during IStiUSD::Initialize
//
PropVariantInit(&PropVar);
PropVar.vt = VT_LPWSTR;
PropVar.pwszVal = (LPWSTR)wszDevicePath; 
pfiCollectionQuery->AddPropertyConstraint(PKEY_PNPX_ID, &PropVar, QC_EQUALS);
```

### <a name="step-4-execute-the-query"></a>步骤 4：执行查询

```cpp
IFunctionInstanceCollection *pfiCollection = NULL;
pfiCollectionQuery->Execute(&pfiCollection);
```

### <a name="step-5-retrieve-the-function-instance-object-that-is-returned"></a>步骤 5：检索返回的函数实例对象

```cpp
//
// Function Instance object that represents our device instance
//
IFunctionInstance *pFunctionInstance;

pfiCollection->Item(0, &m_pFunctionInstance);
```

包含声明的示例类 (CWSDDevice) 的代码示例，请参阅[用于获取函数实例对象的代码示例](code-example-for-obtaining-a-function-instance-object.md)。

 

 




