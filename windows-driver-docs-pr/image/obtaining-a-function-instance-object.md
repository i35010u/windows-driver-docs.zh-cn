---
title: 获取函数实例对象
description: 获取函数实例对象
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11919d5c6a5721f48152fc2a436762a896b940a9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785199"
---
# <a name="obtaining-a-function-instance-object"></a>获取函数实例对象


WIA 微型驱动程序必须标识当前的硬件设备以及它正在其上运行的服务。 为了识别这些项，微型驱动程序将在运行时从函数发现服务获取函数实例对象，并读取设备属性。

若要使用函数发现 COM 接口，微型驱动程序代码必须包含 Windows Vista SDK 中提供的 *FunctionDiscovery* 主头文件，如下面的示例所示。

```cpp
//
// Web Services Function Discovery main header:
//
#include <FunctionDiscovery.h>
```

在初始化期间， [**IStiUSD：： Initialize**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-initialize) 方法可能会发生这种情况，微型驱动程序应查询函数发现以获取代表硬件设备的相应函数实例对象。 若要完成此查询，请使用以下过程 (和关联的代码示例) ：

### <a name="step-1-create-the-function-discovery-object"></a>步骤1：创建函数发现对象

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

### <a name="step-2-create-an-instance-collection-query-object"></a>步骤2：创建实例集合查询对象

```cpp
IFunctionInstanceCollectionQuery *pfiCollectionQuery = NULL;
pFunctionDiscovery->CreateInstanceCollectionQuery(FCTN_CATEGORY_PNP,
   NULL,
   FALSE,
   NULL,
   NULL,
   &pfiCollectionQuery);
```

### <a name="step-3-add-a-constraint-to-the-instance-collection-query-object-to-specify-the-pnpx-id-its-value-is-retrieved-with-istidevicecontrolgetmydeviceportname-as-the-query-constraint"></a><a href="" id="step-3--add-a-constraint-to-the-instance-collection-query-object-to-sp"></a>步骤3：将约束添加到实例集合查询对象，以指定 PNPX ID (其值是使用 IStiDeviceControl：： GetMyDevicePortName) 作为查询约束进行检索

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

### <a name="step-4-execute-the-query"></a>步骤4：执行查询

```cpp
IFunctionInstanceCollection *pfiCollection = NULL;
pfiCollectionQuery->Execute(&pfiCollection);
```

### <a name="step-5-retrieve-the-function-instance-object-that-is-returned"></a>步骤5：检索返回的函数实例对象

```cpp
//
// Function Instance object that represents our device instance
//
IFunctionInstance *pFunctionInstance;

pfiCollection->Item(0, &m_pFunctionInstance);
```

有关包含示例类 (CWSDDevice) 的声明的代码示例，请参阅 [获取函数实例对象的代码示例](code-example-for-obtaining-a-function-instance-object.md)。

 

