---
title: 定义回调对象示例
description: 定义回调对象示例
ms.assetid: d987bb95-cbee-46aa-beaf-167572ca4a80
keywords:
- 回调对象 WDK UMDF，定义的示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1532967be27528fb7dd2454a7a47d16467fbacda
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330900"
---
# <a name="defining-callback-objects-example"></a>定义回调对象示例


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

以下代码示例演示如何将驱动程序继承自[IPnpCallbackHardware](https://msdn.microsoft.com/library/windows/hardware/ff556764)接口可定义设备回调对象。

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

 

 





