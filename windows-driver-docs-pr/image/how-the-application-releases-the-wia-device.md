---
title: 应用程序如何释放 WIA 设备
description: 应用程序如何释放 WIA 设备
ms.assetid: 694daed4-d794-4835-a052-27cc498baa10
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f183d4e1b6996e6be4f6f9179e4449dbcc886b2f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567836"
---
# <a name="how-the-application-releases-the-wia-device"></a>应用程序如何释放 WIA 设备





当应用程序没有进一步的 WIA 设备的需要时，它将调用**IWiaItem::Release**方法 （Microsoft Windows SDK 文档中所述）。 发布到任何 WIA 项的最后一个引用时，WIA 服务调用[ **IWiaMiniDrv::drvUnInitializeWia** ](https://msdn.microsoft.com/library/windows/hardware/ff545010)方法。 WIA 微型驱动程序应使用此方法主要用于管理所有连接的应用程序与关联的资源。 当应用程序关闭时，不再需要其项树与关联的资源。 WIA 微型驱动程序应跟踪的所有连接的应用程序通过中的引用计数器递增[ **IWiaMiniDrv::drvInitializeWia** ](https://msdn.microsoft.com/library/windows/hardware/ff544986)和引用中计数器递减**IWiaMiniDrv::drvUnInitializeWia**。 在这种情况下释放资源可能会导致其他已连接的应用程序出现问题。 当引用计数器达到那里的零时没有更多的应用程序连接到 WIA 微型驱动程序。 微型驱动程序应清理在应用程序连接过程中获取所有已分配资源。

**请注意**  * * * **IWiaMiniDrv::drvUnInitializeWia**方法不会卸载该驱动程序。 该驱动程序可能会再次调用，以处理事件，或当应用程序要与之进行通信。 调用此方法并不意味着所有客户端已断开连接。 应该有一次调用每个客户端断开连接。
每次调用**IWiaMiniDrv::drvUnInitializeWia**方法应与相应地调用配对**IWiaMiniDrv::drvInitializeWia**方法。

WIA 驱动程序应*不*释放此方法调用中的任何驱动程序资源，它可以安全地确定，除非*没有*当前连接的应用程序。

若要确定当前的应用程序连接计数，WIA 驱动程序应增加一个类成员变量作为引用计数器来跟踪对方法调用**IWiaMiniDrv::drvInitializeWia** （递增计数器）并**IWiaMiniDrv::drvUnInitializeWia** （减少计数器）。

 

下面的示例演示的实现**IWiaMiniDrv::drvUnInitializeWia**方法。

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

 

 




