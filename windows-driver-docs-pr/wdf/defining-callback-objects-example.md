---
title: 定义回调对象示例
description: 定义回调对象示例
ms.assetid: d987bb95-cbee-46aa-beaf-167572ca4a80
keywords:
- 回调对象 WDK UMDF，定义的示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac137549d3a37b54697f39adb2a0b60316dda46b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377461"
---
# <a name="defining-callback-objects-example"></a>定义回调对象示例


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

以下代码示例演示如何将驱动程序继承自[IPnpCallbackHardware](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-ipnpcallbackhardware)接口可定义设备回调对象。

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

 

 





