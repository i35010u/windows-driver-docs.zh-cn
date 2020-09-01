---
title: 定义回调对象示例
description: 定义回调对象示例
ms.assetid: d987bb95-cbee-46aa-beaf-167572ca4a80
keywords:
- 回叫对象 WDK UMDF，定义示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aba8ea2b27ce426a5eb19f68b5b2061accef4b09
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191581"
---
# <a name="defining-callback-objects-example"></a>定义回调对象示例


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

下面的代码示例演示驱动程序如何从 [IPnpCallbackHardware](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallbackhardware) 接口继承以定义设备回调对象。

```cpp
class CMyDevice :
       // Callback interface exposed to the framework
       public IPnpCallbackHardware 
{// The following data members make up the context
private:
   HANDLE                  m_CompletionPort;
   WINUSB_INTERFACE HANDLE m_UsbHandle;
   UCHAR                   m_BulkOutPipe;
   ULONG                   m_BulkOutMaxPacket;
   ...
// The following methods make up the callback interfaces
public:
    virtual HRESULT stdcall OnPrepareHardware( 
                              IWDFDevice* pDevice
                              );
    STDMETHOD( OnReleaseHardware )( IWDFDevice *pDevice );

   // Method used to create a device callback object
   static HRESULT CreateInstance( 
                     IUnknown **ppUnknown, 
                     IWDFDeviceInitialize *pDeviceInit,
                     HANDLE CompletionPort 
                     );
   ...
};
```

 

