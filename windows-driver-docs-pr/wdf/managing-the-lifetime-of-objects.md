---
title: 管理对象的生存期
description: 管理对象的生存期
keywords:
- UMDF 对象 WDK，生存期
- framework 对象 WDK UMDF，生存期
- 生存期 WDK UMDF
- 回叫对象 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1d9b27384180fde879bc85719b499f3b416981c1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783695"
---
# <a name="managing-the-lifetime-of-objects"></a>管理对象的生存期


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

UMDF 使用引用计数方案来管理 [回调对象](creating-callback-objects.md) 和 [框架对象](framework-objects.md)的生存期。

## <a name="managing-references-to-driver-supplied-callback-objects"></a>管理对 Driver-Supplied 回调对象的引用


在大多数情况下，驱动程序不需要保留对回调对象的引用。 如果回调对象接口的方法只由框架以及其生存期依赖于回调对象和回调对象的成对框架对象的对象调用，则驱动程序不必保留引用。 换句话说，驱动程序或框架可以安全地调用对象层次结构中较高的对象接口的方法。

## <a name="managing-references-to-framework-objects"></a>管理对框架对象的引用


在 UMDF 中，常规 COM 生存期原则和特定于 WDF 的生存期模型确定框架对象的生存期。 驱动程序必须满足这两个模型的条件，以便在适当的时间从内存中释放框架对象。

### <a name="com-lifetime-management"></a>COM 生存期管理

在 COM 中，调用方通常会在对象正在使用时保留对该对象的引用，然后在不再需要该对象时调用方释放该引用。 但是，UMDF 驱动程序无需保留对框架对象的引用。 事实上，驱动程序可以在驱动程序创建框架对象之后立即释放框架对象引用。

例如，在调用 [**IWDFDriver：： CreateDevice**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createdevice)后，UMDF 示例释放设备对象。 虽然引用在早期释放，但设备对象会一直存在，直到设备被删除，因为 WDF 对象树保留对它的引用。

因为 UMDF 跟踪对象树中的所有框架对象，所以驱动程序无需保留对框架对象的引用。

但是，如果您的驱动程序保持对框架对象的引用，则当该驱动程序不再需要该对象时，它必须释放该引用。 在驱动程序释放其引用之前，循环引用将保持不变。 为了避免循环引用，驱动程序通常不应保持对框架对象的显式引用。

如果驱动程序必须保留对框架对象的引用，则驱动程序的回调对象还必须实现 [IObjectCleanup](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iobjectcleanup) 接口。 当驱动程序在框架对象上调用 [**IWDFObject：:D eletewdfobject**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfobject-deletewdfobject) 时，框架对象将调用其相应的回调对象的 [**IObjectCleanup：： OnCleanup**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iobjectcleanup-oncleanup) 方法。 实现 **IObjectCleanup：： OnCleanup** 必须释放对框架对象的引用，以使框架能够完成框架对象的细分。

### <a name="wdf-lifetime-management"></a>WDF 生存期管理

如果要创建一个允许重写默认父级的类型的对象，则应选择生存期与对象生存期匹配的父级。 有关默认父对象的详细信息以及驱动程序是否可以重写默认父对象的详细信息，请参阅 [框架对象](framework-objects.md)中的表。

如果与对象生存期匹配，则在删除父对象时，框架会删除你的对象。 如果你不匹配对象生存期，并且想要在删除默认父对象之前删除对象，则可以通过在不再需要该对象时调用 [**DeleteWdfObject**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfobject-deletewdfobject) 来显式删除该对象。

例如，如果创建一个新的请求对象，然后调用 [**IWDFDriver：： CreateWdfMemory**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createwdfmemory) 为此请求创建一个内存对象，则可以将该请求对象指定为新内存对象的父级。 因为当删除父对象时，WDF 会删除子对象，因此驱动程序无需调用 [**DeleteWdfObject**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfobject-deletewdfobject) 来删除内存对象。

但是，如果没有任何父级的生存期与对象的生存期最接近，并且你想要在删除默认父对象之前删除该对象，则必须使用显式删除。 例如，驱动程序可能会创建几个用于短时间的请求对象。 在这种情况下，驱动程序可以通过显式删除不再需要的请求来节省内存。

同样，如果您要创建的对象不允许您覆盖默认父级，并且您希望在删除默认父级之前删除该对象，则驱动程序必须显式删除该对象。

 

