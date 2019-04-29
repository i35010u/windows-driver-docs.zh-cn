---
title: UVC 扩展单元的示例接口
description: UVC 扩展单元的示例接口
ms.assetid: 898fdaf7-c3e1-4ef5-be4e-a5f9849ee905
keywords:
- 接口 WDK USB 视频类
- 扩展单位 WDK USB 视频类，示例中，接口
- 示例代码 WDK USB 视频类、 接口 UVC 扩展单位
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad74a5c6da9bff231e71318b18f52aecb946fbe2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389208"
---
# <a name="sample-interface-for-uvc-extension-units"></a>UVC 扩展单元的示例接口


本主题包含有关的示例代码*interface.idl*可用于支持扩展单元。

```IDL
// IExtensionUnit interface
import "unknwn.idl";
[
   object,
   local,
   uuid(yyyyyyyy-yyyy-yyyy-yyyy-yyyyyyyyyyyy),
   pointer_default(unique)
]
interface IExtensionUnit : IUnknown
{
   HRESULT get_InfoSize(
      [out] ULONG *pulSize);
   HRESULT get_Info(
      [in] ULONG ulSize,
      [in, out, size_is(ulSize)] BYTE pInfo[]);
   HRESULT get_PropertySize(
      [in] ULONG PropertyId,
      [out] ULONG *pulSize);
 HRESULT get_Property(
      [in] ULONG PropertyId,
      [in] ULONG ulSize,
      [in, out, size_is(ulSize)] BYTE pValue[]);
   HRESULT put_Property(
      [in] ULONG PropertyId,
      [in] ULONG ulSize,
      [in, out, size_is(ulSize)] BYTE pValue[]);
   HRESULT get_PropertyRange(
      [in] ULONG PropertyId,
      [in] ULONG ulSize,
      [in, out, size_is(ulSize)] BYTE pMin[],
      [in, out, size_is(ulSize)] BYTE pMax[],
      [in, out, size_is(ulSize)] BYTE pSteppingDelta[],
      [in, out, size_is(ulSize)] BYTE pDefault[]);
};
```

 

 




