---
title: UVC 扩展单元的示例应用程序
description: UVC 扩展单元的示例应用程序
ms.assetid: f900b0b1-3469-442f-8593-2094a0966d4a
keywords:
- 扩展单元-WDK USB 视频类、示例、示例应用程序
- 示例代码 WDK USB 视频类，UVC 扩展单元
ms.date: 06/18/2020
ms.localizationpriority: medium
ms.openlocfilehash: 11374359c3942363623aa1c1d4f9f010af477913
ms.sourcegitcommit: 17c1bbc5ea0bef3bbc87794b030a073f905dc942
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88802789"
---
# <a name="sample-application-for-uvc-extension-units"></a>UVC 扩展单元的示例应用程序

本主题包含可用于支持扩展单元的示例应用程序代码。

应用程序通过使用 [**IKsTopologyInfo：： CreateNodeInstance**](https://docs.microsoft.com/previous-versions/windows/win32/api/Vidcap/nf-vidcap-ikstopologyinfo-createnodeinstance) ，然后调用节点对象上的 **QueryInterface** 以获取所需的 COM API 来访问接口。 有关详细信息，请参阅 [**IKsTopologyInfo**](https://docs.microsoft.com/previous-versions/windows/win32/api/Vidcap/nn-vidcap-ikstopologyinfo)。

在应用程序源中包含名为 TestApp 的以下代码。

还包括在 TestApp 中所示的代码， [支持带有扩展单元的自动更新事件](supporting-autoupdate-events-with-extension-units.md)。

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

在这种情况下， **pUnkOuter** 应为指向捕获筛选器的指针，该指针表示) 设备 (UVC 的 USB 视频类。 将捕获筛选器添加到筛选器关系图后，可以查询 **IKsTopologyInfo** 接口的筛选器，如下面的示例代码所示。

编写 **FindExtensionNode** 函数的代码以查找必需的扩展单元节点并在 *dwExtensionNode*中返回其 ID。 此 ID 在此示例代码中对 **IKsTopologyInfo：： CreateNodeInstance** 方法的后续调用中使用。
