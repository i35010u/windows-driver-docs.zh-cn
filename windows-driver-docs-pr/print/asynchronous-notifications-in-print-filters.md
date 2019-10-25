---
title: 打印筛选器中的异步通知
description: 打印筛选器中的异步通知
ms.assetid: 52b0790b-4927-4e1b-8ae5-6e2afc7c9df6
keywords:
- 渲染模块 WDK XPSDrv，XPS 筛选器
- XPS 筛选器 WDK XPSDrv
- 筛选 WDK XPS
- 异步通知 WDK XP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: adf5f3fcade0fb61d2386c8bacf76d2d6a3a9641
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842309"
---
# <a name="asynchronous-notifications-in-print-filters"></a>打印筛选器中的异步通知


打印筛选器管道的异步通知功能非常类似于应用程序打印后台处理程序中支持的异步通知。 打印后台处理程序中提供的[**RouterCreatePrintAsyncNotificationChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prnasntp/nf-prnasntp-routercreateprintasyncnotificationchannel)函数对于打印筛选器不可用。 打印筛选器必须使用[IPrintClassObjectFactory](https://docs.microsoft.com/windows-hardware/drivers/ddi/filterpipeline/nn-filterpipeline-iprintclassobjectfactory)接口来创建 IPrintAsyncNotify 对象。

本主题介绍如何在打印筛选器中使用异步通知功能。

**请注意**  在 v4 打印驱动程序模型中不支持从打印筛选器中引发异步通知。

 

### <a name="iprintclassobjectfactory"></a>IPrintClassObjectFactory

[IPrintClassObjectFactory](https://docs.microsoft.com/windows-hardware/drivers/ddi/filterpipeline/nn-filterpipeline-iprintclassobjectfactory)接口提供对通知接口的访问。 下面的代码示例演示了筛选器如何从属性包获取此接口。

```cpp
// This interface is defined as a private member variable in the filter class
IPrintClassObjectFactory  *m_pPrintClassFactory;

// The following code goes in the IntializeFilter method of the filter
VARIANT var;
VariantInit(&var);

HRESULT hr = pIPropertyBag->GetProperty(
    XPS_FP_PRINT_CLASS_FACTORY, 
    &var);

if (SUCCEEDED(hr))
{
    hr = V_UNKNOWN(&var)->QueryInterface(
 IID_IPrintClassObjectFactory,
 reinterpret_cast<void **>(&m_pPrintClassFactory));
}
```

### <a name="notification-channel"></a>通知通道

使用 IPrintClassObjectFactory 接口，筛选器可以创建单向或双向通知通道，具体取决于筛选器的需求。 下面的代码示例从前面的示例继续，并演示了筛选器如何建立单向通知通道。

```cpp
// Create a unidirectional notification channel
IPrintAsyncNotifyChannel  *pIAsyncNotifyChannel;
IPrintAsyncNotify  *pIAsyncNotify;

HRESULT hr = m_pPrintClassFactory->GetPrintClassObject(
 m_bstrPrinter,      // The printer name that was read from the property bag
 IID_IPrintAsyncNotify,
 reinterpret_cast<void**>(&pIAsyncNotify)));

if (SUCCEEDED(hr))
{
    hr = pIAsyncNotify->CreatePrintAsyncNotifyChannel(
 m_jobId,
 const_cast<GUID*>(&MS_ASYNCNOTIFY_UI),
 kPerUser,
 kUniDirectional,
        NULL,
        &pIAsyncNotifyChannel));

   // Etc.
}
```

若要创建双向通知通道，请使用以下代码示例来替代前面的示例。

```cpp
// Create a bidirectional notification channel
IPrintAsyncNotifyChannel *pIAsyncNotifyChannel;
IPrintAsyncNotify *pIAsyncNotify;

HRESULT hr = m_pPrintClassFactory->GetPrintClassObject(
 m_bstrPrinterName,   // The printer name that was read from the property bag
 IID_IPrintAsyncNotify,
 reinterpret_cast<void**>(&pIAsyncNotify)));

if (SUCCEEDED(hr))
{
    hr = pIAsyncNotify->CreatePrintAsyncNotifyChannel(
 m_jobId,
 const_cast<GUID*>(& SAMPLE_ASYNCNOTIFY_UI),
 kPerUser,
 kBiDirectional,
 pIAsyncCallback,
        &pIAsyncNotifyChannel));

    // Etc.
}
```

在上面的代码示例中，变量 `pIAsyncCallback` 是指向调用方的[IPrintAsyncNotifyCallback](https://go.microsoft.com/fwlink/p/?linkid=124755)接口实现的指针。

在某些情况下，在完成双向通知通道后，必须释放双向通知通道。 为此，请在[IPrintAsyncNotifyChannel](https://go.microsoft.com/fwlink/p/?linkid=124758)上调用[Release](https://go.microsoft.com/fwlink/p/?linkid=98433)方法。 有关何时发布通道的信息，请参阅[通知通道](notification-channel.md)。

### <a name="impersonation-and-notification"></a>模拟和通知

筛选器在调用 IPrintAsyncNotify：： CreatePrintAsyncNotifyChannel 方法时，不能模拟用户帐户。 打印后台处理程序中的授权机制要求从本地服务帐户调用它。 如果筛选器必须模拟提交该作业的用户的帐户，则该筛选器必须恢复到其自身，然后才能调用 CreatePrintAsyncNotifyChannel。 调用返回后，筛选器可以恢复为用户帐户（如有必要）。

**请注意**  即使在本地服务上下文中发出通知调用，也会根据作业 ID 的用户关联，将 kPerUser 通知发送给提交作业的用户。

 

### <a name="adapting-the-wdk-sample-code"></a>调整 WDK 示例代码

可以通过将 RouterCreatePrintAsyncNotificationChannel 调用替换为以下代码示例，从 WDK 示例代码调整通知示例以在打印筛选器中工作。

```cpp
IPrintAsyncNotify  *pIAsyncNotify;

HRESULT hr = m_pPrintClassFactory->GetPrintClassObject(
 m_bstrPrinterName,      // get it from the property bag
 IID_IPrintAsyncNotify,
 reinterpret_cast<void**>(&pIAsyncNotify)));

if (SUCCEEDED(hr))
{
    hr = pIAsyncNotify->CreatePrintAsyncNotifyChannel(
 // the same arguments as for 
 // RouterCreatePrintAsyncNotificationChannel
        );

    // Etc.
}
```

 

 




