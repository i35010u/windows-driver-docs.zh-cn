---
title: UVC 扩展单元的示例应用程序
description: UVC 扩展单元的示例应用程序
ms.assetid: f900b0b1-3469-442f-8593-2094a0966d4a
keywords:
- 扩展单位 WDK USB 视频类，示例，示例应用程序
- 示例代码 WDK USB 视频类，UVC 扩展单位
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a661099f55e56e29e5802cd0f02c704f7ebc8c3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389216"
---
# <a name="sample-application-for-uvc-extension-units"></a>UVC 扩展单元的示例应用程序


本主题包含可用于支持扩展单位的示例应用程序代码。

应用程序通过使用访问接口**IKsTopologyInfo::CreateNodeInstance**调用后跟**QueryInterface**上获取所需的 COM API 的节点对象。 **IKsTopologyInfo**上记录接口[API 和参考目录](https://go.microsoft.com/fwlink/p/?linkid=27252)网站。

在应用程序源中，任意名为 TestApp.cpp 包括下面的代码。

此外包括 TestApp.cpp 中所示的代码[扩展单位支持自动更新事件](supporting-autoupdate-events-with-extension-units.md)。

```cpp
  // pUnkOuter is the unknown associated with the base filter
  hr = pUnkOuter->QueryInterface(__uuidof(IKsTopologyInfo), 
                               (void **) &pKsTopologyInfo);
  if (!SUCCEEDED(hr))
  {
        printf("Unable to obtain IKsTopologyInfo %x\n", hr);
 goto errExit;
  }

  hr = FindExtensionNode(pKsTopologyInfo,                                                                                                   
     GUID_EXTENSION_UNIT_DESCRIPTOR,
     &dwExtensionNode);
  if (FAILED(hr))
  {
        printf("Unable to find extension node : %x\n", hr);
 goto errExit;
  }

  hr = pKsTopologyInfo->CreateNodeInstance(
        dwExtensionNode, 
   __uuidof(IExtensionUnit), 
 (void **) &pExtensionUnit);
 if (FAILED(hr))
  {
        printf("Unable to create extension node instance : %x\n", hr);
 goto errExit;
  }

  hr = pExtensionUnit->get_PropertySize(1, &ulSize);
  if (FAILED(hr))
  {
        printf("Unable to find property size : %x\n", hr);
 goto errExit;
  }

  pbPropertyValue = new BYTE[ulSize];
  if (!pbPropertyValue)
  {
      printf("Unable to allocate memory for property value\n");
      goto errExit;
  }

  hr = pExtensionUnit->get_Property(1,ulSize, pbPropertyValue);
  if (FAILED(hr))
  {
      printf("Unable to get property value\n");
      goto errExit;
  }
 
  // assume the property value is an integer
  ASSERT(ulSize == 4);
  printf("The value of property 1 = %d\n", *((int *) 
     pbPropertyValue));
```

在这种情况下， **pUnkOuter**应是指向表示 USB 视频类 (UVC) 设备捕获筛选器。 将捕获筛选器添加到筛选器关系图后，可以查询的筛选器**IKsTopologyInfo**接口，在此示例代码所示。

为编写代码**FindExtensionNode**函数来查找必要的扩展单元节点并返回其 ID 在*dwExtensionNode*。 在此示例代码的后续调用中使用此 ID **IKsTopologyInfo::CreateNodeInstance**方法。

 

 




