---
title: 打印筛选器中的异步通知
description: 打印筛选器中的异步通知
ms.assetid: 52b0790b-4927-4e1b-8ae5-6e2afc7c9df6
keywords:
- 呈现模块 WDK XPSDrv XPS 筛选器
- XPS 筛选 WDK XPSDrv
- WDK XPS 的筛选器
- 异步通知 WDK XPS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff046003df234ec9a534f91d8ce359007769e3db
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380710"
---
# <a name="asynchronous-notifications-in-print-filters"></a>打印筛选器中的异步通知


打印筛选器管道有一项异步通知功能，非常类似于在应用程序的打印后台处理程序中支持的异步通知。 [ **RouterCreatePrintAsyncNotificationChannel** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prnasntp/nf-prnasntp-routercreateprintasyncnotificationchannel)现已推出打印后台处理程序的函数不是可用于打印筛选器。 打印筛选器必须使用[IPrintClassObjectFactory](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/filterpipeline/nn-filterpipeline-iprintclassobjectfactory)接口，以创建 IPrintAsyncNotify 对象。

本主题介绍如何在打印筛选器中使用异步通知功能。

**请注意**  v4 打印驱动程序模型中不支持引发从打印筛选器的异步通知。

 

### <a name="iprintclassobjectfactory"></a>IPrintClassObjectFactory

[IPrintClassObjectFactory](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/filterpipeline/nn-filterpipeline-iprintclassobjectfactory)接口提供对通知接口访问。 下面的代码示例说明了如何筛选器可以从属性包中获取此接口。

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

使用 IPrintClassObjectFactory 接口，该筛选器可以创建单向或双向通知通道，具体取决于筛选器的需求。 下面的代码示例继续前面的示例中，并显示筛选器如何建立单向通知通道。

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

若要创建双向通知通道，将使用下面的代码示例来代替前面的示例。

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

在前面的代码示例中，变量`pIAsyncCallback`是指向调用方的实现[IPrintAsyncNotifyCallback](https://go.microsoft.com/fwlink/p/?linkid=124755)接口。

在某些情况下，您必须使用它完成后释放双向通知通道。 若要执行此操作，调用[发行](https://go.microsoft.com/fwlink/p/?linkid=98433)方法[IPrintAsyncNotifyChannel](https://go.microsoft.com/fwlink/p/?linkid=124758)。 有关何时释放通道的信息，请参阅[通知通道](notification-channel.md)。

### <a name="impersonation-and-notification"></a>模拟和通知

当调用 IPrintAsyncNotify::CreatePrintAsyncNotifyChannel 方法时，筛选器必须模拟的用户帐户。 打印后台处理程序中的授权机制需要调用本地服务帐户中。 如果筛选器必须模拟的提交该作业的用户帐户，该筛选器必须还原到其自身调用 CreatePrintAsyncNotifyChannel 之前。 在调用返回后，筛选器可以还原到的用户帐户，如有必要。

**请注意**  即使通知调用本地服务上下文中，仍然会 kPerUser 通知发送到提交该作业基于作业 ID 的用户关联的用户

 

### <a name="adapting-the-wdk-sample-code"></a>调整 WDK 示例代码

您可以改写 WDK 示例代码，以便通过 RouterCreatePrintAsyncNotificationChannel 调用替换为下面的代码示例在打印筛选器中从通知示例。

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

 

 




