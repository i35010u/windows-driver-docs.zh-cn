---
title: 应用程序如何释放 WIA 设备
description: 应用程序如何释放 WIA 设备
ms.assetid: 694daed4-d794-4835-a052-27cc498baa10
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 56cf85562128ad23f02b6efbd77f78a8562de52a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840833"
---
# <a name="how-the-application-releases-the-wia-device"></a>应用程序如何释放 WIA 设备





当应用程序不再需要 WIA 设备时，它将调用**IWiaItem：： Release**方法（如 Microsoft Windows SDK 文档中所述）。 发布对任何 WIA 项的最后一个引用时，WIA 服务将调用[**IWiaMiniDrv：:D rvuninitializewia**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvuninitializewia)方法。 WIA 微型驱动程序应主要使用此方法来管理与所有连接的应用程序关联的资源。 当应用程序关闭时，不再需要与其项树关联的资源。 WIA 微型驱动程序应通过在 IWiaMiniDrv 中递增引用计数器来跟踪所有连接的应用程序[ **：:D rvinitializewia**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinitializewia) ，并在**IWiaMiniDrv：:d rvuninitializewia**中递减该引用计数器。 此时释放资源可能会导致其他连接的应用程序出现问题。 如果引用计数器变为零，则没有其他应用程序连接到 WIA 微型驱动程序。 微型驱动程序应清除它在应用程序连接期间获取的任何分配资源。

**请注意**  * * * * **IWiaMiniDrv：:d rvuninitializewia**方法不会卸载驱动程序。 可以再次调用该驱动程序来处理事件，或在应用程序与之通信时进行处理。 对此方法的调用并不意味着所有客户端都已断开连接。 每个客户端断开连接应调用一次。
对**IWiaMiniDrv：:D rvuninitializewia**方法的每个调用都应与对**IWiaMiniDrv：:d rvinitializewia**方法的相应调用配对。

WIA 驱动程序*不*应释放此方法调用中的任何驱动程序资源，除非它能够安全地确定当前*没有任何*应用程序在连接。

为了确定当前应用程序连接计数，WIA 驱动程序应将类成员变量作为引用计数器递增，以跟踪对**IWiaMiniDrv：:D rvinitializewia** （递增计数器）和**IWiaMiniDrv：：drvUnInitializeWia** （递减计数器）。

 

下面的示例演示**IWiaMiniDrv：:D rvuninitializewia**方法的实现。

```cpp
HRESULT _stdcall CWIADevice::drvUnInitializeWia(BYTE *pWiasContext)
{
  //
  // If the caller did not pass in the correct parameters,
  // then fail the call with E_INVALIDARG.
  //

  if (!pWiasContext) {
      return E_INVALIDARG;
  }

  InterlockedDecrement(&m_lClientsConnected);

  //
  // make sure we never decrement below zero (0)
  //

  if(m_lClientsConnected < 0){
      m_lClientsConnected = 0;
  return S_OK;
  }

  //
  // check for connected applications.
  //

  if(m_lClientsConnected == 0){

      //
      // There are no application clients connected to this WIA driver
      //

  }

  return S_OK;
}
```

 

 




