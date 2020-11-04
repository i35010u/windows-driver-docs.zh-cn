---
description: 了解基于 UMDF 的 USB 客户端驱动程序的源代码。
title: 'USB 客户端驱动程序代码结构 (UMDF) '
ms.date: 06/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: 6890b005d57b936c67643f8c1e84f2fbaa9a2b3f
ms.sourcegitcommit: ec7bebe3f94536455e62b372c2a28fe69d1717f7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/04/2020
ms.locfileid: "93349773"
---
# <a name="understanding-the-usb-client-driver-code-structure-umdf"></a>了解 USB 客户端驱动程序代码结构 (UMDF) 

在本主题中，你将了解基于 UMDF 的 USB 客户端驱动程序的源代码。 代码示例由 Microsoft Visual Studio 2019 附带的 **USB User-Mode 驱动程序** 模板生成。 模板代码使用活动模板库 (ATL) 来生成 COM 基础结构。 此处不讨论有关客户端驱动程序中的 COM 实现的 ATL 和详细信息。

有关生成 UMDF 模板代码的说明，请参阅 [如何编写第一个 USB 客户端驱动程序 (UMDF) ](implement-driver-entry-for-a-usb-driver--umdf-.md)。 以下部分讨论了模板代码：

- [驱动程序回调源代码](#driver-callback-source-code)
- [设备回拨源代码](#device-callback-source-code)
- [队列源代码](#queue-source-code)
- [驱动程序条目源代码](#driver-entry-source-code)

在讨论模板代码的详细信息之前，让我们来看一看标头文件中的一些声明， (与 UMDF 驱动程序开发相关的) 。

Internal 包含这些文件，这些文件包含在 Windows 驱动程序工具包 (WDK) ：

```ManagedCPlusPlus
#include "atlbase.h"
#include "atlcom.h"

#include "wudfddi.h"
#include "wudfusb.h"
```

Atlbase.h 和 atlcom.h 包含 ATL 支持的声明。 由客户端驱动程序实现的每个类都实现 ATL 类 public CComObjectRootEx。

Wudfddi 始终包含在 UMDF 驱动程序开发中。 标头文件包含编译 UMDF 驱动程序所需的方法和结构的各种声明和定义。

Wudfusb 包括与框架提供的 USB i/o 目标对象通信所需的 UMDF 结构和方法的声明和定义。

Internal 中的下一个块声明设备接口的 GUID 常量。 应用程序可以通过使用 **SetupDiXxx** api，使用此 GUID 打开设备的句柄。 GUID 是在框架创建设备对象之后注册的。

```ManagedCPlusPlus
// Device Interface GUID
// f74570e5-ed0c-4230-a7a5-a56264465548

DEFINE_GUID(GUID_DEVINTERFACE_MyUSBDriver_UMDF_,
    0xf74570e5,0xed0c,0x4230,0xa7,0xa5,0xa5,0x62,0x64,0x46,0x55,0x48);
```

下一部分声明跟踪宏和跟踪 GUID。 请注意跟踪 GUID;要启用跟踪，你需要用到它。

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

内部 .h forward 中的下一行将为队列回调对象声明客户端驱动程序实现的类。 它还包括模板生成的其他项目文件。 本主题后面将讨论实现和项目头文件。

```ManagedCPlusPlus
// Forward definition of queue.

typedef class CMyIoQueue *PCMyIoQueue;

// Include the type specific headers.

#include "Driver.h"
#include "Device.h"
#include "IoQueue.h"
```

安装客户端驱动程序之后，Windows 将在主机进程的实例中加载客户端驱动程序和框架。 从这里开始，框架加载并初始化客户端驱动程序。 框架将执行以下任务：

1. 在框架中创建一个表示客户端驱动程序的 *驱动程序对象* 。
2. 从类工厂请求 [IDriverEntry](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-idriverentry) 接口指针。
3. 在框架中创建 *设备对象* 。
4. 在 PnP 管理器启动设备后初始化设备对象。

在加载和初始化驱动程序时，会发生多个事件，框架允许客户端驱动程序对它们进行处理。 在客户端驱动程序端，驱动程序将执行以下任务：

1. 实现并从客户端驱动程序模块中导出 [**DllGetClassObject**](/windows/desktop/api/combaseapi/nf-combaseapi-dllgetclassobject) 函数，使框架可以获取对驱动程序的引用。
2. 提供实现 [IDriverEntry](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-idriverentry) 接口的回调类。
3. 提供实现 **IPnpCallbackXxx** 接口的回调类。
4. 获取对设备对象的引用，并根据客户端驱动程序的要求对其进行配置。

## <a name="driver-callback-source-code"></a>驱动程序回调源代码

框架创建 *驱动程序对象* ，该对象表示 Windows 加载的客户端驱动程序的实例。 客户端驱动程序至少提供一个向框架注册驱动程序的驱动程序回调。

驱动程序回调的完整源代码位于驱动程序 .h 和驱动程序中。

客户端驱动程序必须定义一个实现 [**IUnknown**](/windows/desktop/api/unknwn/nn-unknwn-iunknown) 和 [**IDriverEntry**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-idriverentry) 接口的驱动程序回调类。 标头文件 Driver 声明一个名为 CMyDriver 的类，该类定义驱动程序回调。

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

驱动程序回调必须是 COM 类，这意味着它必须实现 [**IUnknown**](/windows/desktop/api/unknwn/nn-unknwn-iunknown) 和相关方法。 在模板代码中，ATL 类 CComObjectRootEx 和 CComCoClass 包含 **IUnknown** 方法。

Windows 实例化主机进程后，框架会创建驱动程序对象。 为此，该框架会创建驱动程序回调类的实例，并调用 [**DllGetClassObject**](/windows/desktop/api/combaseapi/nf-combaseapi-dllgetclassobject) 的驱动程序实现， (在 [驱动程序输入源代码](#driver-entry-source-code) 部分) 中讨论并获取客户端驱动程序的 [**IDriverEntry**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-idriverentry) 接口指针。 该调用将驱动程序回调对象注册到框架驱动程序对象。 成功注册后，框架将在特定于驱动程序的事件发生时调用客户端驱动程序的实现。 框架调用的第一种方法是 [**IDriverEntry：： OnInitialize**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeinitialize) 方法。 在 **IDriverEntry：： OnInitialize** 的客户端驱动程序实现中，客户端驱动程序可以分配全局驱动程序资源。 这些资源必须在 [**IDriverEntry：： OnDeinitialize**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeinitialize) 中发布，该框架会在准备卸载客户端驱动程序之前由框架调用。 模板代码提供 **OnInitialize** 和 **OnDeinitialize** 方法的最小实现。

[**IDriverEntry**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-idriverentry)的最重要方法是 [**IDriverEntry：： OnDeviceAdd**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)。 在框架创建框架设备对象之前 () 的下一节中进行了讨论，它将调用驱动程序的 **IDriverEntry：： OnDeviceAdd** 实现。 调用方法时，框架会将 [**IWDFDriver**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdriver) 指针传递到驱动程序对象和 [**IWDFDeviceInitialize**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdeviceinitialize) 指针。 客户端驱动程序可以调用 **IWDFDeviceInitialize** 方法来指定某些配置选项。

通常，客户端驱动程序在其 [**IDriverEntry：： OnDeviceAdd**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd) 实现中执行以下任务：

- 为要创建的设备对象指定配置信息。
- 实例化驱动程序的设备回调类。
- 创建框架设备对象，并向框架注册其设备回调对象。
- 初始化框架设备对象。
- 注册客户端驱动程序的设备接口 GUID。

在模板代码中， **IDriverEntry：： OnDeviceAdd** 调用在设备回调类中定义的静态方法 CMyDevice：： CreateInstanceAndInitialize。 静态方法首先实例化客户端驱动程序的设备回调类，然后创建框架设备对象。 设备回调类还定义了一个名为 Configure 的公共方法，该方法执行前面列表中提到的剩余任务。 下一节将讨论设备回调类的实现。
下面的代码示例显示模板代码中的 [**IDriverEntry：： OnDeviceAdd**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd) 实现。

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

下面的代码示例显示了在设备中的设备类声明。

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

## <a name="device-callback-source-code"></a>设备回拨源代码

*框架设备对象* 是一个框架类的实例，它表示在客户端驱动程序的设备堆栈中加载的设备对象。 有关设备对象的功能的信息，请参阅 [设备节点和设备堆栈](../debugger/device-node-and-stack-debugger-commands.md)。

设备对象的完整源代码位于设备 .h 和设备 c 中。

框架设备类实现 [**IWDFDevice**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdevice) 接口。 客户端驱动程序负责在 [**IDriverEntry：： OnDeviceAdd**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)的驱动程序实现中创建该类的实例。 创建对象后，客户端驱动程序将获取指向新对象的 **IWDFDevice** 指针，并调用该接口上的方法来管理设备对象的操作。

### <a name="idriverentryondeviceadd-implementation"></a>IDriverEntry：： OnDeviceAdd 实现

在上一部分中，你将简要了解客户端驱动程序在 [**IDriverEntry：： OnDeviceAdd**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)中执行的任务。 下面是有关这些任务的详细信息。 客户端驱动程序：

- 为要创建的设备对象指定配置信息。

    在对客户端驱动程序的 [**IDriverEntry：： OnDeviceAdd**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd) 方法实现的框架调用中，框架传递 [**IWDFDeviceInitialize**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdeviceinitialize) 指针。 客户端驱动程序使用此指针为要创建的设备对象指定配置信息。 例如，客户端驱动程序指定客户端驱动程序是筛选器还是函数驱动程序。 若要将客户端驱动程序标识为筛选器驱动程序，它将调用 [**IWDFDeviceInitialize：： SetFilter**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdeviceinitialize-setfilter)。 在这种情况下，框架 (FiDO) 创建筛选器设备对象。否则，将创建一个 (FDO) 的函数设备对象。 可以设置的另一个选项是通过调用 [**IWDFDeviceInitialize：： SetLockingConstraint**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdeviceinitialize-setlockingconstraint)同步模式。

- 调用 [**IWDFDriver：： CreateDevice**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createdevice) 方法，方法是传递 [**IWDFDeviceInitialize**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdeviceinitialize) 接口指针、设备回调对象的 [**IUnknown**](/windows/desktop/api/unknwn/nn-unknwn-iunknown) 引用和指向指针的指针 [**IWDFDevice**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdevice) 变量。

    如果 [**IWDFDriver：： CreateDevice**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createdevice) 调用成功：

  - 框架创建设备对象。
  - 框架将设备回调注册到框架。
  
    设备回调与框架设备对象配对后，框架和客户端驱动程序将处理某些事件，例如 PnP 状态和电源状态更改。 例如，当 PnP 管理器启动设备时，框架会得到通知。 然后，框架将调用设备回调的 [**IPnpCallbackHardware：： OnPrepareHardware**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware-onpreparehardware) 实现。 每个客户端驱动程序必须注册至少一个设备回叫对象。

  - 客户端驱动程序接收 [**IWDFDevice**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdevice) 变量中新设备对象的地址。 接收到框架设备对象的指针后，客户端驱动程序可以继续执行初始化任务，如为 i/o 流设置队列和注册设备接口 GUID。

- 调用 [**IWDFDevice：： CreateDeviceInterface**](/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedeviceinterfacea) 来注册客户端驱动程序的设备接口 GUID。 应用程序可以使用 GUID 将请求发送到客户端驱动程序。 GUID 常量在内 .h 中声明。
- 为传入和传出设备的 i/o 初始化队列。

模板代码定义 helper 方法 Initialize，它指定配置信息并创建设备对象。

下面的代码示例演示 Initialize 的实现。

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

在上面的代码示例中，客户端驱动程序创建设备对象并注册其设备回调。 在创建设备对象之前，驱动程序通过在 [**IWDFDeviceInitialize**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdeviceinitialize) 接口指针上调用方法来指定其配置首选项。 这是框架在其之前对客户端驱动程序的 [**IDriverEntry：： OnDeviceAdd**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd) 方法的调用中传递的相同指针。

客户端驱动程序指定它将成为设备对象的电源策略所有者。 作为电源策略所有者，客户端驱动程序将确定在系统电源状态更改时设备应输入的适当电源状态。 驱动程序还负责将相关请求发送到设备，以便进行电源状态转换。 默认情况下，基于 UMDF 的客户端驱动程序不是电源策略所有者;框架处理所有电源状态转换。 当系统进入睡眠状态时，框架会自动将设备发送到 **D3** ，并在系统进入工作状态 **S0** 时将设备恢复为 **D0** 状态。 有关详细信息，请参阅 [UMDF 中的电源策略所有权](../wdf/power-policy-ownership-in-umdf.md)。

另一种配置选项是指定客户端驱动程序是设备的筛选器驱动程序还是功能驱动程序。 请注意，在代码示例中，客户端驱动程序未显式指定其首选项。 这意味着客户端驱动程序是函数驱动程序，框架应在设备堆栈中创建 FDO。 如果客户端驱动程序希望成为筛选器驱动程序，则驱动程序必须调用 [**IWDFDeviceInitialize：： SetFilter**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdeviceinitialize-setfilter) 方法。 在这种情况下，框架将在设备堆栈中创建一个 FiDO。

客户端驱动程序还指定对客户端驱动程序的回调的任何调用都不会同步。 客户端驱动程序处理所有同步任务。 若要指定该首选项，客户端驱动程序将调用 [**IWDFDeviceInitialize：： SetLockingConstraint**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdeviceinitialize-setlockingconstraint) 方法。

接下来，客户端驱动程序通过调用 [**iunknown：： QueryInterface**](/windows/win32/api/unknwn/nf-unknwn-iunknown-queryinterface(q))获取指向其设备回调类的 [**IUnknown**](/windows/desktop/api/unknwn/nn-unknwn-iunknown)指针 https://docs.microsoft.com/windows/desktop/api/unknwn/nf-unknwn-iunknown-queryinterface(q_)) 。 随后，客户端驱动程序将调用 [**IWDFDriver：： CreateDevice**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createdevice)，这将使用 **IUnknown** 指针来创建框架设备对象并注册客户端驱动程序的设备回调。

请注意，客户端驱动程序在设备回调类的私有数据成员中存储 (通过 [**IWDFDriver：： CreateDevice**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createdevice)) 调用接收的设备对象的地址，然后通过调用 DriverSafeRelease) 中定义的 (内联函数来释放该引用。 这是因为设备对象的生存期由框架跟踪。 因此，客户端驱动程序不需要保留设备对象的其他引用计数。

模板代码定义公共方法 "配置"，它将注册设备接口 GUID 并设置队列。 下面的代码示例演示设备回调类 CMyDevice 中的 Configure 方法的定义。 创建框架设备对象后，配置由 [**IDriverEntry：： OnDeviceAdd**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd) 调用。

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

在上面的代码示例中，客户端驱动程序执行两个主要任务：为 i/o 流初始化队列并注册设备接口 GUID。

队列是在 CMyIoQueue 类中创建和配置的。 第一个任务是通过调用名为 CreateInstanceAndInitialize 的静态方法来实例化该类。 客户端驱动程序调用配置以初始化队列。 CreateInstanceAndInitialize 和 Configure 在 CMyIoQueue 中声明，本主题稍后将对此进行讨论。

客户端驱动程序还将调用 [**IWDFDevice：： CreateDeviceInterface**](/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedeviceinterfacea) 来注册客户端驱动程序的设备接口 GUID。 应用程序可以使用 GUID 将请求发送到客户端驱动程序。 GUID 常量在内 .h 中声明。

### <a name="ipnpcallbackhardware-implementation-and-usb-specific-tasks"></a>IPnpCallbackHardware 实现和 USB 特定任务

接下来，让我们看看设备 .cpp 中的 [**IPnpCallbackHardware**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallbackhardware) 接口的实现。

每个设备回调类必须实现 [**IPnpCallbackHardware**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallbackhardware) 接口。 此接口有两种方法： [**IPnpCallbackHardware：： OnPrepareHardware**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware-onpreparehardware) 和 [**IPnpCallbackHardware：： OnReleaseHardware**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware-onreleasehardware)。 框架将调用这些方法来响应两个事件：当 PnP 管理器启动设备时，删除设备。 设备启动时，将建立与硬件的通信，但设备尚未进入工作状态 ( **D0** ) 。 因此，在 **IPnpCallbackHardware：： OnPrepareHardware** 中，客户端驱动程序可以从硬件中获取设备信息、分配资源以及初始化驱动程序生存期内所需的框架对象。 当 PnP 管理器删除设备时，驱动程序将从系统中卸载。 框架调用客户端驱动程序的 **IPnpCallbackHardware：： OnReleaseHardware** 实现，在此实现中，驱动程序可以释放这些资源和框架对象。

PnP 管理器可以生成由 PnP 状态更改导致的其他事件类型。 框架为这些事件提供默认处理。 客户端驱动程序可以选择参与处理这些事件。 请考虑一种情况，其中 USB 设备已从主机中分离。 PnP 管理器识别该事件，并通知框架。 如果客户端驱动程序要执行其他任务来响应事件，则驱动程序必须在设备回调类中实现 [**IPnpCallback**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallback) 接口和相关的 [**IPnpCallback：： OnSurpriseRemoval**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallback-onsurpriseremoval) 方法。 否则，框架将继续对事件进行默认处理。

USB 客户端驱动程序必须检索有关支持的接口、备用设置和终结点的信息，并在为数据传输发送任何 i/o 请求之前对其进行配置。 UMDF 提供专用 i/o 目标对象，这些对象简化了客户端驱动程序的多个配置任务。 若要配置 USB 设备，客户端驱动程序需要仅在 PnP 管理器启动设备后才可用的设备信息。

此模板代码在 [**IPnpCallbackHardware：： OnPrepareHardware**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware-onpreparehardware) 方法中创建这些对象。

通常，客户端驱动程序会根据设备) 的设计， (执行其中一项或多项配置任务：

1. 检索有关当前配置的信息，如接口数。 框架选择 USB 设备上的第一个配置。 如果是多配置设备，则客户端驱动程序无法选择其他配置。
2. 检索有关接口的信息，例如终结点的数目。
3. 如果接口支持多个设置，则更改每个接口内的备用设置。 默认情况下，该框架会选择 USB 设备上第一个配置中的每个接口的第一个备用设置。 客户端驱动程序可以选择选择其他设置。
4. 检索有关每个接口中的终结点的信息。

若要执行这些任务，客户端驱动程序可以使用 WDF 提供的这些类型的专用 USB i/o 目标对象。

| USB i/o 目标对象     | 描述                                                                                                                                                                                                                                                                                                                               | UMDF 接口                                  |
|---------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------|
| *目标设备对象*    | 表示一个 USB 设备，并提供用于检索设备描述符并将控制请求发送到设备的方法。                                                                                                                                                                                                             | [IWDFUsbTargetDevice](/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetdevice) |
| *目标接口对象* | 表示单个接口，并提供客户端驱动程序可调用以选择备用设置和检索有关设置的信息的方法。                                                                                                                                                                          | [IWDFUsbInterface](/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbinterface)       |
| *目标管道对象*      | 表示终结点的单个管道，该终结点在接口的当前替代设置中进行配置。 USB 总线驱动程序选择所选配置中的每个接口，并设置接口中每个终结点的通信通道。 在 USB 术语中，该通信通道称为 *管道* 。 | [IWDFUsbTargetPipe](/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetpipe)     |

下面的代码示例演示了 [**IPnpCallbackHardware：： OnPrepareHardware**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware-onpreparehardware)的实现。

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

若要使用框架的 USB i/o 目标对象，客户端驱动程序必须首先创建 USB 目标设备对象。 在框架对象模型中，USB 目标设备对象是代表 USB 设备的设备对象的子对象。 USB 目标设备对象由框架实现并执行 USB 设备的所有设备级任务，如选择配置。

在上面的代码示例中，客户端驱动程序查询框架设备对象并获取指向创建 USB 目标设备对象的类工厂的 [**IWDFUsbTargetFactory**](/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetfactory) 指针。 通过使用该指针，客户端驱动程序将调用 [**IWDFUsbTargetDevice：： CreateUsbTargetDevice**](/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-retrievedescriptor) 方法。 方法创建 USB 目标设备对象，并返回指向 [**IWDFUsbTargetDevice**](/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetdevice) 接口的指针。 方法还会选择默认 (首先) 配置，并为该配置中的每个接口选择备用设置0。

模板代码存储 USB 目标设备对象的地址 (通过设备回叫类的私有数据成员中的 [**IWDFDriver：： CreateDevice**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createdevice)) 调用接收，然后通过调用 DriverSafeRelease 释放该引用。 USB 目标设备对象的引用计数由框架维护。 只要设备对象处于活动状态，对象就会处于活动状态。 客户端驱动程序必须在 [**IPnpCallbackHardware：： OnReleaseHardware**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware-onreleasehardware)中发布引用。

在客户端驱动程序创建 USB 目标设备对象之后，驱动程序将调用 [**IWDFUsbTargetDevice**](/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetdevice) 方法来执行这些任务：

- 检索设备、配置、接口描述符和其他信息（如设备速度）。
- 将 i/o 控制请求格式化并发送到默认终结点。
- 设置整个 USB 设备的电源策略。

有关详细信息，请参阅 [在 UMDF 中使用 USB 设备](../wdf/working-with-usb-devices-in-umdf-1-x-drivers.md)。
下面的代码示例演示了 [**IPnpCallbackHardware：： OnReleaseHardware**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware-onreleasehardware)的实现。

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

## <a name="queue-source-code"></a>队列源代码

*Framework queue 对象* 表示特定框架设备对象的 i/o 队列。 队列对象的完整源代码位于 IoQueue 和 IoQueue 中。

### <a name="ioqueueh"></a>IoQueue

标头文件 IoQueue 声明队列回调类。

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

在上面的代码示例中，客户端驱动程序声明队列回调类。 在实例化时，对象与框架队列对象合作，该对象用于处理请求分派给客户端驱动程序的方式。 类定义了两个用于创建和初始化框架队列对象的方法。 静态方法 CreateInstanceAndInitialize 实例化队列回调类，然后调用用于创建和初始化框架队列对象的 Initialize 方法。 它还为 queue 对象指定调度选项。

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

在上面的代码示例中，客户端驱动程序将创建框架队列对象。 该框架提供了 queue 对象来处理客户端驱动程序的请求流。

若要创建对象，客户端驱动程序对 [**IWDFDriver：： CreateDevice**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createdevice)的上一个调用中获取的 [**IWDFDevice**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdevice)引用调用 [**IWDFDevice：： CreateIoQueue**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createioqueue) 。

在 [**IWDFDevice：： CreateIoQueue**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createioqueue) 调用中，客户端驱动程序在框架创建队列之前指定某些配置选项。 这些选项确定队列是否处于电源管理状态，是否允许长度为零的请求，并充当驱动程序的默认队列。 客户端驱动程序提供了以下信息集：

- 对其队列回调类的引用

    指定一个指向其队列回调类的 [**IUnknown**](/windows/desktop/api/unknwn/nn-unknwn-iunknown) 指针。 这会在框架队列对象和客户端驱动程序的队列回调对象之间创建合作关系。 当 i/o 管理器接收到来自应用程序的新请求时，它会通知该框架。 然后，框架使用 **IUnknown** 指针调用由队列回调对象公开的公共方法。

- 默认队列或辅助队列

    队列必须是默认队列或辅助队列。 如果框架队列对象充当默认队列，则所有请求都会添加到队列中。 辅助队列专用于特定类型的请求。 如果客户端驱动程序请求辅助队列，则驱动程序还必须调用 [**IWDFDevice：： ConfigureRequestDispatching**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-configurerequestdispatching) 方法以指示框架必须放入指定队列的请求的类型。 在模板代码中，客户端驱动程序在 *bDefaultQueue* 参数中传递 FALSE。 指示方法创建辅助队列而非默认队列的。 稍后，它会调用 **IWDFDevice：： ConfigureRequestDispatching** ，以指示队列必须只有设备 i/o 控制请求 (参阅本部分中的示例代码) 。

- 调度类型

    队列对象的调度类型决定了框架如何向客户端驱动程序发送请求。 传递机制可以是连续的，也可以是由客户端驱动程序定义的自定义机制。 对于顺序队列，在客户端驱动程序完成以前的请求之前，不会传递请求。 在并行调度模式下，框架会在请求到达 i/o 管理器后立即转发请求。 这意味着客户端驱动程序可以在处理另一个请求时收到请求。 在自定义机制中，当驱动程序准备好对其进行处理时，客户端会手动从框架队列对象中提取下一个请求。 在模板代码中，客户端驱动程序请求并行调度模式。

- 电源管理的队列

    框架队列对象必须与设备的 PnP 和电源状态同步。 如果设备未处于工作状态，框架队列对象将停止调度所有请求。 当设备处于工作状态时，队列对象会恢复调度。 在电源管理的队列中，同步由框架执行;否则，客户端驱动器必须处理该任务。 在模板代码中，客户端请求一个电源管理的队列。

- 允许长度为零的请求

    客户端驱动程序可以指示框架用长度为零的缓冲区来完成 i/o 请求，而不是将其放在队列中。 在模板代码中，客户端请求框架完成此类请求。

单个框架队列对象可以处理多种类型的请求，如读取、写入和设备 i/o 控制等。 基于模板代码的客户端驱动程序只能处理设备 i/o 控制请求。 为此，客户端驱动程序的队列回调类实现 [**IQueueCallbackDeviceIoControl**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iqueuecallbackdeviceiocontrol) 接口及其 [**IQueueCallbackDeviceIoControl：： OnDeviceIoControl**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackdeviceiocontrol-ondeviceiocontrol) 方法。 这允许框架在框架处理设备 i/o 控制请求时调用 **IQueueCallbackDeviceIoControl：： OnDeviceIoControl** 的客户端驱动程序实现。

对于其他类型的请求，客户端驱动程序必须实现相应的 **IQueueCallbackXxx** 接口。 例如，如果客户端驱动程序要处理读取请求，则队列回调类必须实现 [**IQueueCallbackRead**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iqueuecallbackread) 接口及其 [**IQueueCallbackRead：： OnRead**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackread-onread) 方法。 有关请求和回调接口的类型的信息，请参阅 [I/o 队列事件回调函数](../wdf/i-o-queue-event-callback-functions.md)。

下面的代码示例演示了 [**IQueueCallbackDeviceIoControl：： OnDeviceIoControl**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackdeviceiocontrol-ondeviceiocontrol) 实现。

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

让我们看看队列机制是如何工作的。 若要与 USB 设备通信，应用程序首先会打开设备的句柄，并通过使用特定控制代码调用 [**DeviceIoControl**](/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol) 函数来发送设备 i/o 控制请求。 根据控制代码的类型，应用程序可以在该调用中指定输入和输出缓冲区。 调用最终由 i/o 管理器接收，通知框架。 框架创建框架请求对象并将其添加到框架队列对象。 在模板代码中，因为队列对象是用 WdfIoQueueDispatchParallel 标志创建的，所以，一旦向队列中添加了该请求，就会调用该回调。

当框架调用客户端驱动程序的事件回调时，它会将句柄传递给包含请求 (的框架请求对象及其输入和输出缓冲区) 应用程序发送。 此外，它还向包含该请求的框架队列对象发送句柄。 在事件回调中，客户端驱动程序会根据需要处理请求。 模板代码只完成请求。 客户端驱动程序可以执行更多涉及的任务。 例如，如果应用程序请求某些设备信息，则在事件回调中，客户端驱动程序可以创建 USB 控制请求并将其发送到 USB 驱动程序堆栈以检索请求的设备信息。 Usb 控件 [传输](usb-control-transfer.md)中讨论了 usb 控制请求。

## <a name="driver-entry-source-code"></a>驱动程序条目源代码

在模板代码中，驱动程序条目是在 Dllsup 中实现的。

### <a name="dllsupcpp"></a>Dllsup .cpp

在包含部分后，将声明客户端驱动程序的 GUID 常量。 该 GUID 必须与驱动程序的安装文件中的 GUID 匹配 (INF) 。

```ManagedCPlusPlus
const CLSID CLSID_Driver =
{0x079e211c,0x8a82,0x4c16,{0x96,0xe2,0x2d,0x28,0xcf,0x23,0xb7,0xff}};
```

下一个代码块声明客户端驱动程序的类工厂。

```ManagedCPlusPlus
class CMyDriverModule :
    public CAtlDllModuleT< CMyDriverModule >
{
};

CMyDriverModule _AtlModule;
```

模板代码使用 ATL 支持来封装复杂的 COM 代码。 类工厂继承了模板类 Catldllmodulet 用作基类，其中包含用于创建客户端驱动程序的所有必要代码。

以下代码片段显示了如何实现 DllMain

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

如果客户端驱动程序实现 [*DllMain*](/windows/desktop/Dlls/dllmain) 函数，Windows 会将 *DllMain* 视为客户端驱动程序模块的入口点。 在 WUDFHost.exe 中加载客户端驱动程序模块后，Windows 将调用 *DllMain* 。 Windows 在内存中卸载客户端驱动程序之前，将再次调用 *DllMain* 。 *DllMain* 可以在驱动程序级别分配和释放全局变量。 在模板代码中，客户端驱动程序初始化并释放 WPP 跟踪所需的资源，并调用 ATL 类的 DllMain 实现。

下面的代码段演示了 DllGetClassObject 的实现。

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

在模板代码中，类工厂和 [**DllGetClassObject**](/windows/desktop/api/combaseapi/nf-combaseapi-dllgetclassobject) 在 ATL 中实现。 上面的代码段只调用 ATL **DllGetClassObject** 实现。 通常， **DllGetClassObject** 必须执行以下任务：

1. 确保框架传递的 CLSID 是客户端驱动程序的 GUID。 框架从驱动程序的 INF 文件中检索客户端驱动程序的 CLSID。 在验证时，请确保指定的 GUID 与在 INF 中提供的 GUID 匹配。
2. 实例化由客户端驱动程序实现的类工厂。 在模板代码中，此由 ATL 类封装。
3. 获取指向类工厂的 [**IClassFactory**](/windows/desktop/api/unknwnbase/nn-unknwnbase-iclassfactory) 接口的指针，并将检索到的指针返回到该框架。

在内存中加载客户端驱动程序模块后，框架将调用驱动程序提供的 [**DllGetClassObject**](/windows/desktop/api/combaseapi/nf-combaseapi-dllgetclassobject) 函数。 在框架对 **DllGetClassObject** 的调用中，框架传递标识客户端驱动程序的 CLSID，并请求指向类工厂的 [**IClassFactory**](/windows/desktop/api/unknwnbase/nn-unknwnbase-iclassfactory) 接口的指针。 客户端驱动程序实现了用于简化驱动程序回调创建的类工厂。 因此，客户端驱动程序必须包含至少一个类工厂。 然后，框架将调用 [**IClassFactory：： CreateInstance**](/windows/desktop/api/unknwn/nf-unknwn-iclassfactory-createinstance) 并请求指向驱动程序回调类的 [**IDriverEntry**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-idriverentry) 指针。

## <a name="exportsdef"></a>导出 .def

为了使框架可以调用 [**DllGetClassObject**](/windows/desktop/api/combaseapi/nf-combaseapi-dllgetclassobject)，客户端驱动程序必须从 .def 文件中导出函数。 此文件已包含在 Visual Studio 项目中。

```ManagedCPlusPlus
; Exports.def : Declares the module parameters.

LIBRARY     "MyUSBDriver_UMDF_.DLL"

EXPORTS
        DllGetClassObject   PRIVATE
```

在上面的代码片段中，从驱动程序项目附带的 .def 导入，客户端将驱动程序模块的名称作为库提供，并在导出下提供 [**DllGetClassObject**](/windows/desktop/api/combaseapi/nf-combaseapi-dllgetclassobject) 。 有关详细信息，请参阅 [使用 DEF 文件从 DLL 导出](https://www.microsoft.com/download/details.aspx?id=55984)。