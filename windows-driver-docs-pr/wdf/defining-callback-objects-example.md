---
title: 定义回调对象示例
description: 定义回调对象示例
keywords:
- 回叫对象 WDK UMDF，定义示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0afd1d33e3247a524713daf72af9beb3834c76fa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828979"
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

 

