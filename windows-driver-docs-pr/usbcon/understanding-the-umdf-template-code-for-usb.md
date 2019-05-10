---
Description: 了解如何基于 UMDF 的 USB 客户端驱动程序的源代码。
title: USB 客户端驱动程序代码结构 (UMDF)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a40fc017f0d1c04e52e15a148375955bf9a6d03d
ms.sourcegitcommit: 0504cc497918ebb7b41a205f352046a66c0e26a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2019
ms.locfileid: "65405076"
---
# <a name="understanding-the-usb-client-driver-code-structure-umdf"></a>了解 USB 客户端驱动程序代码结构 (UMDF)


本主题中您将了解 UMDF 基于 USB 客户端驱动程序的源代码。 由生成的代码示例**USB 用户模式驱动程序**Microsoft Visual Studio 2012 中包含的模板。 模板代码使用活动模板库 (ATL) 生成的 COM 基础结构。 ATL 和有关客户端驱动程序中的 COM 实现的详细信息不在此处讨论。

有关生成 UMDF 模板代码的说明，请参阅[如何编写第一个 USB 客户端驱动程序 (UMDF)](implement-driver-entry-for-a-usb-driver--umdf-.md)。 这些部分介绍上述模板代码：

-   [驱动程序回调源代码](#driver-callback-source-code)
-   [设备回调源代码](#device-callback-source-code)
-   [队列的源代码](#queue-source-code)
-   [驱动程序条目的源代码](#driver-entry-source-code)

在讨论之前的模板代码的详细信息，让我们看看标头文件 (Internal.h) UMDF 驱动程序开发相关的一些声明。

Internal.h 包含这些文件，包括 Windows Driver Kit (WDK) 中：

```ManagedCPlusPlus
#include "atlbase.h"
#include "atlcom.h"

#include "wudfddi.h"
#include "wudfusb.h"
```

Atlbase.h 和 atlcom.h 包含 ATL 支持的声明。 由客户端驱动程序实现的每个类实现 ATL 类公共 CComObjectRootEx。

Wudfddi.h 将始终包括 UMDF 驱动程序开发。 标头文件包括各种声明和定义的方法和需要编译 UMDF 驱动程序的结构。

Wudfusb.h 包括声明和定义 UMDF 结构和与框架提供的 USB I/O 目标对象进行通信所需的方法。

Internal.h 中的下一步块声明设备接口的 GUID 常量。 应用程序可以使用此 GUID 使用打开的句柄设备**SetupDiXxx** Api。 GUID 被注册后，框架创建设备对象。

```ManagedCPlusPlus
// Device Interface GUID
// f74570e5-ed0c-4230-a7a5-a56264465548

DEFINE_GUID(GUID_DEVINTERFACE_MyUSBDriver_UMDF_,
    0xf74570e5,0xed0c,0x4230,0xa7,0xa5,0xa5,0x62,0x64,0x46,0x55,0x48);
```

下一步部分声明跟踪宏和跟踪 GUID。 请注意跟踪 GUID;若要启用跟踪，将需要它。

```ManagedCPlusPlus
#define WPP_CONTROL_GUIDS                                              \
    WPP_DEFINE_CONTROL_GUID(                                           \
        MyDriver1TraceGuid, (f0261b19,c295,4a92,aa8e,c6316c82cdf0),    \
                                                                       \
        WPP_DEFINE_BIT(MYDRIVER_ALL_INFO)                              \
        WPP_DEFINE_BIT(TRACE_DRIVER)                                   \
        WPP_DEFINE_BIT(TRACE_DEVICE)                                   \
        WPP_DEFINE_BIT(TRACE_QUEUE)                                    \
        )                             

#define WPP_FLAG_LEVEL_LOGGER(flag, level)                             \
    WPP_LEVEL_LOGGER(flag)

#define WPP_FLAG_LEVEL_ENABLED(flag, level)                            \
    (WPP_LEVEL_ENABLED(flag) &&                                        \
     WPP_CONTROL(WPP_BIT_ ## flag).Level >= level)

#define WPP_LEVEL_FLAGS_LOGGER(lvl,flags) \
           WPP_LEVEL_LOGGER(flags)

#define WPP_LEVEL_FLAGS_ENABLED(lvl, flags) \
           (WPP_LEVEL_ENABLED(flags) && WPP_CONTROL(WPP_BIT_ ## flags).Level >= lvl)
```

Internal.h 中的下一行向前声明队列回调对象的客户端驱动程序实现类。 它还包括由模板生成其他项目文件。 本主题下文中讨论了实现和项目标头文件。

```ManagedCPlusPlus
// Forward definition of queue.

typedef class CMyIoQueue *PCMyIoQueue;

// Include the type specific headers.

#include "Driver.h"
#include "Device.h"
#include "IoQueue.h"
```

安装客户端驱动程序后，Windows 将加载客户端驱动程序和主机进程的实例中的框架。 从此处，框架将加载并初始化客户端驱动程序。 框架执行以下任务：

1.  创建*驱动程序对象*在 framework 中，它表示客户端驱动程序。
2.  请求[IDriverEntry](https://msdn.microsoft.com/library/windows/hardware/ff554885)从类工厂的接口指针。
3.  创建*设备对象*framework 中。
4.  PnP 管理器启动设备后，请初始化设备对象。

该驱动程序已加载并初始化，而多个事件发生，并且框架允许参与处理它们的客户端驱动程序。 在客户端驱动程序的端，该驱动程序执行以下任务：

1.  实现并导出[ **DllGetClassObject** ](https://msdn.microsoft.com/library/windows/desktop/ms680760)函数从你的客户端驱动程序模块，以便该框架可以获取对该驱动程序的引用。
2.  提供一个回调类，实现[IDriverEntry](https://msdn.microsoft.com/library/windows/hardware/ff554885)接口。
3.  提供一个回调类，实现**IPnpCallbackXxx**接口。
4.  获取对设备对象的引用，并将其配置为根据客户端驱动程序的要求。

## <a name="driver-callback-source-code"></a>驱动程序回调源代码


框架将创建*驱动程序对象*，表示加载的 Windows 客户端驱动程序的实例。 客户端驱动程序提供了至少一个向框架注册驱动程序的驱动程序回调。

在 Driver.h 和 Driver.c 是驱动程序回调的完整源代码。

客户端驱动程序必须定义驱动程序回调类，实现该类[ **IUnknown** ](https://msdn.microsoft.com/library/windows/desktop/ms680509)并[ **IDriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff554885)接口。 标头文件，Driver.h，声明一个名为 CMyDriver，定义驱动程序回调类。

```ManagedCPlusPlus
EXTERN_C const CLSID CLSID_Driver;

class CMyDriver :
    public CComObjectRootEx<CComMultiThreadModel>,
    public CComCoClass<CMyDriver, &CLSID_Driver>,
    public IDriverEntry
{
public:

    CMyDriver()
    {
    }

    DECLARE_NO_REGISTRY()

    DECLARE_NOT_AGGREGATABLE(CMyDriver)

    BEGIN_COM_MAP(CMyDriver)
        COM_INTERFACE_ENTRY(IDriverEntry)
    END_COM_MAP()

public:

    // IDriverEntry methods

    virtual
    HRESULT
    STDMETHODCALLTYPE
    OnInitialize(
        __in IWDFDriver *FxWdfDriver
        )
    {
        UNREFERENCED_PARAMETER(FxWdfDriver);
        return S_OK;
    }

    virtual
    HRESULT
    STDMETHODCALLTYPE
    OnDeviceAdd(
        __in IWDFDriver *FxWdfDriver,
        __in IWDFDeviceInitialize *FxDeviceInit
        );

    virtual
    VOID
    STDMETHODCALLTYPE
    OnDeinitialize(
        __in IWDFDriver *FxWdfDriver
        )
    {
        UNREFERENCED_PARAMETER(FxWdfDriver);
        return;
    }

};

OBJECT_ENTRY_AUTO(CLSID_Driver, CMyDriver)
```

驱动程序回调必须是 COM 类，这意味着它必须实现[ **IUnknown** ](https://msdn.microsoft.com/library/windows/desktop/ms680509)和相关的方法。 在模板代码中，ATL 类 CComObjectRootEx 和包含 CComCoClass **IUnknown**方法。

Windows 实例化宿主进程后，框架将创建的驱动程序对象。 若要执行此操作，框架将创建的驱动程序回调类并调用驱动程序实现的实例[ **DllGetClassObject** ](https://msdn.microsoft.com/library/windows/desktop/ms680760) (中所述[驱动程序条目源代码](#driver-entry-source-code)部分)，并获取客户端驱动程序[ **IDriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff554885)接口指针。 该调用 framework 驱动程序对象向注册的驱动程序回调对象。 注册成功后，框架在发生特定驱动程序特定事件时调用客户端驱动程序的实现。 第一种方法，该框架将调用[ **IDriverEntry::OnInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff554885_oninitialize)方法。 在客户端驱动程序的实现中的**IDriverEntry::OnInitialize**，客户端驱动程序可以分配全局驱动程序资源。 必须在释放这些资源[ **IDriverEntry::OnDeinitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff554885_ondeinitialize)它正在准备卸载客户端驱动程序之前由框架调用。 模板代码提供的最小实现**OnInitialize**并**OnDeinitialize**方法。

最重要的方法[ **IDriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff554885)是[ **IDriverEntry::OnDeviceAdd**](https://msdn.microsoft.com/library/windows/hardware/ff554885_ondeviceadd)。 框架创建框架设备对象 （在下一节中讨论） 之前，它会调用驱动程序的**IDriverEntry::OnDeviceAdd**实现。 调用方法时，框架将传递[ **IWDFDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff558893)指向驱动程序对象和一个[ **IWDFDeviceInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff556965)指针。 客户端驱动程序可以调用**IWDFDeviceInitialize**方法指定某些配置选项。

通常情况下，客户端驱动程序将执行以下任务在其[ **IDriverEntry::OnDeviceAdd** ](https://msdn.microsoft.com/library/windows/hardware/ff554896)实现：

-   指定要创建的设备对象的配置信息。
-   实例化驱动程序的设备回调类。
-   创建框架设备对象并向框架注册其设备回调对象。
-   初始化框架设备对象。
-   注册设备接口的客户端驱动程序的 GUID。

在模板代码中， **IDriverEntry::OnDeviceAdd**的静态方法调用，CMyDevice::CreateInstanceAndInitialize，设备回调类中定义。 静态方法首先实例化客户端驱动程序的设备回调类，然后创建 framework 设备对象。 设备回调类还定义一个名为上述列表中执行剩余任务所述的配置的公共方法。 下一节中讨论的设备回调类的实现。
下面的代码示例演示[ **IDriverEntry::OnDeviceAdd** ](https://msdn.microsoft.com/library/windows/hardware/ff554896)模板代码中的实现。

```ManagedCPlusPlus
HRESULT
CMyDriver::OnDeviceAdd(
    __in IWDFDriver *FxWdfDriver,
    __in IWDFDeviceInitialize *FxDeviceInit
    )
{
    HRESULT hr = S_OK;
    CMyDevice *device = NULL;

    hr = CMyDevice::CreateInstanceAndInitialize(FxWdfDriver,
                                                FxDeviceInit,
                                                &device);

    if (SUCCEEDED(hr))
    {
        hr = device->Configure();
    }

    return hr;
}
```

下面的代码示例演示了在 Device.h 设备类声明。

```ManagedCPlusPlus
class CMyDevice :
    public CComObjectRootEx<CComMultiThreadModel>,
    public IPnpCallbackHardware
{

public:

    DECLARE_NOT_AGGREGATABLE(CMyDevice)

    BEGIN_COM_MAP(CMyDevice)
        COM_INTERFACE_ENTRY(IPnpCallbackHardware)
    END_COM_MAP()

    CMyDevice() :
        m_FxDevice(NULL),
        m_IoQueue(NULL),
        m_FxUsbDevice(NULL)
    {
    }

    ~CMyDevice()
    {
    }

private:

    IWDFDevice *            m_FxDevice;

    CMyIoQueue *            m_IoQueue;

    IWDFUsbTargetDevice *   m_FxUsbDevice;

private:

    HRESULT
    Initialize(
        __in IWDFDriver *FxDriver,
        __in IWDFDeviceInitialize *FxDeviceInit
        );

public:

    static
    HRESULT
    CreateInstanceAndInitialize(
        __in IWDFDriver *FxDriver,
        __in IWDFDeviceInitialize *FxDeviceInit,
        __out CMyDevice **Device
        );

    HRESULT
    Configure(
        VOID
        );
public:

    // IPnpCallbackHardware methods

    virtual
    HRESULT
    STDMETHODCALLTYPE
    OnPrepareHardware(
            __in IWDFDevice *FxDevice
            );

    virtual
    HRESULT
    STDMETHODCALLTYPE
    OnReleaseHardware(
        __in IWDFDevice *FxDevice
        );

};
```

## <a name="device-callback-source-code"></a>设备回调源代码


*Framework 设备对象*是表示在客户端驱动程序的设备堆栈中加载的设备对象的框架类的实例。 有关设备对象的功能的信息，请参阅[设备节点和设备堆栈](https://msdn.microsoft.com/library/windows/hardware/hh406296)。

设备对象的完整源代码位于 Device.h 和 Device.c。

Framework 设备类实现[ **IWDFDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff556917)接口。 客户端驱动程序负责在驱动程序的实现中创建该类的实例[ **IDriverEntry::OnDeviceAdd**](https://msdn.microsoft.com/library/windows/hardware/ff554896)。 创建对象后，客户端驱动程序将获取**IWDFDevice**指针，指向要管理的设备对象的操作该接口上的新对象并调用方法。

**IDriverEntry::OnDeviceAdd 实现**

在上一节中，您简要看到客户端驱动程序中执行的任务[ **IDriverEntry::OnDeviceAdd**](https://msdn.microsoft.com/library/windows/hardware/ff554896)。 下面是有关这些任务的详细信息。 客户端驱动程序：

-   指定要创建的设备对象的配置信息。

    在 framework 中调用的客户端驱动程序的实现[ **IDriverEntry::OnDeviceAdd** ](https://msdn.microsoft.com/library/windows/hardware/ff554896)方法，该框架将传递[ **IWDFDeviceInitialize**](https://msdn.microsoft.com/library/windows/hardware/ff556965)指针。 客户端驱动程序使用此指针来指定要创建的设备对象的配置信息。 例如，客户端驱动程序指定一个筛选器或功能驱动程序是否有客户端驱动程序。 若要标识客户端驱动程序，因为筛选器驱动程序，它将调用[ **IWDFDeviceInitialize::SetFilter**](https://msdn.microsoft.com/library/windows/hardware/ff556965_setfilter)。 在这种情况下，框架将创建一个筛选器设备对象 (FiDO);否则，创建一个函数设备对象 (FDO)。 可以设置的另一个选项是同步模式下通过调用[ **IWDFDeviceInitialize::SetLockingConstraint**](https://msdn.microsoft.com/library/windows/hardware/ff556965_setlockingconstraint)。

-   调用[ **IWDFDriver::CreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff558899)方法并传递[ **IWDFDeviceInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff556965)接口指针， [ **IUnknown** ](https://msdn.microsoft.com/library/windows/desktop/ms680509)设备回调对象和指针到指针的引用[ **IWDFDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff556917)变量。

    如果[ **IWDFDriver::CreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff558899)调用是成功：

    -   框架将创建的设备对象。
    -   该框架向框架注册设备回调。

        Framework 设备对象与配对设备回调后，框架和客户端驱动程序处理特定事件，如即插即用的状态和电源状态更改。 例如，当 PnP 管理器将启动设备，将通知框架。 框架调用设备回调[ **IPnpCallbackHardware::OnPrepareHardware** ](https://msdn.microsoft.com/library/windows/hardware/ff556766)实现。 每个客户端驱动程序必须注册至少一个设备回调对象。

    -   客户端驱动程序将收到新的设备对象中的地址[ **IWDFDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff556917)变量。 收到指向 framework 设备对象的指针时，客户端驱动程序可以继续进行初始化任务，例如为 I/O 流设置队列并注册设备接口的 GUID。

-   调用[ **IWDFDevice::CreateDeviceInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff550965)注册设备接口的客户端驱动程序的 GUID。 应用程序可以使用 GUID 来将请求发送到客户端驱动程序。 在 Internal.h 中声明的 GUID 常量。
-   初始化的 I/O 传输到和从设备队列。

模板代码定义的帮助器方法初始化指定的配置信息并创建设备对象。

下面的代码示例显示了实现进行初始化。

```ManagedCPlusPlus
HRESULT
CMyDevice::Initialize(
    __in IWDFDriver           * FxDriver,
    __in IWDFDeviceInitialize * FxDeviceInit
    )
{
    IWDFDevice *fxDevice = NULL;
    HRESULT hr = S_OK;
    IUnknown *unknown = NULL;

    TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_DEVICE, "%!FUNC! Entry");

    FxDeviceInit->SetLockingConstraint(None);

    FxDeviceInit->SetPowerPolicyOwnership(TRUE);

    hr = this->QueryInterface(__uuidof(IUnknown), (void **)&unknown);
    if (FAILED(hr))
    {
        TraceEvents(TRACE_LEVEL_ERROR,
                    TRACE_DEVICE,
                    "%!FUNC! Failed to get IUnknown %!hresult!",
                    hr);
        goto Exit;
    }

    hr = FxDriver->CreateDevice(FxDeviceInit, unknown, &fxDevice);
    DriverSafeRelease(unknown);
    if (FAILED(hr))
    {
        TraceEvents(TRACE_LEVEL_ERROR,
                    TRACE_DEVICE,
                    "%!FUNC! Failed to create a framework device %!hresult!",
                    hr);
        goto Exit;
    }

     m_FxDevice = fxDevice;

     DriverSafeRelease(fxDevice);

Exit:

    TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_DEVICE, "%!FUNC! Exit");

    return hr;
}
```

在前面的代码示例中，客户端驱动程序创建设备对象，并注册其设备回调。 之前创建的设备对象，该驱动程序指定其配置首选项由上调用方法[ **IWDFDeviceInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff556965)接口指针。 它是相同的指针传递在上一个调用客户端驱动程序的框架[ **IDriverEntry::OnDeviceAdd** ](https://msdn.microsoft.com/library/windows/hardware/ff554896)方法。

客户端驱动程序指定它将设备对象的电源策略所有者。 作为 power 策略所有者，客户端驱动程序确定系统电源状态更改时，应输入设备的相应的电源状态。 驱动程序还负责将相关的请求发送到设备，以使电源状态转换。 默认情况下，基于 UMDF 的客户端驱动程序不是电源策略所有者;该框架将处理所有的电源状态转换。 该框架会自动发送到设备**D3**在系统进入睡眠状态，并与之相反将使设备回**D0**当系统进入工作状态的**S0**. 有关详细信息，请参阅[UMDF 中的电源策略所有权](https://msdn.microsoft.com/library/windows/hardware/ff560462)。

另一个配置选项是指定筛选器驱动程序或设备的功能驱动程序是否有客户端驱动程序。 请注意，在代码示例中，客户端驱动程序未显式指定其首选项。 这意味着客户端驱动程序是函数驱动程序，则框架应在设备堆栈中创建 FDO。 如果客户端驱动程序的目标是筛选器驱动程序，则该驱动程序必须调用[ **IWDFDeviceInitialize::SetFilter** ](https://msdn.microsoft.com/library/windows/hardware/ff556985)方法。 在这种情况下，框架将创建 FiDO 设备堆栈中。

客户端驱动程序还指定同步的任何框架的客户端驱动程序的回调调用。 客户端驱动程序负责处理所有同步任务。 若要指定该首选项，客户端驱动程序调用[ **IWDFDeviceInitialize::SetLockingConstraint** ](https://msdn.microsoft.com/library/windows/hardware/ff556991)方法。

接下来，客户端驱动程序将获取[ **IUnknown** ](https://msdn.microsoft.com/library/windows/desktop/ms680509)指向通过调用其设备回调类[ **iunknown:: Queryinterface**](https://msdn.microsoft.com/library/windows/desktop/ms682521)。 随后，客户端驱动程序调用[ **IWDFDriver::CreateDevice**](https://msdn.microsoft.com/library/windows/hardware/ff558899)，后者创建 framework 设备对象并使用注册客户端驱动程序的设备回调**IUnknown**指针。

请注意，客户端驱动程序存储的设备对象的地址 (通过接收[ **IWDFDriver::CreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff558899)调用) 中的设备回调类的私有数据成员，然后释放的通过调用 DriverSafeRelease （内联函数定义中 Internal.h） 引用。 这是因为设备对象的生存期跟踪框架。 因此客户端驱动程序不需要保留的设备对象的其他引用计数。

模板代码定义配置，这将注册的设备接口的 GUID，并设置队列的公共方法。 下面的代码示例显示了设备回调类，CMyDevice 中的配置方法的定义。 配置由调用[ **IDriverEntry::OnDeviceAdd** ](https://msdn.microsoft.com/library/windows/hardware/ff554896)创建 framework 设备对象之后。

```ManagedCPlusPlus
CMyDevice::Configure(
    VOID
    )
{

    HRESULT hr = S_OK;

    TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_DEVICE, "%!FUNC! Entry");

     hr = CMyIoQueue::CreateInstanceAndInitialize(m_FxDevice, this, &m_IoQueue);
    if (FAILED(hr))
    {
        TraceEvents(TRACE_LEVEL_ERROR,
                    TRACE_DEVICE,
                    "%!FUNC! Failed to create and initialize queue %!hresult!",
                    hr);
        goto Exit;
    }

    hr = m_IoQueue->Configure();
    if (FAILED(hr))
    {
        TraceEvents(TRACE_LEVEL_ERROR,
                    TRACE_DEVICE,
                    "%!FUNC! Failed to configure queue %!hresult!",
                    hr);
        goto Exit;
    } 

    hr = m_FxDevice->CreateDeviceInterface(&GUID_DEVINTERFACE_MyUSBDriver_UMDF_,NULL);
    if (FAILED(hr))
    {
        TraceEvents(TRACE_LEVEL_ERROR,
                    TRACE_DEVICE,
                    "%!FUNC! Failed to create device interface %!hresult!",
                    hr);
        goto Exit;
    }

Exit:

    TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_DEVICE, "%!FUNC! Exit");

    return hr;
}
```

在前面的代码示例中，客户端驱动程序执行两项主要任务： 初始化的 I/O 流的队列并注册设备接口的 GUID。

中的队列、 创建和配置 CMyIoQueue 类中。 第一个任务是通过调用静态方法名为 CreateInstanceAndInitialize 实例化该类。 客户端驱动程序调用配置来初始化队列。 CreateInstanceAndInitialize 和配置 CMyIoQueue，本主题后面所述中声明。

客户端驱动程序还会调用[ **IWDFDevice::CreateDeviceInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff550965)注册设备接口的客户端驱动程序的 GUID。 应用程序可以使用 GUID 来将请求发送到客户端驱动程序。 在 Internal.h 中声明的 GUID 常量。

**IPnpCallbackHardware 实现和特定于 USB 的任务**

接下来，让我们看看的实现[ **IPnpCallbackHardware** ](https://msdn.microsoft.com/library/windows/hardware/ff556764) Device.cpp 中的接口。

每个设备回调类必须实现[ **IPnpCallbackHardware** ](https://msdn.microsoft.com/library/windows/hardware/ff556764)接口。 此接口有两个方法：[**IPnpCallbackHardware::OnPrepareHardware** ](https://msdn.microsoft.com/library/windows/hardware/ff556764_onpreparehardware)并[ **IPnpCallbackHardware::OnReleaseHardware**](https://msdn.microsoft.com/library/windows/hardware/ff556764_onreleasehardware)。 框架将调用这些方法对两个事件的响应： 当 PnP 管理器启动设备并将删除设备。 设备已启动、 建立与硬件通信，但设备未进入工作状态时 (**D0**)。 因此，在**IPnpCallbackHardware::OnPrepareHardware**客户端驱动程序可以从硬件中获取设备信息、 分配资源，并初始化所需的驱动程序的生存期内的 framework 对象。 PnP 管理器中删除设备，该驱动程序时，从系统中卸载。 框架将调用客户端驱动程序**IPnpCallbackHardware::OnReleaseHardware**驱动程序可以释放这些资源和 framework 对象的实现。

PnP 管理器可以生成其他类型的事件而导致的即插即用的状态更改。 该框架提供默认处理这些事件。 客户端驱动程序可以选择参与这些事件的处理。 请考虑 USB 设备与主机的方案。 PnP 管理器就能识别该事件，并会通知框架。 如果客户端驱动程序想要在响应该事件中执行其他任务，该驱动程序必须实现[ **IPnpCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff556762)接口以及相关[ **IPnpCallback:: OnSurpriseRemoval** ](https://msdn.microsoft.com/library/windows/hardware/ff556762_onsurpriseremoval)设备回调类中的方法。 否则，该框架将继续进行默认处理的事件。

USB 客户端驱动程序必须检索有关受支持的接口、 替代设置和终结点的信息并发送任何数据传输的 I/O 请求之前对其进行配置。 UMDF 提供简化许多客户端驱动程序的配置任务的专用的 I/O 目标对象。 若要配置 USB 设备，客户端驱动程序需要即插即用管理器启动设备后，只是可用的设备信息。

此模板代码将创建这些对象中的[ **IPnpCallbackHardware::OnPrepareHardware** ](https://msdn.microsoft.com/library/windows/hardware/ff556766)方法。

通常情况下，客户端驱动程序执行一个或多个 （具体取决于设备的设计） 这些配置任务：

1.  检索当前的配置，如接口的数量有关的信息。 框架将选择 USB 设备上的第一个配置。 客户端驱动程序不能选择对于多配置设备的另一个配置。
2.  检索接口，例如终结点的数量有关的信息。
3.  更改替代设置的内每个接口，如果该接口支持对多个设置。 默认情况下，框架将 USB 设备上的第一个配置中选择每个接口的第一个备用设置。 客户端驱动程序可以选择以选择备用设置。
4.  检索有关每个接口中的终结点的信息。

若要执行这些任务，客户端驱动程序可以使用这些类型的 WDF 所提供的专用 USB I/O 目标对象。

| USB I/O 目标对象     | 描述                                                                                                                                                                                                                                                                                                                               | UMDF 接口                                  |
|---------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------|
| *目标设备对象*    | 表示 USB 设备，并提供用于检索设备描述符并将控制请求发送到设备的方法。                                                                                                                                                                                                             | [IWDFUsbTargetDevice](https://msdn.microsoft.com/library/windows/hardware/ff560362) |
| *目标接口对象* | 表示单个接口，并提供客户端驱动程序可以调用来选择备用设置和检索有关设置的信息的方法。                                                                                                                                                                          | [IWDFUsbInterface](https://msdn.microsoft.com/library/windows/hardware/ff560312)       |
| *目标管道对象*      | 表示单个管道接口的当前备用设置中配置的终结点。 USB 总线驱动程序选择所选的配置中的每个接口，并设置在界面中每个终结点的通信通道。 在 USB 术语中，调用该信道*管道*。 | [IWDFUsbTargetPipe](https://msdn.microsoft.com/library/windows/hardware/ff560391)     |



下面的代码示例显示了为实现[ **IPnpCallbackHardware::OnPrepareHardware**](https://msdn.microsoft.com/library/windows/hardware/ff556766)。

```ManagedCPlusPlus
HRESULT
CMyDevice::OnPrepareHardware(
    __in IWDFDevice * /* FxDevice */
    )
{
    HRESULT hr;
    IWDFUsbTargetFactory *usbFactory = NULL;
    IWDFUsbTargetDevice *usbDevice = NULL;

    TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_DEVICE, "%!FUNC! Entry");

    hr = m_FxDevice->QueryInterface(IID_PPV_ARGS(&usbFactory));

    if (FAILED(hr))
    {
        TraceEvents(TRACE_LEVEL_ERROR,
                    TRACE_DEVICE,
                    "%!FUNC! Failed to get USB target factory %!hresult!",
                    hr);
        goto Exit;
    }

    hr = usbFactory->CreateUsbTargetDevice(&usbDevice);

    if (FAILED(hr))
    {
        TraceEvents(TRACE_LEVEL_ERROR,
                    TRACE_DEVICE,
                    "%!FUNC! Failed to create USB target device %!hresult!",
                    hr);

        goto Exit;
    }

     m_FxUsbDevice = usbDevice;

Exit:

    DriverSafeRelease(usbDevice);

    DriverSafeRelease(usbFactory);

    TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_DEVICE, "%!FUNC! Exit");

    return hr;
}
```

若要使用框架的 USB I/O 目标对象，客户端驱动程序必须首先创建的 USB 目标设备对象。 在 framework 对象模型中，USB 目标设备对象是表示 USB 设备的设备对象的子级。 USB 目标设备对象由该框架实现和执行所有的 USB 设备，如选择一种配置的设备级任务。

在前面的代码示例中，客户端驱动程序查询 framework 设备对象，并获取[ **IWDFUsbTargetFactory** ](https://msdn.microsoft.com/library/windows/hardware/ff560387)指向创建的 USB 目标设备对象的类工厂。 通过使用该指针，该客户端驱动程序调用[ **IWDFUsbTargetDevice::CreateUsbTargetDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff560387_createusbtargetdevice)方法。 此方法创建的 USB 目标设备对象并返回一个指向[ **IWDFUsbTargetDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff560362)接口。 该方法还将选择默认 （第一个） 配置，并在该配置中设置的每个接口的 0 备用。

模板代码将存储的 USB 目标设备对象的地址 (通过接收[ **IWDFDriver::CreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff558899)调用) 中的设备回调类的私有数据成员，然后释放的通过调用 DriverSafeRelease 引用。 由框架进行维护的 USB 目标设备对象的引用计数。 只要设备对象处于活动状态，该对象处于活动状态。 客户端驱动程序必须发布中的引用[ **IPnpCallbackHardware::OnReleaseHardware**](https://msdn.microsoft.com/library/windows/hardware/ff556768)。

客户端驱动程序创建的 USB 目标设备对象之后，该驱动程序调用[ **IWDFUsbTargetDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff560362)方法来执行这些任务：

-   检索设备、 配置、 接口描述符和其他信息，例如设备的速度。
-   格式化并将输入/输出控制请求发送到默认终结点。
-   设置整个 USB 设备的电源策略。

有关详细信息，请参阅[使用 USB 设备中 UMDF](https://msdn.microsoft.com/library/windows/hardware/ff561472)。
下面的代码示例显示了为实现[ **IPnpCallbackHardware::OnReleaseHardware**](https://msdn.microsoft.com/library/windows/hardware/ff556768)。

```ManagedCPlusPlus
HRESULT
CMyDevice::OnReleaseHardware(
    __in IWDFDevice * /* FxDevice */
    )
{
    TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_DEVICE, "%!FUNC! Entry");

    if (m_FxUsbDevice != NULL) {

        m_FxUsbDevice->DeleteWdfObject();
        m_FxUsbDevice = NULL;
    }

    TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_DEVICE, "%!FUNC! Exit");

    return S_OK;
}
```

## <a name="queue-source-code"></a>队列的源代码


*Framework 队列对象*表示特定的框架设备对象的 I/O 队列。 队列对象的完整源代码是 IoQueue.h 和 IoQueue.c 中。

**IoQueue.h**

标头文件 IoQueue.h 声明队列回调类。

```ManagedCPlusPlus
class CMyIoQueue :
    public CComObjectRootEx<CComMultiThreadModel>,
    public IQueueCallbackDeviceIoControl
{

public:

    DECLARE_NOT_AGGREGATABLE(CMyIoQueue)

    BEGIN_COM_MAP(CMyIoQueue)
        COM_INTERFACE_ENTRY(IQueueCallbackDeviceIoControl)
    END_COM_MAP()

    CMyIoQueue() : 
        m_FxQueue(NULL),
        m_Device(NULL)
    {
    }

    ~CMyIoQueue()
    {
        // empty
    }

    HRESULT
    Initialize(
        __in IWDFDevice *FxDevice,
        __in CMyDevice *MyDevice
        );

    static 
    HRESULT 
    CreateInstanceAndInitialize( 
        __in IWDFDevice *FxDevice,
        __in CMyDevice *MyDevice,
        __out CMyIoQueue**    Queue
        );

    HRESULT
    Configure(
        VOID
        )
    {
        return S_OK;
    }


    // IQueueCallbackDeviceIoControl

    virtual
    VOID
    STDMETHODCALLTYPE
    OnDeviceIoControl( 
        __in IWDFIoQueue *pWdfQueue,
        __in IWDFIoRequest *pWdfRequest,
        __in ULONG ControlCode,
        __in SIZE_T InputBufferSizeInBytes,
        __in SIZE_T OutputBufferSizeInBytes
        );

private:

    IWDFIoQueue *               m_FxQueue;

    CMyDevice *                 m_Device;

};
```

在前面的代码示例中，客户端驱动程序声明队列回调类。 实例化时，该对象是与处理请求调度到客户端驱动程序的方式的 framework 队列对象合作。 类定义创建和初始化 framework 队列对象的两个方法。 静态方法 CreateInstanceAndInitialize 实例化队列回调类，然后调用创建并初始化 framework 队列对象的 Initialize 方法。 它还指定队列对象的调度选项。

```ManagedCPlusPlus
HRESULT 
CMyIoQueue::CreateInstanceAndInitialize(
    __in IWDFDevice *FxDevice,
    __in CMyDevice *MyDevice,
    __out CMyIoQueue** Queue
    )
{

    CComObject<CMyIoQueue> *pMyQueue = NULL;
    HRESULT hr = S_OK;

    TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_QUEUE, "%!FUNC! Entry");

    hr = CComObject<CMyIoQueue>::CreateInstance( &pMyQueue );
    if (FAILED(hr))
    {
        TraceEvents(TRACE_LEVEL_ERROR,
                    TRACE_QUEUE,
                    "%!FUNC! Failed to create instance %!hresult!",
                    hr);
        goto Exit;
    }

    hr = pMyQueue->Initialize(FxDevice, MyDevice);
    if (FAILED(hr))
    {
        TraceEvents(TRACE_LEVEL_ERROR,
                    TRACE_QUEUE,
                    "%!FUNC! Failed to initialize %!hresult!",
                    hr);
        goto Exit;
    }

    *Queue = pMyQueue;

Exit:

    TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_QUEUE, "%!FUNC! Exit");

    return hr;
}
```

下面的代码示例演示了 Initialize 方法的实现。

```ManagedCPlusPlus
HRESULT
CMyIoQueue::Initialize(
    __in IWDFDevice *FxDevice,
    __in CMyDevice *MyDevice
    )
{
    IWDFIoQueue *fxQueue = NULL;
    HRESULT hr = S_OK;
    IUnknown *unknown = NULL;

    TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_QUEUE, "%!FUNC! Entry");

    assert(FxDevice != NULL);
    assert(MyDevice != NULL);

    hr = this->QueryInterface(__uuidof(IUnknown), (void **)&unknown);
    if (FAILED(hr))
    {
        TraceEvents(TRACE_LEVEL_ERROR,
                    TRACE_QUEUE,
                    "%!FUNC! Failed to query IUnknown interface %!hresult!",
                    hr);
        goto Exit;
    }

    hr = FxDevice->CreateIoQueue(unknown,
                                 FALSE,     // Default Queue?
                                 WdfIoQueueDispatchParallel,  // Dispatch type
                                 TRUE,     // Power managed?
                                 FALSE,     // Allow zero-length requests?
                                 &fxQueue); // I/O queue
    DriverSafeRelease(unknown);

    if (FAILED(hr))
    {
        TraceEvents(TRACE_LEVEL_ERROR, 
                   TRACE_QUEUE, 
                   "%!FUNC! Failed to create framework queue.");
        goto Exit;
    }

    hr = FxDevice->ConfigureRequestDispatching(fxQueue,
                                               WdfRequestDeviceIoControl,
                                               TRUE);

    if (FAILED(hr))
    {
        TraceEvents(TRACE_LEVEL_ERROR, 
                   TRACE_QUEUE, 
                   "%!FUNC! Failed to configure request dispatching %!hresult!.",
                   hr);
        goto Exit;
    }

    m_FxQueue = fxQueue;
    m_Device= MyDevice;

Exit:

    DriverSafeRelease(fxQueue);

    TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_QUEUE, "%!FUNC! Exit");

    return hr;
}
```

在前面的代码示例中，客户端驱动程序创建的 framework 队列对象。 该框架提供要处理的请求流到客户端驱动程序的队列对象。

若要创建的对象，客户端驱动程序调用[ **IWDFDevice::CreateIoQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff557020)上[ **IWDFDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff556917)中获得引用对上一个调用[ **IWDFDriver::CreateDevice**](https://msdn.microsoft.com/library/windows/hardware/ff558899)。

在中[ **IWDFDevice::CreateIoQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff557020)调用时，客户端驱动程序指定某些配置选项之前，框架创建队列。 这些选项确定队列是电源管理，允许长度为零的请求，并充当驱动程序的默认队列。 客户端驱动程序提供了此组的信息：

-   对其队列回调类的引用

    指定[ **IUnknown** ](https://msdn.microsoft.com/library/windows/desktop/ms680509)指向其队列回调类。 这将创建 framework 队列对象和客户端驱动程序的队列的回调对象之间的合作。 当 I/O 管理器收到新请求时从应用程序时，它会通知框架。 然后使用该框架**IUnknown**指针来调用由队列回调对象公开的公共方法。

-   默认值或辅助队列

    队列必须是默认的队列或辅助队列。 如果 framework 队列对象充当默认队列，所有请求都添加到队列中。 辅助队列专用于特定类型的请求。 如果客户端驱动程序会请求辅助队列，则该驱动程序还必须调用[ **IWDFDevice::ConfigureRequestDispatching** ](https://msdn.microsoft.com/library/windows/hardware/ff557014)方法，以指示框架必须置于的请求的类型指定的队列。 在模板代码中，客户端驱动程序将传递 FALSE *bDefaultQueue*参数。 指示要创建辅助队列并不默认队列的方法。 更高版本调用**IWDFDevice::ConfigureRequestDispatching**以指示该队列必须具有仅设备 I/O 控制请求 （请参阅本部分中的示例代码）。

-   调度类型

    队列对象的调度类型决定了框架如何提供给客户端驱动程序的请求。 传送机制可以是连续的并行情况下，或由客户端驱动程序定义的自定义机制。 对于顺序队列，直到客户端驱动程序完成上一个请求未传递请求。 在并行调度模式下，框架将请求转发到达从 I/O 管理器时。 这意味着客户端驱动程序可以处理另一个时接收的请求。 在自定义机制中，客户端手动提取从 framework 队列对象，在下一个请求时，驱动程序已准备好对其进行处理。 在模板代码中，并行调度模式的客户端驱动程序请求。

-   电源管理队列

    必须将与设备的即插即用和电源状态同步框架队列对象。 如果设备不处于工作状态，framework 队列对象会停止调度所有请求。 当设备处于工作状态时，队列对象恢复调度。 中电源管理的队列，由框架; 执行的同步否则客户端驱动器必须处理该任务。 在模板代码中，客户端请求的电源管理的队列。

-   允许的长度为零的请求

    客户端驱动程序可以指示框架将会完成 I/O 请求，而不是将它们放在队列的长度为零的缓冲区。 在模板代码中，客户端请求来完成此类请求的框架。

单一框架队列对象可以处理多种类型的请求，如读取、 写入和设备 I/O 控制，等等。 基于模板代码的客户端驱动程序可以处理仅设备 I/O 控制请求。 为此，客户端驱动程序的队列回调类实现[ **IQueueCallbackDeviceIoControl** ](https://msdn.microsoft.com/library/windows/hardware/ff556852)接口并将其[ **IQueueCallbackDeviceIoControl::OnDeviceIoControl** ](https://msdn.microsoft.com/library/windows/hardware/ff556852_ondeviceiocontrol)方法。 这样，框架调用客户端的驱动程序的实现**IQueueCallbackDeviceIoControl::OnDeviceIoControl**框架时处理设备 I/O 控制请求。

对于其他类型的请求，，客户端驱动程序必须实现相应**IQueueCallbackXxx**接口。 例如，如果客户端驱动程序想要处理读取的请求，该队列回调类必须实现[ **IQueueCallbackRead** ](https://msdn.microsoft.com/library/windows/hardware/ff556872)接口并将其[ **IQueueCallbackRead::OnRead** ](https://msdn.microsoft.com/library/windows/hardware/ff556872_onread)方法。 有关请求和回调接口的类型的信息，请参阅[I/O 队列事件回调函数](https://msdn.microsoft.com/library/windows/hardware/ff560424)。

下面的代码示例演示[ **IQueueCallbackDeviceIoControl::OnDeviceIoControl** ](https://msdn.microsoft.com/library/windows/hardware/ff556854)实现。

```ManagedCPlusPlus
VOID
STDMETHODCALLTYPE
CMyIoQueue::OnDeviceIoControl(
    __in IWDFIoQueue *FxQueue,
    __in IWDFIoRequest *FxRequest,
    __in ULONG ControlCode,
    __in SIZE_T InputBufferSizeInBytes,
    __in SIZE_T OutputBufferSizeInBytes
    )
{
    UNREFERENCED_PARAMETER(FxQueue);
    UNREFERENCED_PARAMETER(ControlCode);
    UNREFERENCED_PARAMETER(InputBufferSizeInBytes);
    UNREFERENCED_PARAMETER(OutputBufferSizeInBytes);

    HRESULT hr = S_OK;

    TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_QUEUE, "%!FUNC! Entry");

    if (m_Device == NULL) {
        // We don't have pointer to device object
        TraceEvents(TRACE_LEVEL_ERROR, 
                   TRACE_QUEUE, 
                   "%!FUNC!NULL pointer to device object.");
        hr = E_POINTER;
        goto Exit;
    }

    //
    // Process the IOCTLs
    //

Exit:

    FxRequest->Complete(hr);

    TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_QUEUE, "%!FUNC! Exit");

    return;

}
```

我们来看的队列机制的工作原理。 若要与 USB 设备进行通信，应用程序首次打开设备的句柄并发送设备 I/O 控制请求通过调用[ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/hh404258)与特定的控件代码的函数。 根据控制代码的类型，该应用程序可以在该调用中指定输入和输出缓冲区。 通过 I/O 管理器，它会通知框架，最终接收呼叫。 框架创建框架请求对象，并将其添加到框架队列对象。 在模板代码中，因为 WdfIoQueueDispatchParallel 标志中，创建队列对象调用回调时立即将请求添加到队列。

当框架调用客户端驱动程序的事件回调时，会传递一个句柄的 framework 请求对象，用于保存请求 （和其输入和输出缓冲区） 给发送应用程序。 此外，它将一个句柄发送到包含该请求的 framework 队列对象。 在事件回叫，客户端驱动程序处理请求根据需要。 模板代码只需完成请求。 客户端驱动程序可以执行更复杂的任务。 例如，如果应用程序请求特定设备的信息，在事件回调，客户端驱动程序可以创建 USB 控制请求并将其发送到 USB 驱动程序堆栈，以便检索请求的设备信息。 中讨论了 USB 控制请求[USB 控制传输](usb-control-transfer.md)。

## <a name="driver-entry-source-code"></a>驱动程序条目的源代码


在模板代码中，驱动程序入口 Dllsup.cpp 中实现。

**Dllsup.cpp**

声明之后的 include 部分中，客户端驱动程序的 GUID 常量。 该 GUID 必须与匹配的驱动程序安装文件 (INF) 中的 GUID。

```ManagedCPlusPlus
const CLSID CLSID_Driver =
{0x079e211c,0x8a82,0x4c16,{0x96,0xe2,0x2d,0x28,0xcf,0x23,0xb7,0xff}};
```

下一个代码块声明的客户端驱动程序的类工厂。

```ManagedCPlusPlus
class CMyDriverModule :
    public CAtlDllModuleT< CMyDriverModule >
{
};

CMyDriverModule _AtlModule;
```

模板代码使用 ATL 支持封装复杂的 COM 代码。 类工厂将继承此模板类 CAtlDllModuleT 包含所有所需的代码创建客户端驱动程序。

下面的代码段显示了 DllMain 的实现

```ManagedCPlusPlus
extern "C"
BOOL
WINAPI
DllMain(
    HINSTANCE hInstance,
    DWORD dwReason,
    LPVOID lpReserved
    )
{
    if (dwReason == DLL_PROCESS_ATTACH) {
        WPP_INIT_TRACING(MYDRIVER_TRACING_ID);

        g_hInstance = hInstance;
        DisableThreadLibraryCalls(hInstance);

    } else if (dwReason == DLL_PROCESS_DETACH) {
        WPP_CLEANUP();
    }

    return _AtlModule.DllMain(dwReason, lpReserved);
}
```

如果您的客户端驱动程序实现[ *DllMain* ](https://msdn.microsoft.com/library/windows/desktop/ms682583)函数，Windows 会考虑*DllMain*为客户端驱动程序模块的入口点。 Windows 调用*DllMain*加载 WUDFHost.exe 中的客户端驱动程序模块之后。 Windows 调用*DllMain*再次只是之前 Windows 卸载的客户端驱动程序在内存中。 *DllMain*可以分配和释放在驱动程序级别的全局变量。 在模板代码中，客户端驱动程序初始化和释放 WPP 跟踪所需的资源并调用 ATL 类 DllMain 的实现。

有关如何编写您[ *DllMain*](https://msdn.microsoft.com/library/windows/desktop/ms682583)，请参阅[实现 DllMain](https://msdn.microsoft.com/library/aa370448)。

以下代码片段演示实现 DllGetClassObject。

```ManagedCPlusPlus
STDAPI
DllGetClassObject(
    __in REFCLSID rclsid,
    __in REFIID riid,
    __deref_out LPVOID FAR* ppv
    )
{
    return _AtlModule.DllGetClassObject(rclsid, riid, ppv);
}
```

在模板中的代码的类工厂和[ **DllGetClassObject** ](https://msdn.microsoft.com/library/windows/desktop/ms680760) ATL 中实现 上述代码段只是调用了 ATL **DllGetClassObject**实现。 一般情况下， **DllGetClassObject**必须执行以下任务：

1.  请确保传递由框架的 CLSID 是客户端驱动程序的 GUID。 框架从驱动程序的 INF 文件中检索客户端驱动程序的 CLSID。 在验证，请确保指定的 GUID 匹配一个 INF 中提供。
2.  实例化由客户端驱动程序实现的类工厂。 在模板代码封装由 ATL 类。
3.  获取一个指向[ **IClassFactory** ](https://msdn.microsoft.com/library/windows/desktop/ms694364)接口的类工厂并返回检索到指针到框架。

客户端驱动程序模块加载到内存中后，框架将调用的驱动程序提供[ **DllGetClassObject** ](https://msdn.microsoft.com/library/windows/desktop/ms680760)函数。 框架的调用中**DllGetClassObject**，框架将传递，用于标识客户端驱动程序并请求指向的 CLSID [ **IClassFactory** ](https://msdn.microsoft.com/library/windows/desktop/ms694364)类工厂的接口。 客户端驱动程序实现，从而有助于创建驱动程序回调的类工厂。 因此，客户端驱动程序必须包含至少一个类工厂。 然后，框架将调用[ **IClassFactory::CreateInstance** ](https://msdn.microsoft.com/library/windows/desktop/ms682215) ，并请求[ **IDriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff554885)指向驱动程序回调类。

**Exports.def**

框架调用以便[ **DllGetClassObject**](https://msdn.microsoft.com/library/windows/desktop/ms680760)，客户端驱动程序必须从.def 文件导出函数。 该文件已包含在 Visual Studio 项目中。

```ManagedCPlusPlus
; Exports.def : Declares the module parameters.

LIBRARY     "MyUSBDriver_UMDF_.DLL"

EXPORTS
        DllGetClassObject   PRIVATE
```

在上述代码段中从 Export.def 附带驱动程序项目，客户端提供的库的驱动程序模块的名称和[ **DllGetClassObject** ](https://msdn.microsoft.com/library/windows/desktop/ms680760)下导出。 有关详细信息，请参阅[DLL 使用 DEF 文件从导出](https://msdn.microsoft.com/library/d91k01sh(VS.80).aspx)。








