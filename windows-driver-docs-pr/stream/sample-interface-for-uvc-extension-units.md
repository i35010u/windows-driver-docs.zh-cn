---
title: UVC 扩展单元的示例接口
description: UVC 扩展单元的示例接口
keywords:
- 接口 WDK USB 视频类
- 扩展单元-WDK USB 视频类，示例，接口
- 示例代码 WDK USB 视频类，UVC 扩展单元的接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c7d4df0d7615589ea552063bfc622ddabd2cee1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825867"
---
# <a name="sample-interface-for-uvc-extension-units"></a>UVC 扩展单元的示例接口


本主题包含可用于支持扩展单元的示例 *接口 .idl* 的代码。

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

 

 




